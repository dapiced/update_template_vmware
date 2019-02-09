# Description

### This playbook makes it possible to update the official vmware (template) AKA rhel image in an automated way by incrementing the image by 1: EX: rhel75001 to rhel75002.


# Prerequisites

> Endpoints with python 3.6 and pyvmomi module

> Obviously at least one image starting with a specific words ex: "rhel" (+ digital) must exist on vmware env.

> The name of templates vmware linux must always begin with a specific words ex: "rhel" with numerical at the end to be able to make the incrementation

> Have access to vmware with a read and write account 

> a reserved IP address  (vmtemp) on the DNS for the temporary vm for which it can be updated with Redhat Satellite

> vm_shell_args need to be changed according to your network

> yum method and redhat satellite is needed


# flow of the playbook

> name: Get template vmware_vm_facts

> name: Increment by 1 the next no. of the current template in VMware for rhel
  
> name: Clone the current template as a temporary VM

> name: Pause the time the clone complete     
 
> name: Assign an IP to the temporary VM

> name: Restart the network of the temporary VM
 
> name: Installation katello>ca>consumer>latest.noarch.rpm from {{ sat6_fqdn }}
 
> name: Subcribe to Satellite image vra

> name: Installation katello-agent
 
> name: update rpm

> name: De-registration of the server at Redhat Satellite
  
> name: Removing subscriptions from the temporary vm

> name: Removing the Satellite Temporary vm
 
> name: Removing the IP Temporary vm

> name: Reset the initial network
  
> name: Shutdown the temporary VM

> name: Get VM name uuid to rename the VM

> name: Rename the VM to the next current template

> name: Convert VM to template in increment no. template
 
> name: Playbook Done! The new current template is now:XXXX
