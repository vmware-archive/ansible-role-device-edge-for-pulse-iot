# VMware has ended active development of this project, this repository will no longer be updated.

# ansible-role-device-edge-for-pulse-iot

The purpose of this repository is to automate the installation of the Pulse agent into
device edge(s) and enroll the device edge(s) into Pulse IoT Center 2.0.

***Note**: In Pulse IoT Center, device edges are called gateways.

## Getting Started

Clone this repository into the machine you wish to use to run the Ansible playbook.
Make sure the machine has SSH access to the device edge(s).

### Prerequisites

The following needs to be installed on the Ansible control machine:

* Ansible 2.7

The following needs to be installed on the device edge(s):

* SSH daemon with remote access enabled
* Python 2.7 or greater

Also, be sure you have access to a Pulse 2.0 instance and are authorized to enroll new devices.

### Configuration

Once you have the repository cloned into the machine you are going to use as the
Ansible controller, then you must modify a few of the files to make the playbook
work for your setup. The following are the list of steps to follow:

1. Make a copy of the `group_vars/device-edges.sample` file to the same folder but name it `device-edges`. Be sure to update the variable values that are marked `EDIT_ME` with the correct values for your setup.
2. (Optional) Make one or more copies of the `host_vars/device_edge01.sample` file to the same folder. You can choose any name you wish for the file(s) but they must not contain special characters. Each file corresponds to a device edge. Be sure to update the variable values that are marked `EDIT_ME` with the correct values for your setup. This step can be skipped if you are using the same Pulse template for all your device edges.
3. Make a copy of the `hosts.sample` file to the same folder but name it `hosts`. Be sure to update the file based on the number of device edges that you wish to enroll and fill in the IP addresses corresponding to each device edge. A sample of the format to use to list out the device edges is included in the sample file. (Optional) In case you completed step 2, the name you give to each device edge must match one of the files you created in the `host_vars` folder. For example, if you have a file `host_vars/mydevice`, then in your `hosts` file you should have an entry like this `mydevice ansible_host=127.0.0.1`.
4. Update the variable `remote_user` in the `site.yml` file with the name of a user that has SSH access to the device edge(s).

## Running the Playbook

To execute the playbook, run the following command from the root directory:

```bash
 sudo ansible-playbook -i hosts site.yml --ask-pass --ask-become-pass
```

The playbook may ask you for the sudo password of your Ansible controller. 
The playbook will ask you for the password that belongs to the `remote_user` 
account you specified and the sudo password for the device edge(s) if it 
is different than the one for the `remote_user`. If your SSH password for the 
`remote_user` is the same as the sudo password for the device edge, then 
you can just press enter when it asks you for it.

Once the playbook finishes executing, you can verify the results by login into 
the Pulse 2.0 UI and checking that the device edge(s) are listed under 
`inventory -> devices`. The name of each devices in Pulse will be a combination 
of the name you specified in the `hosts` file and the MAC address of the device edge.

## Contributing

The ansible-role-device-edge-for-pulse-iot project team welcomes contributions from the community. Before you start working with ansible-role-device-edge-for-pulse-iot, please
read our [Developer Certificate of Origin](https://cla.vmware.com/dco). All contributions to this repository must be
signed as described on that page. Your signature certifies that you wrote the patch or have the right to pass it on
as an open-source patch. For more detailed information, refer to [CONTRIBUTING.md](CONTRIBUTING.md).

## Authors

* **Luis M. Valerio** - *Initial work* - [ansible-role-device-edge-for-pulse-iot](https://github.com/vmware/ansible-role-device-edge-for-pulse-iot)

## License

This project is licensed under the BSD 2-Clause License - see the [LICENSE.txt](LICENSE.txt) file for details
