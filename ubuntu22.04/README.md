# Using the b-plus MDILink Wireshark Dissector

This guide provides instructions on how to install and use the b-plus MDILink Wireshark Dissector developed for the BPLMeas/DAQ protocol.

---

## Prerequisites

Before using the dissector, ensure you have:

- Wireshark version 4.5
- The custom dissector binary (`.so`)

---

## Installation

### 1. Build Wireshark
Build wireshark easily by running the script: wireshark_build.sh

You can find the script here: https://gist.github.com/syneart/2d30c075c140624b1e150c8ea318a978
```bash
rsaad@rsaad:~$ sudo chmod +x wireshark_build.sh
rsaad@rsaad:~$ ./wireshark_build.sh
```

### 2. Place the bplus plugin
Place bplus.so into Wireshark's plugin directory: `wireshark/build/run/plugins/4.5/epan`

### 3. Run Wireshark
Run wireshark with the following command

```bash
rsaad@rsaad:~$ wireshark/build/run/wireshark
```
### 4. Protocol add in Decoding
After opening Wireshark successfully, you need to press on Analyze→ Decode as...

![](docs/analyze_decode_as.png)

Add the following parameters:

![](docs/decoding_parameters.png)

Afterwards you will be able to see such

![](docs/wireshark.png)

### 5. Features

#### 1. DAQ CSI-2 
Here you will be able to see:

![](docs/csi2.png)

and at the end

![](docs/csi2_end.png)

#### 2. DAQ JSON
Wireshark decode that alone, these are the json information given by the MDILink, like sensor config...

![](docs/json.png)

#### 3. DAQ I2C Sniffer
Here you will see all the I2C Communication

![](docs/i2c.png)

## TShark
It is possible to use the I2C Sniffer in TShark to extract all the I2C messages and export it in a .txt file or so, this is very helpful for debugging and building MDILink Configurations

- First open Terminal
- run the following command: 

`wireshark/build/run/tshark -G protocols | grep -i i2c ` 

to make sure that the protocol is correctly recognized by TShark
- Afterwards run the following command: 

`wireshark/build/run/tshark -r Downloads/test.pcapng -V | grep "I2C Sniffer: Message Payload" > i2c_messages.txt`

this command will extract the i2c messages from the pcapng and export them to a .txt file

So the whole Procedure will look like this:

![](docs/TShark.png)

Make sure that you saved the decoding as parameters in wireshark before!!!
