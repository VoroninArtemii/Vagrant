There is a _Vagrantfile_, used to define and configure three virtual machines with different settings.

### General Configuration:
- `Vagrant.configure("2")`: Specifies the version of the Vagrant configuration.
- `config.ssh.insert_key = false`: Disables automatic insertion of an SSH key for these VMs.

### VM Definitions:

1. **VM1**:
   - **Box**: Uses the `ubuntu/jammy64` base image.
   - **Hostname**: The VM will be named `vm1`.
   - **Network Configuration**:
     - **Forwarded Port**: Forwards port 80 (HTTP) from the guest VM to port 8080 on the host machine.
     - **Private Network**: Assigns a static IP (`172.20.0.10`) on a private network.
   - **Provisioning**: Runs a shell script to:
     - Update and upgrade the system.
     - Install `nginx`.
     - Start and enable `nginx` to run on boot.

2. **VM2**:
   - **Box**: Uses the `ubuntu/jammy64` base image.
   - **Hostname**: The VM will be named `vm2`.
   - **Disk Size**: Sets the disk size to 40GB for this VM.
   - **Network Configuration**: Uses a **public network**, which will allow the VM to get an IP address from the local network and be accessible externally.
   - **Provisioning**: Runs a shell script to:
     - Update and upgrade the system.
     - Install required dependencies for Docker.
     - Add Docker’s official GPG key and repository.
     - Install Docker CE.
     - Start and enable Docker to run on boot.

3. **VM3**:
   - **Box**: Uses the `ubuntu/jammy64` base image.
   - **Hostname**: The VM will be named `vm3`.
   - **Network Configuration**: Assigns a static IP (`172.20.0.11`) on a private network.
   - **Provisioning**: Runs a shell script to:
     - Create a new user `adam` with a home directory and Zsh as the shell.
     - Add the user `adam` to the `sudo` group, allowing them to run commands as root without a password prompt.
