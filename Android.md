
# Android Setup

# wifi setup

[](./assets/image/1.jpg)
[](./assets/image/2.jpg)
[](./assets/image/3.jpg)
[](./assets/image/4.jpg)
[](./assets/image/5.jpg)

- enter the following code
- adb connect IP:PORT
// check this value in setting>Dev>enable wireless debugging> ip address & port

- adb connect ip:port
Port can be identified from settings>Developer mode>enable wireless debugging>ip:port

### other ways

- For initial via usb then wifi
- `adb tcpip 5555`
- disconnect usb
- adb connect ip: port
- adb install further extension for other things adb interface in vs code
