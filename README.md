Winmon
=========

Winmon is a service for Windows that allows you to views basic system statistics on your Android device. 

  - View your system's processor usage
  - View your system's memory usage
  - View your system's storage usage
  - View your system's uptime
  - View your system's external IP address

Winmon doesn't really have an interface because it is designed to be as minimally invasive as possible and as resilient as possible.

In additon to using simply monitoring your system's statistics, it also sends your device push notification when someone logs on/off to your computer or when someone locks/unlocks your computer.

Building
----

Winmon relies on few external libraries which are all listed in the requirements.txt file.

 - psutil
 - uptime
 - requests
 - python-gcm

Once all dependency requirements have been fulfilled, you can begin compiling the code into the executable. Winmon relies
on Py2Exe for bootstrapping it into a Windows executable. You can build the executable by executing:

```
python -OO setup.py py2exe
```

Building the executable should yield a a bunch of DLLs, PYDs, ZIPs and a EXE in the `dist` directory. For packing the files into a MSI, you'll need to the WiX toolchain installed. If you've installed WiX and `candle` and `light` are in your path, execute:

```
candle.exe -nologo installer.wxs -out build\bdist.win32\winmsi\installer.wix -ext WixUIExtension
light.exe -nologo build\bdist.win32\winmsi\installer.wix -pdbout build\bdist.win32\winmsi\installer.pdb -out installer.msi -ext WixUIExtension
```

This will build a MSI that you can distribute.

Installing
----

If you've downloaded the ZIP archive for the source distribution, simply unpack the archive to the location your service  should reside and execute:

```
python service.py install
```

If you've downloaded the ZIP archive for binary distribution, simply unpack the archive to the location your service  should reside and execute:

```
service.exe --startup=auto install
```

The `-startup=auto` option installs the service to startup automatically when the system starts.

If you've downloaded the MSI installed, simply run it and follow the instructions onscreen to install it.

Contributing
----

If you would like to help improve Winmon, or you've found a bug, you can either open an issue or send me a pull-request (if you're feeling adventerous).

License
----

Winmon is licensed under the MIT license. 
Copyright (c) 2014 Mridang Agarwalla

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
