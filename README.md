We will use terraform with openstack and ansible. Terraform will be leveraging the deployment an infrastructure on OpenStack. Ansible will provision the deployed machines.

Step 1:
install Terraform on your host machine or use virtual machine(Vagrant provides you a virtual machine with the software required to run Terraform).


Step2:

Create terraform provider file named as terraform-provider.tf


Step3:

Now next step is to create terraform-instances.tf and terraform-networks.tf file
In  terraform-networks.tf, we are creating a frontend network, a subnet and defining a security group.
In file terraform-instances.tf, we are defining two web servers and one load balancer. It then assigns them to a network, a security group, and a subnet.


Step4:

You should have public-private keypair.This keypair will be stored at /home/.ssh/. Your pair of keys will be imported by Terraform (terraform.tfvars).


Step5:

Next step is use terraform to create infra. Terraform has five essential commands that allow us to deal with an end-to-end workflow.
-> terraform init: This command is used to initialize a working directory containing Terraform configuration files.
-> terraform refresh: This command is used to reconcile the state Terraform knows about (via its state file) with the real- world infrastructure.
-> terraform plan: Creates an execution plan. Terraform performs a refresh, and then determines what actions are necessary to achieve the desired state specified in the configuration files.
-> terraform apply: Apply the changes required to reach the desired state of the configuration.
terraform destroy: destroys Terraform-managed infrastructure.

Firstly, we need to initialize the working directory. This is the first command that should be run after writing a new Terraform configuration. Run:
$ terraform init

In order you to know what are the changes that Terraform has to do on the provider, run:
$ terraform plan

It’s now time to deploy the infrastructure. Run:
$ terraform apply

By now, your infrastructure has been deployed.


Step6:

To provision the machines, we are going to use Ansible.To tell Ansible which machines to target, replace the IPs of the machines on the file hosts. If you can not find them, run terraform output. Now, run the playbook which installs Node with:
$ ansible-playbook site-servers-setup-all.yml


