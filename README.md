# connective-shit

A replacement for the Connective Plugin which is used on several websites to log in or sign documents using a card reader and an electronic identity card. There is only official support for Windows and Mac, so this application is primarily focused on Linux support. The acronym shit stands for SHady Identity Transmission.

## Limitations

This application is only tested with a [VASCO Digipass 870](https://www.onespan.com/products/card-readers/digipass-870). It may work for other card readers with a keypad, but card readers without keypad are not supported. Adding this is trivial though, once you have the right hardware. Look at the TODO comments in the code to find out more if you'd like to contribute.

There is also one security feature which is not implemented, because the algorithm is unknown. Whether this [security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity) feature is really improving the security or not is up for debate, but you should be aware that using this application you may send your personal data to anyone on the internet.

## Alternative

You can find an alternative solution in the client-server directory. With this solution the browser plugin is installed in Linux, but all commands to the backend are sent over the network to a Windows machine where you should connect the card reader.

There are obvious disadvantages with this solution. First of all your identity is transferred unencrypted over the network, which may be visible by anyone, but apart from that you will have to walk from one computer to another while logging in.
The advantage is that all security features and all hardware is supported, since the official backend is used. It was implemented with the intention to run the backend under [wine](https://www.winehq.org/), but wine has incomplete support for smartcards.

You may still opt to use this solution if you can run Windows in a virtual machine. See the README.md file in the client-server directory for installation instructions.

## Requirements

The backend runs under Python. To communicate with the card reader the [pyscard](https://github.com/LudovicRousseau/pyscard) module is used. Installing the backend also requires the [nativemessaging](https://github.com/Rayquaza01/nativemessaging) module, but this is not mandatory to run the code. If you know how to install the manifest for native messaging applications you can skip this requirement.

## Installation

### Obtaining the plugin

Trying to install the Connective browser package under Linux results in a message `This operating system is not supported`. You are not even able to download anything.
To obtain the necessary files run the `get_connective_plugin.py` script included in this repository. A subdirectory `connective-downloads` will be created, containing the installer for both the browser plugin and the windows native application. The native application is only required for the client-server alternative solution.

### Installing the browser plugin

This should be straightforward. Go to the `connective-downloads` directory created in the previous step and open `connective_signing_extension-1.0.4.xpi` in your web browser and follow the installation instructions.

### Installing the backend

This script will be started by your browser whenever the Connective Browser Plugin receives the command to do so and provides the functionality to use the card reader.

Install nativemessaging using `pip install nativemessaging` and run `nativemessaging-install.py firefox` or `nativemessaging-install.py chrome` depending on your browser. For other browsers you have to investigate where to install `native-manifest.json`.

Note that the full path to the backend is saved in your browser's native messaging configuration. This means that if you want to move the backend to another location after installation you are also required to re-run `nativemessaging-install.py` with the appropriate parameter.
