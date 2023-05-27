# Making Packges for Ubuntu

This short guide is a starting point blueprint. It summarizes others work ([see references](#references)).

<br>
<br>

## Decide on the name of your package. Standard debian notation is all lowercase in the following format:

```
appName_majorVersion.minorVersion
```

For example, you could name your first package...

```
myApp_1.0
```

## Create a directory to make your package in. The name should be the same as the package name.

```
mkdir myApp_1.0
```

Pretend that the packaging directory is actually the root of the file system. Put the files of your program where they would be installed to on a system.

* Note that the file is without the .sh extention

```
mkdir myApp_1.0/usr
mkdir myApp_1.0/usr/local
mkdir myApp_1.0/usr/local/bin
cp "~/ProjectFolder/appFile" myApp_1.0/usr/local/bin
```

## Create a special metadata file with which the package manager will install your program...

```
mkdir myApp_1.0/DEBIAN
gedit myApp_1.0/DEBIAN/control
```

Give the minimum required configurations:

```
Package: myApp
Version: 1.0-1
Section: base
Priority: optional
Architecture: xxx => chose from {i386 / amd64}
Depends: someLibrary (>= 1.2.13), someDependancy (>= 1.2.6)
Maintainer: Your Name <you@email.com>
Description: myApp
 Give other usefull details if needed.
```

For every new line of the description make sure you add one space at the beginning of the line.

Leave blank for no dependancies.

### To check the architecture you can run:

```
dpkg-architecture -q DEB_BUILD_ARCH
```

`i386` -> 32bit

`amd64` -> 64bit

<br>
<br>

## Make the package:

```
dpkg-deb --build myApp_1.0
```

<br>
<br>

# Install:

```
sudo dpkg -i package_file.deb
```

<br>
<br>

# Uninstall:

```
sudo apt-get remove package_name
```

<br>
<br>

# References

This basic manual was created with the help of:

#### [1] curvedinfinity @ https://ubuntuforums.org/showthread.php?t=910717

#### [2] https://help.ubuntu.com/kubuntu/desktopguide/C/manual-install.html
