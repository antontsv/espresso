# Espresso bin board
Configurations on Marvell ARMADA 3700

# Basic configuration:
* Install Ubuntu 16.04.3 TLS:
   http://espressobin.net/wp-content/uploads/2017/10/ebin-ubuntu-16.04.3.zip

* Include Kernel 4.4.8:
  http://espressobin.net/wp-content/uploads/2017/02/kernel.zip

Note: ebin-ubuntu-16.04.3 includes kernel 4.4.52, that has frequent panics.
I suggest overwriting it using 4.4.8

# Network configuration
If you attached WAN to your router,
and need network to be up on reboot:

/etc/network/interfaces

```
auto eth0
iface eth0 inet manual
post-up /sbin/dhclient wan
```

# Serial connection

For a serial connection to a board from your MacOS, this software works well:

https://pbxbook.com/other/mac-tty.html

```
brew install c-kermit

cat > ~/kermit-connect.conf
set line /dev/tty.usbserial
set speed 115200
set carrier-watch off
set flow-control none
set handshake none
set prefixing all
set streaming off
set parity none
connect
# Control+D to stop cat input

kermit ~/kermit-connect.conf

```

# LED

When you connect DC 12V power, green LED lights up.
I was looking if there is a way to dim or turn it off through GPIO.

I don't see any so far.

Looking as the board it is labeled "LED3".
In [current schematics](http://espressobin.net/wp-content/uploads/2017/08/ESPRESSObin_V5_Schematics.pdf)

Looks like it's directly connected to power through a resistor `R48`.
There are couple capasitors and zener diodes around, which does not help.

Why would you build in high intensity LED, for such a simple thing as indicating power?
