# Instructions 

1. Set your DHCP server's client options to point to this Dockerhost's IP for FTFP server and specify bootfile `rancheros.pxe`.

2. Modify the following files and the corresponding values for your specification. 

File | Value | Notes
--- | ---  | ---
`./ipxe/netboot/rancheros.pxe` | `${host-ip}` | Update this placeholder value to the IP of this host that his hosting the `config-drive` service.
`./ipxe/netboot/rancheros.pxe` | `{cloud-init-file}` | Update this placeholder value to the name of your desired cloud-init file for Rancher OS. This filename should match the same file hosted by config-drive : `./config-drive/configs/<cloud-init.yaml>` 
`./config-drive/configs/<cloud-init.yaml>` | Cloud-init file values | Refer to [RancherOS documentation](http://rancher.com/docs/os/v1.1/en/configuration/) to construct your cloud-init file. 
**[Optional]** `./docker-compose.yaml` | uncomment volume mount reference ~ line 11 | Update placeholder **/you/data/directory** to a volume to where you will store your cloud-init files.

3. In this repository's directory, execute `docker-compose up -d` to start the stack. 