# vbox-service-template

vbox-service-template is a template init.d script for running a VirtualBox machine as a service.

## Installation

Make a copy of the script as `/etc/init.d/vbox-NAME` and follow the instructions in the comments in the script.

To mark the service for automatic start at boot time:

* Ubuntu: `update-rc.d vbox-NAME defaults`
* Fedora: `chkconfig vbox-NAME on`

To remove the service from the boot process:

* Ubuntu: `update-rc.d vbox-NAME purge`
* Fedora: `chkconfig vbox-NAME off`

Additionally, if you are going to shut down your computer while a VM is running you should tell VirtualBox how to handle shutdown. Create or edit `/etc/default/virtualbox`:

    SHUTDOWN_USERS="user1 user2" # space-delimited list of users who might have runnings vms
    SHUTDOWN=savestate # if any are found, suspend them to disk

## Usage

    service vbox-NAME start
    service vbox-NAME start-wait # Start and wait for the VM to be pingable
    service vbox-NAME stop
    service vbox-NAME restart
    service vbox-NAME restart-wait # Restart and wait for the VM to be pingable
    service vbox-NAME status
