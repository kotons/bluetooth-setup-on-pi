# Bluetooth setup for Raspberry pi

Use these to  install and setup the bluetooth for serial use and communication using bluetooth
## Setting Up Bluetooth Serial Port Profile on Raspberry Pi using sdptool
### Enable SPP on Raspberry Pi

1. Open Bluetooth service configuration file.

```bash 
 sudo nano /etc/systemd/system/dbus-org.bluez.service 
```
2. Look for a line that starts with “ExecStart” and add compatibility flag ‘-C’ at the end of the line.
```
ExecStart=/usr/lib/bluetooth/bluetoothd -C
```
3. Add a line below immediately after “ExecStart” line, then save and close the file.
```
ExecStartPost=/usr/bin/sdptool add SP
```
4.  Reload the configuration file.

``` 
sudo systemctl daemon-reload
```
5. Restart the service.
```
sudo systemctl restart bluetooth.service
```

## Run the bluetooth to communicate 
1. Launch the Bluetooth control
```bash
bluetoothctl
```
2. Make discoverable Rpi bluetooth
```
discoverable on
```
## Testing
1. Listen for incoming connection on Raspberry Pi.
```
sudo rfcomm watch hci0
```
1. Install and launch “Serial Bluetooth Terminal”  on the phone.
2. In the app, go to the “Device” menu and select Raspberry Pi. If everything goes well and the connection is established, you should be able to see like this:
```bash 
$ sudo rfcomm watch hci0
Waiting for connection on channel 1
Connection from XX:XX:XX:XX:XX:XX to /dev/rfcomm0
Press CTRL-C for hangup
```



## Reference link for above setup
[Raspberry pi Bluetooth serial setup](https://scribles.net/setting-up-bluetooth-serial-port-profile-on-raspberry-pi/)
