## Instructions
`FROM <image>` - specify base image
`RUN <args>` - execute specified command
`ENTRYPOINT` -specify the command to execute the container
`COPY <path>` - specify files/directories to copy from host to container
	`ADD <src>` - `COPY` + unzip
`USER <name>` - specify username 
`EXPOSE` - specify port to expose
`WORKDIR <path>` - change current directory
`CMD <args>` - Specify the command at the time of container execution (can be overwritten)
`ENV <NAME> <value>` - add environment variables 
`LABEL <label>` - add a label

