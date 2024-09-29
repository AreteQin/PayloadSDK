# PayloadSDK

# DJI M30T

## Development
```bash
sudo vim /etc/rc.local
```
Uncomment the following line:
```bash
echo 424 > /sys/class/gpio/export
echo out > /sys/class/gpio/gpio424/direction
echo 1 > /sys/class/gpio/gpio424/value
echo 264 > /sys/class/gpio/export
echo out > /sys/class/gpio/gpio264/direction
echo 1 > /sys/class/gpio/gpio264/value
sleep 1
```
Comment the following line:
```bash
sleep 25
#cd /home/nvidia/icreast/build
#./bin/dji_sdk_demo_linux_cxx &
```

Set the port name in:
```bash
vim ~/Payload-SDK/samples/sample_c++/platform/linux/manifold2/hal/hal_uart.h
```
```cpp
/* Exported constants --------------------------------------------------------*/
//User can config dev based on there environmental conditions
#define LINUX_UART_DEV1    "/dev/ttyTHS1"
#define LINUX_UART_DEV2    "/dev/ttyTHS1"
```

Set hardware connection in file:
```bash
vim ~/Payload-SDK/samples/sample_c++/platform/linux/manifold2/application/dji_sdk_config.h
```
```C++
/* Exported constants --------------------------------------------------------*/
#define DJI_USE_ONLY_UART                  (0)
#define DJI_USE_UART_AND_USB_BULK_DEVICE   (1)
#define DJI_USE_UART_AND_NETWORK_DEVICE    (2)

/*!< Attention: Select your hardware connection mode here.
* */
#define CONFIG_HARDWARE_CONNECTION         DJI_USE_UART_AND_NETWORK_DEVICE
```

Set your DJI enterprise account in file:
```bash
vim ~/Payload-SDK/samples/sample_c++/platform/linux/manifold2/application/dji_sdk_app_info.h
```
```C++
/* Exported constants --------------------------------------------------------*/
// ATTENTION: User must goto https://developer.dji.com/user/apps/#all to create your own dji sdk application, get dji sdk application
// information then fill in the application information here.
#define USER_APP_NAME               ""
#define USER_APP_ID                 ""
#define USER_APP_KEY                ""
#define USER_APP_LICENSE            ""
#define USER_DEVELOPER_ACCOUNT      ""
#define USER_BAUD_RATE              "460800"
```

Finally, build the project:
```bash
mkdir build && cd build
cmake ..
make -j4
sudo ./bin/dji_sdk_demo_linux_cxx
```