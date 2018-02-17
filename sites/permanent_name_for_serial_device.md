# Permanent name for serial device

Solution is already written [here](http://hintshop.ludvig.co.nz/show/persistent-names-usb-serial-devices/),
but it doesn't cover all usecases. If you want to plug multiple dedevices of same type, then you may need to
distinguish which one is which.

## more info about serial device

You can find more info about serial device (or any usb device) by running
```
> udevadm info -an /dev/ttyUSB0
```
<details>
<summary>
Click here to see full ouptut
</summary>

```
Udevadm info starts with the device specified by the devpath and then                                                                                                                                              
walks up the chain of parent devices. It prints for every device                                                                                                                                                   
found, all possible attributes in the udev rules key format.                                                                                                                                                       
A rule to match, can be composed by the attributes of the device                                                                                                                                                   
and the attributes from one single parent device.                                                                                                                                                                  
                                                                                                                                                                                                                   
 looking at device '/devices/pci0000:00/0000:00:14.0/usb1/1-6/1-6:1.0/ttyUSB0/tty/ttyUSB0':                                                                                                                       
    KERNEL=="ttyUSB0"                               
    SUBSYSTEM=="tty"                                
    DRIVER==""                                      
                                                    
 looking at parent device '/devices/pci0000:00/0000:00:14.0/usb1/1-6/1-6:1.0/ttyUSB0':
    KERNELS=="ttyUSB0"                              
    SUBSYSTEMS=="usb-serial"                               
    DRIVERS=="ftdi_sio"                             
    ATTRS{latency_timer}=="16"                      
    ATTRS{port_number}=="0"                         
                                                    
 looking at parent device '/devices/pci0000:00/0000:00:14.0/usb1/1-6/1-6:1.0':
    KERNELS=="1-6:1.0"                              
    SUBSYSTEMS=="usb"                               
    DRIVERS=="ftdi_sio"                             
    ATTRS{authorized}=="1"                          
    ATTRS{bAlternateSetting}==" 0"                            
    ATTRS{bInterfaceClass}=="ff"                    
    ATTRS{bInterfaceNumber}=="00"                   
    ATTRS{bInterfaceProtocol}=="ff"                 
    ATTRS{bInterfaceSubClass}=="ff"                 
    ATTRS{bNumEndpoints}=="02"                      
    ATTRS{interface}=="FT232R USB UART"              <-- info about chip used in serial device 
    ATTRS{supports_autosuspend}=="1"    
    
 looking at parent device '/devices/pci0000:00/0000:00:14.0/usb1/1-6':
    KERNELS=="1-6"                                  
    SUBSYSTEMS=="usb"                               
    DRIVERS=="usb"                                  
    ATTRS{authorized}=="1"                          
    ATTRS{avoid_reset_quirk}=="0"                   
    ATTRS{bConfigurationValue}=="1"
    ATTRS{bDeviceClass}=="00"                                                                            
    ATTRS{bDeviceProtocol}=="00"                    
    ATTRS{bDeviceSubClass}=="00"                    
    ATTRS{bMaxPacketSize0}=="8"                     
    ATTRS{bMaxPower}=="90mA"                        
    ATTRS{bNumConfigurations}=="1"                  
    ATTRS{bNumInterfaces}==" 1"                     
    ATTRS{bcdDevice}=="0600"                        
    ATTRS{bmAttributes}=="a0"                       
    ATTRS{busnum}=="1"                              
    ATTRS{configuration}==""                        
    ATTRS{devnum}=="69"                             
    ATTRS{devpath}=="6"                             
    ATTRS{idProduct}=="6001"                        <-- product id
    ATTRS{idVendor}=="0403"                         <-- vendor id
    ATTRS{ltm_capable}=="no"                        
    ATTRS{manufacturer}=="FTDI"                     
    ATTRS{maxchild}=="0"                            
    ATTRS{product}=="FT232R USB UART"               
    ATTRS{quirks}=="0x0"                            
    ATTRS{removable}=="removable"                   
    ATTRS{serial}=="AI03I296"                       <-- serial number
    ATTRS{speed}=="12"
    ATTRS{urbnum}=="15"
    ATTRS{version}==" 2.00"

 looking at parent device '/devices/pci0000:00/0000:00:14.0/usb1':
    KERNELS=="usb1"
    SUBSYSTEMS=="usb"
    DRIVERS=="usb"
    ATTRS{authorized}=="1"
    ATTRS{authorized_default}=="1"
    ATTRS{avoid_reset_quirk}=="0"
    ATTRS{bConfigurationValue}=="1"
    ATTRS{bDeviceClass}=="09"
    ATTRS{bDeviceProtocol}=="01"
    ATTRS{bDeviceSubClass}=="00"
    ATTRS{bMaxPacketSize0}=="64"
    ATTRS{bMaxPower}=="0mA"
    ATTRS{bNumConfigurations}=="1"
    ATTRS{bNumInterfaces}==" 1"
    ATTRS{bcdDevice}=="0413"
    ATTRS{bmAttributes}=="e0"
    ATTRS{busnum}=="1"
    ATTRS{configuration}==""
    ATTRS{devnum}=="1"
    ATTRS{devpath}=="0"
    ATTRS{idProduct}=="0002"
    ATTRS{idVendor}=="1d6b"
    ATTRS{interface_authorized_default}=="1"
    ATTRS{ltm_capable}=="no"
    ATTRS{manufacturer}=="Linux 4.13.0-32-generic xhci-hcd"
    ATTRS{maxchild}=="12"
    ATTRS{product}=="xHCI Host Controller"
    ATTRS{quirks}=="0x0"
    ATTRS{removable}=="unknown"
    ATTRS{serial}=="0000:00:14.0"
    ATTRS{speed}=="480"
    ATTRS{urbnum}=="2462"
    ATTRS{version}==" 2.00"

 looking at parent device '/devices/pci0000:00/0000:00:14.0':
    KERNELS=="0000:00:14.0"
    SUBSYSTEMS=="pci"
    DRIVERS=="xhci_hcd"
    ATTRS{broken_parity_status}=="0"
    ATTRS{class}=="0x0c0330"
    ATTRS{consistent_dma_mask_bits}=="64"
    ATTRS{d3cold_allowed}=="1"
    ATTRS{device}=="0x9d2f"
    ATTRS{dma_mask_bits}=="64"
    ATTRS{driver_override}=="(null)"
    ATTRS{enable}=="1"
    ATTRS{irq}=="120"
    ATTRS{local_cpulist}=="0-3"
    ATTRS{local_cpus}=="f"
    ATTRS{msi_bus}=="1"
    ATTRS{numa_node}=="-1"
    ATTRS{revision}=="0x21"
    ATTRS{subsystem_device}=="0x5053"
    ATTRS{subsystem_vendor}=="0x17aa"
    ATTRS{vendor}=="0x8086"

 looking at parent device '/devices/pci0000:00':
    KERNELS=="pci0000:00"
    SUBSYSTEMS==""
    DRIVERS==""
```
</details>


Your output may loook different, you you are using some USB hub, then it will be included here (full chain is shown).

If your device has attribute `serial`, then you can write your udev rule like this:

```
SUBSYSTEMS=="usb", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", SYMLINK+="serial_ftdi_$attr{serial}"
```
and have unique name for your device:
```
> ls /dev/serial_ftdi*
/dev/serial_ftdi_AI03I296@
```
Problem starts whem your chip doesn't have serial attribute. 

I was playing around with cheap RS485 -> USB converter:
```
> udevadm info -an /dev/ttyUSB0  
(...) deleted negligible info 
  looking at parent device '/devices/platform/soc/3f980000.usb/usb1/1-1/1-1.2/1-1.2:1.0/ttyUSB0':
    KERNELS=="ttyUSB0"
    SUBSYSTEMS=="usb-serial"
    DRIVERS=="ch341-uart"
    ATTRS{port_number}=="0"
(...)
  looking at parent device '/devices/platform/soc/3f980000.usb/usb1/1-1/1-1.2':
    KERNELS=="1-1.2"
    SUBSYSTEMS=="usb"
    DRIVERS=="usb"
    ATTRS{bDeviceClass}=="ff"
    ATTRS{bmAttributes}=="80"
    ATTRS{bConfigurationValue}=="1"
    ATTRS{version}==" 1.10"
    ATTRS{devnum}=="4"
    ATTRS{bMaxPower}=="96mA"
    ATTRS{idProduct}=="7523"
    ATTRS{avoid_reset_quirk}=="0"
    ATTRS{urbnum}=="13"
    ATTRS{bDeviceSubClass}=="00"
    ATTRS{maxchild}=="0"
    ATTRS{bcdDevice}=="0254"
    ATTRS{bMaxPacketSize0}=="8"
    ATTRS{idVendor}=="1a86"
    ATTRS{product}=="USB2.0-Serial"
    ATTRS{speed}=="12"
    ATTRS{removable}=="removable"
    ATTRS{ltm_capable}=="no"
    ATTRS{bNumConfigurations}=="1"
    ATTRS{busnum}=="1"
    ATTRS{authorized}=="1"
    ATTRS{quirks}=="0x0"
    ATTRS{configuration}==""
    ATTRS{devpath}=="1.2"
    ATTRS{bDeviceProtocol}=="00"
    ATTRS{bNumInterfaces}==" 1"
(...)
```
No `serial` here, so above udev rule won't work.
One can see that it uses [`ch341` chip](https://www.google.pl/search?&q=ch341+datasheet)

I plugged two converters to raspberry pi and run:
```
udevadm info -an /dev/ttyUSB0 >> rs1.txt
udevadm info -an /dev/ttyUSB1 >> rs2.txt
```
and diffed output:
```
diff rs1.txt rs2.txt
8,9c8,9
<   looking at device '/devices/platform/soc/3f980000.usb/usb1/1-1/1-1.5/1-1.5:1.0/ttyUSB0/tty/ttyUSB0':
<     KERNEL=="ttyUSB0"
---
>   looking at device '/devices/platform/soc/3f980000.usb/usb1/1-1/1-1.2/1-1.2:1.0/ttyUSB1/tty/ttyUSB1':
>     KERNEL=="ttyUSB1"
13,14c13,14
<   looking at parent device '/devices/platform/soc/3f980000.usb/usb1/1-1/1-1.5/1-1.5:1.0/ttyUSB0':
<     KERNELS=="ttyUSB0"
---
>   looking at parent device '/devices/platform/soc/3f980000.usb/usb1/1-1/1-1.2/1-1.2:1.0/ttyUSB1':
>     KERNELS=="ttyUSB1"
19,20c19,20
<   looking at parent device '/devices/platform/soc/3f980000.usb/usb1/1-1/1-1.5/1-1.5:1.0':
<     KERNELS=="1-1.5:1.0"
---
>   looking at parent device '/devices/platform/soc/3f980000.usb/usb1/1-1/1-1.2/1-1.2:1.0':
>     KERNELS=="1-1.2:1.0"
32,33c32,33
<   looking at parent device '/devices/platform/soc/3f980000.usb/usb1/1-1/1-1.5':
<     KERNELS=="1-1.5"
---
>   looking at parent device '/devices/platform/soc/3f980000.usb/usb1/1-1/1-1.2':
>     KERNELS=="1-1.2"
40c40
<     ATTRS{devnum}=="5"
---
>     ATTRS{devnum}=="6"
59c59
<     ATTRS{devpath}=="1.5"
---
>     ATTRS{devpath}=="1.2"
132c132
<     ATTRS{wr_reg_test}=="Time to write GNPTXFSIZ reg 10000000 times: 400 msecs (40 jiffies)"
---
>     ATTRS{wr_reg_test}=="Time to write GNPTXFSIZ reg 10000000 times: 700 msecs (70 jiffies)"
```

They only usable difference between those ouptus is `KERNELS` and attribute `devpath` which corresponds to physical USB ports.
So that it would be possible to write udev rule which composes name which corresponds to physical port. 

I will update this post after making tests. 
