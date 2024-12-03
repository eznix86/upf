
# Uncomplicated Port Forwarder (UPF)

Uncomplicated Port Forwarder (UPF) is a simple command-line tool to manage port forwarding rules using `iptables`. It supports both TCP and UDP protocols, making it easy to set up port forwarding for specific ports or ranges of ports.


## Installation

```bash
pip install upf
```
Run the script with `sudo` for administrative privileges (required to modify `iptables`).

## Usage

### Add a Single Port Forwarding Rule

Add a port forwarding rule from a host to a remote IP and port.

#### TCP (default)
```bash
sudo upf add <remote-ip> <host-port>:<remote-port>
```

Example:
```bash
sudo upf add 192.168.0.2 2200:22
```

#### UDP
```bash
sudo upf add <remote-ip> <host-port>:<remote-port> --udp
```

Example:
```bash
sudo upf add 192.168.0.2 2200:22 --udp
```

### Add a Range of Port Forwarding Rules

Add a range of port forwarding rules for a subnet starting from a specified port.

#### TCP (default)
```bash
sudo upf add-range <gateway>/<subnet> <starting-port>
```

Example:
```bash
sudo upf add-range 192.168.0.1/24 2200
```

#### UDP
```bash
sudo upf add-range <gateway>/<subnet> <starting-port> --udp
```

Example:
```bash
sudo upf add-range 192.168.0.1/24 2200 --udp
```

### List All Managed Port Forwarding Rules

List all the port forwarding rules that have been added using UPF.

```bash
sudo upf list
```

### Delete a Specific Port Forwarding Rule

Delete a specific port forwarding rule by host port.

#### TCP (default)
```bash
sudo upf delete <host-port>
```

Example:
```bash
sudo upf delete 2200
```

#### UDP
```bash
sudo upf delete <host-port> --udp
```

Example:
```bash
sudo upf delete 2200 --udp
```

## Notes

- **Persistence:** By default, changes made using `iptables` are not persistent after reboot. To make them persistent, you can save the rules using `iptables-save` and restore them with `iptables-restore`.