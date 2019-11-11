<!---
Copyright IBM Corp. 2018, 2019
--->

# IBM Cloud Private Node

This template will add worker, proxy, and management nodes to your existing IBM Cloud Private cluster. 

##### This template can be used to add nodes to ICP deployed using [ICP Medium](https://github.com/IBM-CAMHub-Open/template_icp_installer_medium) and [ICP HA](https://github.com/IBM-CAMHub-Open/template_icp_installer) templates. 

For more infomation on IBM Cloud Private, refer to the [ICP knowledge center](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.2.1/getting_started/architecture.html)

## IBM Cloud Private Versions

| ICP Version | GitTag Reference|
|------|:-------------:|
| 3.2.1  | 3.2.1|

## System Requirements

### Hardware requirements

IBM Cloud Private nodes must meet the following [hardware requirements](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.2.1/supported_system_config/hardware_reqs.html)

***Notes***
Disk 1: Base Disk Size on virtual machine
Disk 2: Additonal Disk on virtual Machine

- GlusterFS is required only if the added node is Worker node.


### Supported operating systems and platforms

The following operating systems and platforms are supported.

***Ubuntu 16.04 LTS***

- On VMware VMware Tools must be enabled in the image for VMWare template.
- Ubuntu Repositories with correct configuration must be enabled in the images.
- Sudo User and password must exist and be allowed for use.
- Firewall (via iptables) must be disabled.
- SELinux must be disabled.
- The system umask value must be set to 0022.

### Network Requirements

The following network information is required:
Based on the Standard setup:

- IP Address
  - 1 IP Address / node
- Netmask Bit Number eg 24
- Network Gateway
- Interface Name

## Template Input Variables for VMware template

The following tables list the template variables for VMware deployments.

### Cloud Input Variables

| Name | Description | Type | Default |
|------|-------------|:----:|:-----:|
| vsphere_datacenter |vSphere DataCenter Name| string |  |
| vsphere_resource_pool | vSphere Resource Pool | string |  |
| vm_network_interface_label | vSphere Port Group Name | string | `VM Network` |
| vm_folder | vSphere Folder Name | string |  |

### IBM Cloud Private Template Settings

| Name | Description | Type | Default |
|------|-------------|:----:|:-----:|
| vm_dns_servers | IBM Cloud Private DNS Servers | list | `<list>` |
| vm_dns_suffixes | IBM Cloud Private DNS Suffixes | list | `<list>` |
| vm_domain | IBM Cloud Private Domain Name | string | `ibm.com` |
| vm_os_user | Virtual Machine  Template User Name | string | `root` |
| vm_os_password | Virtual Machine Template User Password | string |  |
| vm_template | Virtual Machine Template Name | string |  |
| vm_disk1_datastore | Virtual Machine Datastore Name - Disk 1 | string |  |
| vm_disk2_datastore | Virtual Machine Datastore Name - Disk 2 | string |  |
| vm_clone_timeout | The timeout, in minutes, to wait for the virtual machine clone to complete. | string | 30 |

### IBM Cloud Private Deployment Information

| Name | Description | Type | Default |
|------|-------------|:----:|:-----:|
| boot_vm_ipv4_address | Boot Node IP Address | string | |
| master_vm_ipv4_address | Master Node IP Address | string | |
| cluster_location | IBM Cloud Private Cluster Folder | string | /root/ibm-cloud-private-x86_64-3.2.1/cluster |

### New Nodes Input Settings

| Name | Description | Type | Default |
|------|-------------|:----:|:-----:|
| node_type | New Node Type. Valid values are Management or Proxy (HA only) or Worker or Vulnerability Advisor | option | `Worker` |
| worker_memory | New Node Memory Allocation (mb) | string | `16384` |
| worker_vcpu | New Node vCPU Allocation | string | `16` |
| worker_vm_disk1_size | New Node Disk Size (GB) | string | `200` |
| worker_enable_glusterFS | Enable IBM Cloud Private GlusterFS on new Nodes (Worker Node only) | string | `true` |
| worker_vm_disk2_size | New Node Disk Size (GB) - Disk 2 | string |  |
| worker_hostname_ip | New Node Hostname and IP Address | map | |
| worker_vm_ipv4_gateway |New Node IP Gateway  | string |  |
| worker_vm_ipv4_prefix_length | New Node IP Netmask (CIDR) | string | `24` |

## Template Input Variables for OpenStack template

The following tables list the template variables for OpenStack deployments.

### IBM Cloud Private Template Settings

| Name | Description | Type | Default |
|------|-------------|:----:|:-----:|
| vm_security_groups | Virtual Machine OpenStack Security Groups | list | |
| vm_public_ip_pool | Virtual Machine OpenStack Public IP Pool | string | |
| vm_domain | IBM Cloud Private Domain Name | string | |
| vm_image_id | Virtual Machine OpenStack Image ID | string | |
| vm_os_user | Virtual Machine  Template User Name | string | `root` |
| vm_os_password | Virtual Machine Template User Password | string |  |

### IBM Cloud Private Deployment Information

| Name | Description | Type | Default |
|------|-------------|:----:|:-----:|
| boot_vm_ipv4_address | Boot Node IP Address | string | |
| master_vm_ipv4_address | Master Node IP Address | string | |
| cluster_location | IBM Cloud Private Cluster Folder | string | /root/ibm-cloud-private-x86_64-3.2.1/cluster |

### New Nodes Input Settings

| Name | Description | Type | Default |
|------|-------------|:----:|:-----:|
| node_type | New Node Type. Valid values are Management or Proxy (HA only) or Worker or Vulnerability Advisor | option | `Worker` |
| worker_vm_flavor_id | New Node Flavor ID | string | |
| worker_vm_disk1_size | New Node Disk Size (GB) | string | `200` |
| worker_enable_glusterFS | Enable IBM Cloud Private GlusterFS on new Nodes (Worker Node only) | string | `true` |
| worker_vm_disk2_size | New Node Disk Size (GB) - Disk 2 | string |  |
| worker_hostname_ip | New Node Hostname and IP Address | map | |

## Template Output Variables

| Name | Description |
|------|-------------|
| ibm_cloud_private_admin_url | IBM Cloud Private Cluster URL |
