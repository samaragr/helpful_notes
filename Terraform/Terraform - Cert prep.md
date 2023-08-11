Type: #terraform #general 
## IaC
- define cloud and on-prem resources that are versionable, can be reused and shared

## Advantages of IaC Patterns
- Consistency - across builds and environments
- Repeatability - reuse common code for deployment
- Efficiency - allows ops teams to integrate with dev teams
- Reduces risks and costs

## Advantages of terraform
- provider agnostic 
- Benefits of state (terraform.tfstate)
	- Idempotence - only updates what has changed
	- deduces dependencies 
	- performance -  `-refresh=false` flag to skip state refresh, `-target` flag to refresh specific resource
	- collaborate without overwriting

## Terraform architecture
- Written in Go - uses plug-ins to communicate with providers using an RPC interface, keeps terraform binary small, allows for independent provider updates

## Providers
- use aliases to enable multiple instances of a provider
- Terraform will automatically download plugins from sources identified in the `required_providers` block when a configuration is initialised.

## Provisioners
- Part of resource config - can't be fired off when a resource is altered
- Terraform isn’t able to track the results and status of provisioners in the same way it can for other resources.
- Should be used as last resort
- There are three basic provisioner use cases:
	- Loading data into a virtual machine.
	- Bootstrapping a virtual machine for a config manager.
	- Saving data locally on the system.
- The `remote-exec` provisioner allows connection to a remote machine via Windows Remote Management (WinRM) or Secure Shell (SSH) and runs script remotely.
- `local-exec` will run a script on local machine.

## Workspace
- Each Terraform workspace is meant to represent the deployment of a configuration to one of these separate working environments.
- Each workspace will have persistent data stored in the back-end, most often as a state file, though it could be stored as JSON in a database as well.
- The local file back-end and Amazon Simple Storage Service (Amazon S3) both support workspaces and [etcd](https://etcd.io/) doesn’t.

## State
- The state maintained by Terraform is a JSON document stored locally or on a remote backend.
- `[module path][resource spec]`
	- `[resource spec]` - path to the instance in a given module
	- `module.module_name_label.resource_type.resource_- name_label.resource_attribute[element]`
- 