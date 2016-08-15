Xmpp support for Asterisk with oauth
====================================

This provides an XMPP module for Asterisk with oauth support, which allows you to use
google voice with Asterisk.
It works with asterisk versions 13.x or later

Requirements
------------
- Asterisk 13.x (or later) header files (http://asterisk.org)
- libiksemel libraries and header files
- libssl libraries and header files
- patch command

Installation
------------

    $ make patch
    $ make
    $ make install

To install the sample configuration file, issue the following command after
the 'make install' command:

    $ make samples

Load the module:

    $ systemctl restart asterisk
    $ asterisk -r
    $ modules load res_xmpp_oauth.so

Or add the module on your /etc/asterisk/modules.conf

Configuration
-------------

Please edit xmpp_oauth.conf in /etc/asterisk/.
