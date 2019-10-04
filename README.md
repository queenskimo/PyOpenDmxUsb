
# PyOpenDmxUsb

PODU is an API for the [Enttec OPEN DMX USB](https://www.enttec.co.uk/en/product/controls/dmx-usb-interfaces/open-dmx-usb/) on **Windows** that lets your python programm easily controll any DMX device connected to it. It is build in two parts, a server and a client.
The Server is written in C# and connects to the USB interface to control the DMX devices. It is controlled by a python module over a named pipe.

## Getting Started
The easiest way to use PODU is to run the DMXServer with the following command:
```
DMXServer -n PODU
```
this will start the DMXServer and attach it to a named pipe called 'PODU'.

In Python use DMXClient like in the following example:
```py
from DMXClient import DMXClient

dmxClient = DMXClient("PODU")
dmxClient.connect()
dmxClient.write([16, 255, 17, 125])
dmxClient.write("DMX 18 90 19 40")
dmxClient.write({20:'30', '21': 243})

dmxClient.close()
```
As you can see, there are many different formats you can choose from.

## Usage

After getting an FMF object the following functions can be called:

#### Connect to server

```py
dmxClient.connect()
```
This will block until connected to the DMXServer

#### Set DMX values

```py
dmxClient.write(str)
dmxClient.write(list)
dmxClient.write(dict)
```

These will send command to the server setting the designated channels to the specified values

###### Faster method

As commands to the server are send as string you may also use the following method to get a tiny performance boost:
```py
dmxClient._write(str)
```

#### Close connection to the server
```py
dmxClient.close()
```

This will close the connection to the DMXServer

## DMXServer Usage
```
Usage: DMXServer [OPTIONS]
DMXServer is the part of PODU that interfaces with the OPEN DMX USB.

Options:
  -h     Show this screen.
  -n     Name of named pipe (must be same as used by DMXClient).
  -v     Show verbose output.
  -s     Wait for another connection after a DMXClient disconnects.
```

## Installation
### Binarys
In order to use PODU you need the DMXClient(Python) and the DMXServer(C#), both of which can be downloaded on the [release](https://github.com/Coronon/PyOpenDmxUsb/releases) tab.
### Sources
You can also compile the DMXServer from source, it is located under 'C#/DMXServer.cs'.

## License

GNU General Public License v3.0