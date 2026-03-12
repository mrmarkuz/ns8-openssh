# ns8-openssh

[OpenSSH](https://www.openssh.org/) is the premier connectivity tool for remote login with the SSH protocol.

## Install

Install via Software center:

  - Add a Software repository pointing to `https://repo.mrmarkuz.com/ns8/updates/`, check out the [repo webpage](https://repo.mrmarkuz.com) how to do it
  - Install OpenSSH via Software Center

Or instantiate the module with:

    add-module ghcr.io/nethserver/openssh:latest 1

The output of the command will return the instance name.
Output example:

    {"module_id": "openssh1", "image_name": "openssh", "image_url": "ghcr.io/nethserver/openssh:latest"}

## Configure

Let's assume that the openssh instance is named `openssh1`.

Launch `configure-module`, by setting the following parameters:
- `password_access`: Allow password access
- `user`: Username
- `password`: Password used when password access is allowed
- `sudo_access`: Allow sudo for the SSH user which is needed to execute for example `ping` inside the container, i.e. `sudo ping example.com`

Example:

    api-cli run module/openssh1/configure-module --data '{"password_access": true, "user": "username", "password": "secret123", "sudo_access": false}'

The above command will:
- start and configure the openssh instance

## Usage

The used SSH port to connect to the OpenSSH container can be found on the app settings page.

    ssh -p <port> user@example.com

When connected it's possible to connect to the NS8 host using the IP 10.0.0.1:

    ssh user@10.0.0.1

## Firewall

It's possible to close the port to the original host system SSH service:

    firewall-cmd --permanent --service=ssh --remove-port=22/tcp
    firewall-cmd --reload
