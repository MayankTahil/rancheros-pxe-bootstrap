# Pre-requisites 

Have a quick read through [Rancher's documentation on bare-metal booting](http://rancher.com/docs/os/v1.1/en/running-rancheros/server/pxe/) with iPXE for context and background information. 

With this repository, you only have to create your [`boot.cfg`](./ipxe/example/installer.pxe) and [cloud-init file](./config-drive/configs/rancher-cloud-init-example.yaml) and mount it to respective volumes in the [docker-compose.yaml](./docker-compose.yaml) file. Start the stack and update your DHCP server to point to the boot filename and TFTP server. 

# Instructions 

1. Set your DHCP server's client options to point to this Dockerhost's IP for FTFP server and specify bootfile `rancheros.pxe`.

2. Modify the following files and the corresponding values for your specification. 

File | Value | Notes
--- | ---  | ---
`./ipxe/example/installer.pxe` | `${cloud-config.lab}` | Update this placeholder value to the IP of this host that his hosting the `config-drive` service.
`./ipxe/example/installer.pxe` | `{cloud-init-file.yaml}` | Update this placeholder value to the name of your desired cloud-init file for Rancher OS. This filename should match the same file hosted by config-drive : `./config-drive/configs/<cloud-init.yaml>` 
`./config-drive/configs/<cloud-init.yaml>` | Cloud-init file values | Refer to [RancherOS documentation](http://rancher.com/docs/os/v1.1/en/configuration/) to construct your cloud-init file. 
`./docker-compose.yaml` | update volume mount reference ~ line 11 and ~ line 22 | Update placeholder **{/your/boot-cfg/data}** and {/your/cloud-init/data} to a volume where you will store your cloud-init and boot config files.

3. In this repository's directory, execute `docker-compose up -d` to start the stack. 