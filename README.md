# Ansible Cloud Provisioning Role
This roles provisions virtual machines to cloud targets. At this point, only `vSphere` is supported, but roles can be built for any cloud provider.

## Layout

### `provision.yml`
Invocation point

### `/roles`
Directory for new roles. The only role currently is `provision.vmware`

### `/roles/provision.vmware/tasks`
Directory for tasks for vSphere VM provisioning

## Variables

### Hidden (these don't show up in the playbooks, but must be passed in)
- `vcenter_hostname` - FQDN of vSphere API host
- `vcenter_username` - user of service account that can perform vSphere operations
- `vcenter_password` - password of service account

### Visible
- `provision_notes` - Annotation for VM
- `provision_vmware_template` - name of VM template to clone from
- `provision_vmware_datacenter` - name of VMware datacenter to provision to
- `provision_vmware_folder` - folder name to add VM to
- `provision_vmware_cluster` - which ESXi cluster to use. Do not use with `provision_vmware_esxi_hostname`
- `provision_vmware_esxi_hostname` which ESXi host to use. Do not use with `provision_vmware_cluster`
- `provision_cpus` - number of CPUs to use (configured to 1 cpu core per socket)
- `provision_memory` - memory in GB
- `provision_resource_names` - Iterable list of VM names. Do not manually set if using Tower/AWX (see below)
- `provision_extra_disks` - Iterable list of extra disks. Do not manually set if using Tower/AWX (see below)

### Ansible Tower/AWX
These variables are designed to be used in an Ansible Tower/AWX survey.
- `provision_resource_names_textarea` - textarea variable for VM names
- `provision_extra_disks_textarea` - textarea variable for extra disks