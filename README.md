!!!!! WARNING !!!!!

WILL BE DEPRECATING WITH THE NEXT ASTERISK 14.7 VERSION, OAUTH SUPPORT IS NOW INCLUDED

https://github.com/asterisk/asterisk/commit/dc4435f68dd50cb1fbf40a8d49aa3c906ea6d125

!!!!! WARNING !!!!!


Google Voice support for Wazo with oauth2
=========================================

This provides an XMPP module for Asterisk with oauth support, which allows you to use
google voice with Asterisk.
It works with asterisk versions 13 or later.

The source of the patches is in debian/patches directory. The res_xmpp.c is from asterisk vanilla 14.0.2 sources.

Tested with xivo 16.10. (Thanks to Ward Mundy to give me the informations and thank to Asterisk wiki for the documentation)

- http://nerdvittles.com
- https://wiki.asterisk.org/wiki/display/AST/Calling+using+Google

Tutorial to use it with incrediblepbx for Wazo is here : http://nerdvittles.com/?p=19169

Requirements
------------
- Asterisk 13 (or later) header files (http://asterisk.org)
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
    $ modules load chan_motif.so

Or add the module on your /etc/asterisk/modules.conf

Configuration
-------------

Please edit xmpp_oauth.conf and motif.conf in /etc/asterisk/. (see samples in configs)

To get a token please follow this documentation : http://pbxinaflash.com/community/resources/incredible-pbx-google-voice-oauth.46/

You need to add icesupport=yes in /etc/asterisk/rtp.conf.

Add gv.conf in /etc/asterisk/extensions_extra.d/ and edit this file to add your DID in GV_DID variables.

    chown asterisk.www-data /etc/asterisk/extensions_extra.d/gv.conf
    chmod 660 /etc/asterisk/extensions_extra.d/gv.conf
    asterisk -rx "core reload"

Add your google voice DID in incoming call on the wazo web interface.

To do call with google voice add a custom trunk with:

 * name googlevoice
 * interface Motif/googlevoice
 * suffix @voice.google.com

In your outgoing call for google voice, use this custom trunk, please add the subroutine subr-google-voice.
