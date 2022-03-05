
# Android Setup

# wifi setup

![](./assets/image/1.jpg=250x250)
![](./assets/image/2.jpg=250x250)
![](./assets/image/3.jpg=250x250)
![](./assets/image/4.jpg=250x250)
![](./assets/image/5.jpg=250x250)

- enter the following code
- adb connect IP:PORT
// check this value in setting>Dev>enable wireless debugging> ip address & port

- adb connect ip:port
Port can be identified from settings>Developer mode>enable wireless debugging>ip:port
- adb devices
// Show devices
- adb disconnect ip:port
//To disconnect Wi-Fi devices

### other ways

- For initial via usb then wifi
- `adb tcpip 5555`
- disconnect usb
- adb connect ip: port
- adb install further extension for other things adb interface in vs code
