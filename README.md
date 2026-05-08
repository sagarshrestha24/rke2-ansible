Kubernetes Cluster Deployment Using RKE2 with ArgoCD via Ansible under LB
=========
```
               ,        ,  _______________________________
   ,-----------|'------'|  |                             |
  /.           '-'    |-'  |_____________________________|
 |/|             |    |
   |   .________.'----'    _______________________________
   |  ||        |  ||      |                             |
   \__|'        \__|'      |_____________________________|

|‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾|
|________________________________________________________|

|‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾|
|________________________________________________________|
```
Overview
-------

This guide provides a step-by-step process for setting up a Kubernetes cluster using RKE2 (Rancher’s next-generation Kubernetes distribution) and deploying ArgoCD and its applications with Ansible. This setup includes configuring the control plane and worker nodes for the RKE2 cluster and installing ArgoCD for GitOps-based application management.

Unofficial Rancher Government Repository
---------

Support: Please note that the code provided in this repository is not supported under any official support subscriptions. While we strive to ensure the quality and functionality of our code, we provide it on an "as-is" basis and make no guarantees regarding its performance.

Issues: We understand that issues may arise, and while we do not offer formal support, we will address reported issues on a "best effort" basis. We encourage users to report any problems or bugs they encounter, and we will do our best to address them in a timely manner.

Contributions: Contributions to this repository are welcome! If you have improvements or fixes, please feel free to submit a pull request. We appreciate your efforts to improve the quality and effectiveness of this code.

Thank you for your understanding and cooperation.

Ansible RKE2 (RKE Government) Playbook
---------


RKE2, also known as RKE Government, is Rancher's next-generation Kubernetes distribution. This Ansible  playbook installs RKE2 for both the control plane and workers.

See the [docs](https://docs.rke2.io/) more information about [RKE Government](https://docs.rke2.io/).


Platforms
---------
The RKE2 Ansible playbook supports all [RKE2 Supported Operating Systems](https://docs.rke2.io/install/requirements/#operating-systems)

Supported Operating Systems:
- SLES 15
- Rocky 8 and 9
- RedHat: 8 and 9
- Ubuntu: 18, 20, and 22


System requirements
-------------------

Deployment environment must have Ansible 2.9.0+

Server and agent nodes must have passwordless SSH access

Installation
-------------

Step 1: Install Ansible and kubectl on Deployment Bastion
---------------------------------------------------------

```
sudo yum install epel-release
sudo yum install ansible
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```


Step 2: Clone the GitHub Repository
----------------------------------

```
git clone https://github.com/01cloud/inl-infra.git
cd rke2-ansible/
```

Step 3: Install Required Ansible Collections
--------------------------------------------
```
ansible-galaxy collection install -r requirements.yml
```
Step 4: Configure Inventory
---------------------------


Edit `inventory/my-cluster/hosts.yml` to match the system information gathered above. For example:

```yml
all:
  hosts:
    192.168.3.44:
      ansible_user: ec2-user
      hostname: rke-worker1.labenv.ai
      ansible_host: 192.168.3.44
    192.168.2.134:
      ansible_user: ec2-user
      hostname: rke-worker2.labenv.ai
      ansible_host: 192.168.2.134
    192.168.2.226:
      ansible_user: ec2-user
      hostname: rke-server1.labenv.ai
      ansible_host: 192.168.2.226
    192.168.3.205:
      ansible_user: ec2-user
      hostname: rke-server2.labenv.ai
      ansible_host: 192.168.3.205
    192.168.3.32:
      ansible_host: 192.168.3.32
      ansible_user: ec2-user
      hostname: rke-server3.labenv.ai   
    192.168.3.186:
      ansible_host: 192.168.3.186
      ansible_user: ec2-user
      hostname: rke-lb.labenv.ai
    192.168.3.165:
      ansible_host: 192.168.3.165
      ansible_user: ec2-user
      hostname: etcd-1.labenv.ai
    192.168.2.138:
      ansible_host: 192.168.2.138
      ansible_user: ec2-user
      hostname: etcd-2.labenv.ai
    192.168.3.66:
      ansible_host: 192.168.3.66
      ansible_user: ec2-user
      hostname: etcd-3.labenv.ai
  vars:
    host_entries:
      - 192.168.3.186 rke-lb.labenv.ai
      - 192.168.2.226 rke-server1.labenv.ai
      - 192.168.3.205 rke-server2.labenv.ai
      - 192.168.3.32 rke-server3.labenv.ai
      - 192.168.3.44 rke-worker1.labenv.ai
      - 192.168.2.134 rke-worker2.labenv.ai
      - 192.168.3.165 etcd-1.labenv.ai
      - 192.168.2.138 etcd-2.labenv.ai
      - 192.168.3.66 etcd-3.labenv.ai
    kubernetes_api_server_host: "rke-lb.labenv.ai"
    kubeconfig_path: "/home/ansible/.kube/config"
    values_file_path: "/home/ansible/project/coreii/k8s/ansible/roles/argocd-install/values.yaml"
    install_rke2_version: v1.31.1+rke2r2
    # # In air-gapped envs, it might be convenient to download the tar files from custom URLs
    rke2_image_tar_urls:
    - https://github.com/rancher/rke2/releases/download/v1.31.1%2Brke2r1/rke2-images-canal.linux-amd64.tar.zst
    - https://github.com/rancher/rke2/releases/download/v1.31.1%2Brke2r1/rke2-images-core.linux-amd64.tar.zst
rke2_cluster:
  children:
    rke2_lb: 
      hosts:
        192.168.3.186:
    rke2_servers:
      hosts:
        192.168.3.165:
          rke2_config:
             disable-apiserver: true
             disable-controller-manager: true
             disable-scheduler: true
             selinux: true
             tls-san:
             - rke-lb.labenv.ai
             - etcd-1.labenv.ai
             - etcd-2.labenv.ai
             - etcd-3.labenv.ai
             - rke-server1.labenv.ai
             - rke-server2.labenv.ai
             - rke-server3.labenv.ai
          node_taints:
          - CriticalAddonsOnly=true:NoSchedule
        192.168.2.138:
          rke2_config:
             disable-apiserver: true
             disable-controller-manager: true
             disable-scheduler: true
             selinux: true
             tls-san:
             - rke-lb.labenv.ai
             - etcd-1.labenv.ai
             - etcd-2.labenv.ai
             - etcd-3.labenv.ai
             - rke-server1.labenv.ai
             - rke-server2.labenv.ai
             - rke-server3.labenv.ai
          node_taints:
          - CriticalAddonsOnly=true:NoSchedule
        192.168.3.66:
          rke2_config:
             disable-apiserver: true
             disable-controller-manager: true
             disable-scheduler: true
             selinux: true
             tls-san:
             - rke-lb.labenv.ai
             - etcd-1.labenv.ai
             - etcd-2.labenv.ai
             - etcd-3.labenv.ai
             - rke-server1.labenv.ai
             - rke-server2.labenv.ai
             - rke-server3.labenv.ai
          node_taints:
          - CriticalAddonsOnly=true:NoSchedule
        192.168.2.226:
          rke2_config:
            disable-etcd: true
            selinux: true
            tls-san:
             - rke-lb.labenv.ai
             - etcd-1.labenv.ai
             - etcd-2.labenv.ai
             - etcd-3.labenv.ai
             - rke-server1.labenv.ai
             - rke-server2.labenv.ai
             - rke-server3.labenv.ai
          node_taints:
          - CriticalAddonsOnly=true:NoSchedule
        192.168.3.205:
          rke2_config:
            disable-etcd: true
            selinux: true
            tls-san:
             - rke-lb.labenv.ai
             - etcd-1.labenv.ai
             - etcd-2.labenv.ai
             - etcd-3.labenv.ai
             - rke-server1.labenv.ai
             - rke-server2.labenv.ai
             - rke-server3.labenv.ai
          node_taints:
          - CriticalAddonsOnly=true:NoSchedule
        192.168.3.32:
          rke2_config:
            disable-etcd: true
            selinux: true
            tls-san:
             - rke-lb.labenv.ai
             - etcd-1.labenv.ai
             - etcd-2.labenv.ai
             - etcd-3.labenv.ai
             - rke-server1.labenv.ai
             - rke-server2.labenv.ai
             - rke-server3.labenv.ai
          node_taints:
          - CriticalAddonsOnly=true:NoSchedule
    rke2_agents:
      vars:
        rke2_config:
          node-label:
            - agentGroupLabel=true
      hosts:
        192.168.3.44:
          node_labels:
            - agent0Label=true
        192.168.2.134:
          node_labels:
            - agent1Label=true

```

Here's a summarized breakdown of the provided YAML inventory and variables setup for an RKE2 (Rancher Kubernetes Engine 2) cluster configuration with Ansible:
#### 1. Host Definitions (`all: hosts`)

This section lists the servers (both control plane and worker nodes) along with their specific details

  - IP Address: Each host's IP address (e.g., 192.168.3.44).

  - ansible_user: The user that Ansible will use to connect to the server (ec2-user).
  - hostname: The internal hostname for each server (e.g., rke-worker1.labenv.ai).
  - ansible_host: Defines the IP address Ansible will use for connection, which can be different if needed.

#### 2. Variables (`Under vars`)

  - host_entries: This is a list of IP-hostname mappings. It defines all hosts involved in the cluster for easy reference and possibly to add entries to /etc/hosts on each server.
  - kubernetes_api_server_host: Specifies the hostname for the API server (the main endpoint for cluster control). Here, it’s set to the load balancer (rke-lb.labenv.ai).
  - install_rke2_version: Sets the version of RKE2 to be installed (v1.31.1+rke2r2).
  - rke2_image_tar_urls: Lists URLs to the tar files for RKE2 container images. These are useful for air-gapped (isolated) environments where external internet access is restricted.

#### 3. Groupings (`rke2_cluster: children`)

This section organizes hosts into groups based on their role within the RKE2 cluster:

  - rke2_lb: Contains the load balancer host (192.168.3.186) that will distribute network traffic across the RKE2 servers.
  - rke2_servers:
      - Hosts for RKE2 control plane servers, responsible for managing the cluster state and running essential components like the API server.
      - rke2_config:
          - selinux: true: Enables SELinux (Security-Enhanced Linux) on each server for enhanced security.
          - tls-san: Defines a list of additional hostnames and IPs that should be trusted when making secure connections to the API server. This allows external systems or nodes to communicate with the API server using these names or IPs.
      - node_taints: Applies taints on specific nodes (NoSchedule policy) to control which workloads can be scheduled on them, usually marking them as critical for control plane components only.
  - rke2_agents:
      - Defines the worker nodes that will run workloads (user applications) in the cluster.
      - node-label: Adds labels at the group level to categorize or group worker nodes, like agentGroupLabel=true.
      - node_labels: Adds specific labels to each node individually, e.g., agent0Label=true and agent1Label=true. These labels can be used for scheduling purposes in Kubernetes (like targeting certain nodes for specific workloads).

#### Key Points to Remember:

  - `hosts` Section: Lists each server’s details to allow Ansible to connect and manage them.
  - `vars` Section: Sets cluster-wide variables like host entries, the API server host, and RKE2 installation details.
  - `children` Section: Groups the hosts by role (load balancer, control plane servers, agent/worker nodes) to define distinct configurations and behaviors for each role within the cluster.
  - Labels and Taints: `node_labels` and `node_taints` help manage workload scheduling, targeting specific nodes based on their role in the cluster.



Step 5: Run the Final Playbook
-------------------------------------------------------
Run the playbook to set up the RKE2 cluster and install ArgoCD:
```
ansible-playbook install_rke2.yml -i inventory/my-cluster/hosts.yml
```

Uninstall RKE2
---------------
    Note: Uninstalling RKE2 deletes the cluster data and all of the scripts.
The offical documentation for fully uninstalling the RKE2 cluster can be found in the [RKE2 Documentation](https://docs.rke2.io/install/uninstall/).

If you used this module to created the cluster and RKE2 was installed via yum, then you can attempt to run this command to remove all cluster data and all RKE2 scripts.


Run the playbook with the following command to uninstall RKE2 on all server and agent nodes:

```bash
ansible-playbook -i inventory/my-cluster/hosts.yml uninstall_rke2.yml
```
