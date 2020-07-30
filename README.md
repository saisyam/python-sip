# Build SIP applications using PJSIP Python3 bindings
Implement SIP clients/servers using [PJSIP Library](http://www.pjsip.org) Python3 bindings

# Installing PJSIP on Ubuntu 18.04
You can download the latest version of PJSIP from [here](https://www.pjsip.org/download.htm). Current version as of this update is 2.10. Download the `tar.gz` file. Follow the below commands to compile.

```shell
$ sudo apt install build-essential python3-dev libasound2-dev
$ tar -xf 2.10.tar.gz && cd pjproject-2.10/
$ export CFLAGS="$CFLAGS -fPIC"
$ ./configure --enable-shared
$ make dep
$ make
$ sudo make install
```

# Install Python3 bindings
By default PJSIP does not support Python3. We will install Python3 bindings. Follow the below commands to install Python3 bindings.

```shell
$ sudo apt install python3-dev
$ cd pjproject-2.10/pjsip-apps/src/
$ git clone https://github.com/mgwilliams/python3-pjsip.git
$ cd python3-pjsip
```
There is an issue with the above code. I was unable to send DTMF tones. So I made some changes in `_pjsua.c` file. Comment out the below lines in the function `py_pjsua_call_dial_dtmf`.

```c
static PyObject *py_pjsua_call_dial_dtmf(PyObject *pSelf, PyObject *pArgs)
{    	
    int call_id;
    ...

    /*
    if (!PyBytes_Check(pDigits))
	    return Py_BuildValue("i", PJ_EINVAL);
    */

    ...
}
```
Run the below commands to compile and install

```shell
$ python3 setup.py build
$ sudo python3 setup.py install
```
Now you can send DTMF tones using Python

# Check your installation

```shell
$ python3
Python 3.6.9 (default, Jul 17 2020, 12:50:27) 
[GCC 8.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import pjsua
>>> 
```

