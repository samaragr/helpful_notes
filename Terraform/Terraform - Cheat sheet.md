
## Block types
#terraform #blocktypes
- Terraform - define global config and behaviour
`terraform{}`
- Provide
`provider "aws" {}`
- Data
`data "aws_vpc" "existing_vpc" {}`
- Resource -
`resource "aws_instance" "example" {}`
- Module
`module "vpc" {}`
- Variable
`variable "instance_count" {}`
- Output
`output "instance_ip" {}`
- Locals
`locals {}`


## Terraform commands
#commands #terraform
https://spacelift.io/blog/terraform-commands-cheat-sheet

### main
- `init` - Prepare your working directory for other commands
- `plan` - Show changes required by the current configuration
- `apply` - Create or update infrastructure
- `destroy` - Destroy previously-created infrastructure
- `validate` - Check whether the configuration is valid

### other
- `console` - Try Terraform expressions at an interactive command prompt
- `fmt [options] [DIR]` - Reformat your configuration in the standard style, scans the current directory for configuration files ending in `tf` and `tfvars`
	- `[options]` 
		- `--list=false` - Don’t list the files containing formatting inconsistencies.
		- `--write=false` - Don’t overwrite the input files (implied by `-check` or STDIN)
		- `--diff` - display formatting differences
		- `--check` - useful in CI/CD pipelines, used to check correct formatting (exit status 0 = correct).
		- `--recursive` - run on parent for subdirectories
	- `[DIR]` - specifies directory 
- `force-unlock` - Release a stuck lock on the current workspace
- `get` - Install or upgrade remote Terraform modules
- `graph` - Generate a Graphviz graph of the steps in an operation
- `import` - bring the existing deployments under Terraform management.
- `login` - Obtain and save credentials for a remote host
- `logout` - Remove locally-stored credentials for a remote host
- `metadata` - Metadata related commands
- `output` - Show output values from your root module
- `providers` - Show the [[Terraform - Cert prep#Providers|providers]] required for this configuration
- `refresh` - Update the state to match remote systems
- `show` - Show the current state or a saved plan
- `state` - [[Terraform - Cert prep#State|Advanced state management]]
	- `list [options] [address...]` - subcommand lists resources in the state.
		- `[options]` 
			- `-state=statefile` - specify a particular state file
			- `-id=ID` - specify a particular id
	- `mv [options] SOURCE DESTINATION` - subcommand moves an item in the state. 
		- `[options]`
			- `-dry-run` flag can be thought of as a what-if. It tells us what it’ll do without making any changes.
			- `-state` flag is the path of the source state file, which needs to be specified if we’re not using the `terraform.tfstate` file or a remote back-end.
			- `-state-out` flag is the path of the destination file. Terraform uses the source state file unless this is specified.
	- `pull [options]` - subcommand pulls the current state and output to `stdout`.
	- `push [options] PATH` - subcommand updates the remote state from a local state file.
		- `PATH` - defines the local path of the file pushed to the remote state
	- `rm [options] ADDRESS` - subcommand removes instances from the state.
	- `show [options] ADDRESS` - subcommand shows a resource in the state.
		- The `ADDRESS` specified by the `show` subcommand must be an instance of a resource and not a grouping of resources created by count or `for_each`.
- `taint` - Mark a resource instance as not fully functional, will destroy and recreate on next `apply`
	- `terraform taint [options] <address>`
		- `<address>` - address of a resource using the same syntax we’d use inside a configuration
- `untaint` - Remove the 'tainted' state from a resource instance
- `version` - Show the current Terraform version
- `workspace` - [[Terraform - Cert prep#Workspace|Workspace]] management (`env` - likely to be deprecated)
	- `new <workspace name>` - command creates a new workspace and selects it. 
	- `select <workspaace name>` - command selects an existing workspace.
	- `list` - command lists the existing workspaces.
	- `show` - command shows the name of the current workspace.
	- `delete <workspace name>` - command deletes an empty workspace. state file must be empty and workspace not currently selected
		- `-force` flag can be specified if the state file isn’t empty, and the resources created by the state file will be abandoned.
- `provisioner` - [[Terraform - Cert prep#Provisioners|provisioners]] used when have scripts or operations to perform locally or on the remote resource
	- `remote-exec` - will run a script on the remote machine through WinRM or SSH
	- `local-exec` - will run a script on local machine.

### Global options (use these before the subcommand, if any):
- `-chdir=DIR` - Switch to a different working directory before executing the given subcommand.
- `-help` - Show this help output, or the help for a specified subcommand. e.g. `terraform commandName -help`
- `-version ` - An alias for the "version" subcommand.


## Environment variables
https://developer.hashicorp.com/terraform/cli/config/environment-variables
- `TF_LOG` - generate detailed logs, output sent to `stderr` (std error output)
	log levels - decreasing verbosity
	- `=trace` - default
	- `=debug`
	- `=info`
	- `=warn`
	- `=error`
	- `=off` - disable
- `TF_LOG_PATH` - write the resulting logs to a specific file location
- `TF_INPUT` - disable prompts for undefined variables. Set to `false` or `=0` same as `-input=false` 
- `TF_VAR_name` - can be used to set variables
- `TF_CLI_ARGS` - specify additional arguments to the command-line. good for CI env. Inserted directly after the subcommand. Affects all terraform commands
	- `TF_CLI_ARGS_name` - Only affects named commands
- `TF_DATA_DIR` - changes the location where Terraform keeps its per-working-directory data
- `TF_WORKSPACE` - selection of workspace. Same as `terraform workspace select your_workspace`
- `TF_IN_AUTOMATION` - 
- `TF_REGISTRY_DISCORVERY_RETRY` - configure the max number of request retries the remote registry client will attempt for client connection errors
- `TF_REGISTRY_CLIENT_TIMEOUT` - default is 10s. Can be configured and increased.
- `TF_CLI_CONFIG_FILE` - 
- `TF_PLUGIN_CACHE_DIR` - an alternative way to set [the `plugin_cache_dir` setting in the CLI configuration](https://developer.hashicorp.com/terraform/cli/config/config-file#provider-plugin-cache).
	- `TF_PLUGIN_CACHE_MAY_BREAK_DEPENDENCY_LOCK_FILE`
- `TF_IGNORE` - `=trace` will output debug messages to display ignored files and folders. Useful for large repos.
