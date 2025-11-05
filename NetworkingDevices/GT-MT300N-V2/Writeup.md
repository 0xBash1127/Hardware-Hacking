## Exploit: UART -> Root via Failsafe mode

## Tools used

- Putty
- USB to TTL UART Converter

## Identifying the serial interface

- Looking at the top of the PCB, we can see three header pins. Just off to the bottom right of the pins, their purpose is conveniently labeled `GRD`, `RX0`, `TX0`, and `VCC`. We can safely assume this will be the serial interface we need to connect to.
	- ![PCB Image](./GT-MT300N-V2/.hidden_images/PCB.jpg)

## Setting up our Putty session
- From researching the device, we learn that the baud rate is `115200`. Let's use this information to set up a Putty session
  - ![Putty Sesion](./GT-MT300N-V2/.hidden_images/Putty_Session)


## Booting into FAILSAFE mode

- Examining the device during bootup, we can see that there is an option to put the device into failsafe mode by pressing `f` and then hitting `enter`
	- ![Failsafe Mode](./GT-MT300N-V2/.hidden_images/failSafeMode.png)

## FAILSAFE menu

- From the menu, we can see that after we execute the `mount_root` command, we're able to interact with the `/etc/config` files, and we can change root's password with `passwd`
- We will skip investigating the config files for now and change root's passwords so we can access the device.
	- ![BusyBox failsafe console](./GT-MT300N-V2/.hidden_images/BusyBox_v1.35.0.png)


## Changing root password

- We first mount the root file system with `mount_root`. Next, we change the root password with `passwd root`.
	- ![Passwd_root](./GT-MT300N-V2/.hidden_images/Passwd_Root.png)

## Logging in as root

- Finally, we login and verify that we are actually root with `id`
	- ![Root login](./GT-MT300N-V2/.hidden_images/RootLoginProof.png)