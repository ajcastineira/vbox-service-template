# vbox-service-template

vbox-service-template is an init.d script template for running a VirtualBox machine as a service.

Sending a `stop` command to the service will either save the state of the VM (hibernate) or send the ACPI Power Button signal to the VM and wait for it to self-terminate (powerbutton).

Some more context and howto information can be found here:
http://www.glump.net/howto/virtualbox_as_a_service

## Installation

Make a copy of the script as `/etc/init.d/vbox-NAME` and follow the instructions in the comments in the script. Make sure you set the `x` bit on the file to make it executable.

To mark the service for automatic start at boot time:

* Ubuntu: `update-rc.d vbox-NAME defaults 90` (The '90' is to make sure it starts after the VirtualBox core services.
* Fedora: `chkconfig vbox-NAME on`

To remove the service from the boot process:

* Ubuntu: `update-rc.d -f vbox-NAME remove`
* Fedora: `chkconfig vbox-NAME off`

Additionally, if you are going to shut down your computer while a VM is running you should tell VirtualBox how to handle shutdown. Create or edit `/etc/default/virtualbox`:

    SHUTDOWN_USERS="user1 user2" # space-delimited list of users who might have runnings vms
    SHUTDOWN=savestate # if any are found, suspend them to disk

## Usage

Start

    service vbox-NAME start

Start and wait for the VM to be reachable on the network

    service vbox-NAME start-wait

Stop (hibernate or power button -- see config lines in script)

    service vbox-NAME stop

Restart

    service vbox-NAME restart

Restart and wait for the VM to be reachable on the network

    service vbox-NAME restart-wait

Display status

    service vbox-NAME status
