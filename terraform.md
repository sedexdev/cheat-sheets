# Terraform

Cloud provisioning toolchain for declarative infrastructure scripting using IaC

# Setup

<code>terraform</code> - Shows all available commands</br>
<code>terraform init</code> - Initialise the Terraform provider</br>

# Planning

<code>terraform validate</code> - Validate the configuration is valid</br>
<code>terraform plan</code> - Show the changes <apply> will make</br>
<code>terraform plan -out=[path].plan</code> - Show the changes <apply> will make and save to file at [path].plan</br>
<code>terraform show -no-color [path].plan > [path].txt</code> - Convert the file [path].plan to readable format</br>

# Provisioning

<code>terraform apply</code> - Apply the change to deploy resources</br>
<code>terraform apply --auto-approve</code> - Apply the change to deploy resources and auto approve deployment</br>
<code>terraform apply -target [resource.name]</code> - Apply the change to deploy target resource</br>
<code>terraform apply -var [variable_name]</code> - Apply the change and assign variable value</br>
<code>terraform apply -var-file [file_name]</code> - Apply the change and provide variable file (.tfvars)</br>

# Destroying

<code>terraform destroy</code> - Destroy configuration file resources (can also comment out/delete resources from the file)</br>
<code>terraform destroy -target [resource.name]</code> - Destroy the target resource</br>

# State

<code>terraform state list</code> - List all resources and their properties</br>
<code>terraform state show [resource.name]</code> - List single resource and its properties</br>
<code>terraform refresh</code> - Refresh state (including showing outputs)</br>

# Outputs

<code>terraform output</code> - Show configuration outputs</br>
