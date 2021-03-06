# Go FTP Secure server with support for local file system and Microsoft Azure Blob storage

[![License](https://img.shields.io/github/license/mashape/apistatus.svg)](https://img.shields.io/github/license/mashape/apistatus.svg) 
[![Release](https://img.shields.io/github/release/MindFlavor/ftpserver2.svg)](https://img.shields.io/github/release/MindFlavor/ftpserver2.svg) [![Build Status](https://drone.io/github.com/MindFlavor/ftpserver2/status.png)](https://drone.io/github.com/MindFlavor/ftpserver2/latest) [![Commits since](https://img.shields.io/github/commits-since/MindFlavor/ftpserver2/v1.1.svg)](https://img.shields.io/github/commits-since/MindFlavor/ftpserver2/v1.1.svg) [![Coverage Status](https://coveralls.io/repos/MindFlavor/ftpserver2/badge.svg?branch=master&service=github)](https://coveralls.io/github/MindFlavor/ftpserver2?branch=master) 


### A pure go FTP Secure server with support for local file system and [Microsoft Azure Blob storage](https://azure.microsoft.com/en-us/documentation/services/storage/).


The interface based file system makes easy to support different file systems. Please tell me if you are interested in something not covered here.

## Features
This server implements most - not all - the FTP commands available. This should be enough for most *passive* clients, below you will find a tested program list.

The main features are:
* Local file system support (ie standard FTP)
* Azure blob storage backed file system
* Unsecure (plain) FTP
* FTP Secure explicit
* FTP Secure implicit
* File system agnostic
* Azure nested directory support (thanks to [Shuichiro MAKIGAKI](https://github.com/shuichiro-makigaki))
* Pluggable logging system (thanks to [logrus](https://github.com/sirupsen/logrus))

### Implemented commands

Command | Since version 
--- | ----
USER | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
PASS | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
PWD  | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
TYPE | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
PASV | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
EPSV | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
LIST | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
SYST | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
CWD  | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
CDUP | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
SIZE | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
RETR | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
STOR | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
DELE | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
FEAT | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
QUIT | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
NOOP | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
MKD  | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
RMD  | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
REST | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
AUTH | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
PROT | [1.0](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.0)
NLST | [1.1](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.1)
LIST nested | [1.1](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.1)
CWD nested  | [1.1](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.1)
MKD nested  | [1.1](https://github.com/MindFlavor/ftpserver2/releases/tag/v1.1)



This list may not be updated: please refer to [session.go](https://github.com/MindFlavor/ftpserver2/blob/master/ftp/session/session.go) source file to the updated list.


## How to build
The main FTP server object can be called on its own in your project. Here, however, I give you a very simple program to test it. In order to use it download it, compile it and launch it. Here we suppose you have installed [GO](https://golang.org/) on your build machine and have the ```GOPATH``` environment variable set.

### Download

With this command you can download the code with all its references. You can also use it later to update to the latest source code:

```
go get -u github.com/mindflavor/ftpserver2
```

### Build

To build the application use this code. The binary will be saved in the ```%GOPATH\bin``` folder (```$GOPATH``` in linux):

```
go install github.com/mindflavor/ftpserver2
```

### Use
Here we assume you have a folder called ```ftphome``` in your ```C:\``` disk. Substitute it with your FTP home folder.

#### Windows
```
%GOPATH%\bin\ftpserver2 -lfs C:\ftphome
```

#### Linux
Here we assume you have a folder called ```/mnt/ftphome``` on your file system. Substitute it with your FTP home folder.

```
sudo $GOPATH%/bin/ftpserver2 -lfs /mnt/ftphome
```

You need to be *su* in order to listen on port 21 (standard FTP command port). If you use another port you can start the program without *sudo*. Check the parameters section for how to do it.

## Azure blob storage
In order to have the FTP server serve the azure storage blobs simply replace the ```-lfs``` parameter with ```-ak``` and ```-an``` like this:

```
$GOPATH/bin/ftpserver2 -ak <mystorageaccount> -as <shared_key_primary_or_secondary>
```

More info on the parameters in the Parameters section.

## Some screenshots

This is an example of execution in ubuntu:

![](http://i.imgur.com/NDupZcK.jpg)

As you can see here, TLS is available (it's up to you to use valid certs however):

![](http://i.imgur.com/Iv7d85S.jpg)

Here is how an Azure storage account appears in Chrome:

![](http://i.imgur.com/2cWdtM1.jpg)

## Parameters
At any time you can call the executable with ```-help``` flag in order to be reminded of the parameters.

|Flag|Type|Description|Default|
|---|---|---|---|
|```an```| string |        Azure blob storage account name (*1*)|```nil```|
|```ak```|string|Azure blob storage account key (either primary or secondary) (*1*)|```nil```|
|```crt```| string|        TLS certificate file (*2*)|```nil```|
|```key```| string|        TLS certificate key file (*2*)|```nil```|
|```lDebug```| string|        Debug level log file|```nil```|
|```lError```| string|        Error level log file|```nil```|
|```lInfo```| string|        Info level log file|```nil```|
|```lWarn```| string|        Warn level log file|```nil```|
|```lfs```| string|        Local file system root (*3*)|```nil```|
|```ll```| string|        Minimum log level. Available values are ```Debug```, ```Info```, ```Warn```, ```Error``` |```Info```
|```maxPasvPort```| int|        Higher passive port range |50100
|```minPasvPort```| int|        Lower passive port range |50000
|```plainPort```| int|        Plain FTP port (unencrypted). If you specify a TLS certificate and key encryption you can pass -1 to start a SFTP implicit server only |21
|```tlsPort```| int|        Encrypted FTP port. If you do not specify a TLS certificate this port is ignored. If you specify -1 the implicit SFTP is disabled |990

#### Notes

1.These two flags must be specified together. If you need to retrieve the storage account key look here [http://stackoverflow.com/questions/6985921/where-can-i-find-my-azure-account-name-and-account-key](http://stackoverflow.com/questions/6985921/where-can-i-find-my-azure-account-name-and-account-key). You cannot both specify this flags and the local file system one (```lfs```).

2.These two flags must be specified together. Without either one the secure extensions of FTP will be disabled. This article ([http://stackoverflow.com/questions/12871565/how-to-create-pem-files-for-https-web-server](http://stackoverflow.com/questions/12871565/how-to-create-pem-files-for-https-web-server)) explains how to generate both the certificate file and the key one.

3.You cannot both specify this flag and the azure storage ones (```an``` and ```ak```).

## ToDo

* Better tests. Coverage is abysmal. Script unit testing for a distributed state machine such as FTP is a PITA though.
* File access privilege check (right now is ignored).
* Authentication. Right now the FTPServer delegates authentication to the caller but the provided executable does not validate the passed identity.

## Tested clients  

#### PC
* [FileZilla](https://filezilla-project.org/).
* [Chome](https://www.google.com/chrome/browser/desktop/).
* [Firefox](https://www.mozilla.org/en-US/firefox/new/#).
* [Internet Explorer](http://windows.microsoft.com/en-us/internet-explorer/download-ie).

#### Android
* [ES File Explorer File Manager](https://play.google.com/store/apps/details?id=com.estrongs.android.pop)
* [Turbo FTP client & SFTP client](https://play.google.com/store/apps/details?id=turbo.client)
* [FTP Client](https://play.google.com/store/apps/details?id=my.mobi.android.apps4u.ftpclient)

### License
Please refer here: [LICENSE](https://github.com/MindFlavor/ftpserver2/blob/master/LICENSE).

## Contributing
If you want to contribute please do so, just fork and ask for merge. 
An huge *thank you* to everyone contributing (please see here the [GitHub contributors page](https://github.com/MindFlavor/ftpserver2/graphs/contributors) for their names).
