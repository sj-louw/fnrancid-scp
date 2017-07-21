# fnrancid-scp

Unfortunately, while Rancid supports Fortinet devices, it doesn’t work well with “VDOMs” (virtual domains), and there are problems when restoring the configuration. The issue is that when you execute “show full-configuration”, it doesn’t dump everything!
The one true way of getting the full configuration of Fortinet devices is via scp. It works quite well, and you might even say that it is superior than using the an interactive SSH session to transfer the data.

Rancid support for Fortinet devices using the scp interface.

License: same as whatever license rancid version 3 uses

## Installation

1.   Enable scp on your Fortinet devices:

        config system global
           set admin-scp enable
        end

1.   Copy the 'fnrancid-scp' script to the location where the other rancid scripts
     are located. On FreeBSD it is /usr/local/libexec/rancid.

1.   Make sure that it is executable:
     
        chmod +x /usr/local/libexec/rancid/fnrancid-scp

1.   Edit the file rancid.types.conf (located in /etc/rancid or /usr/local/etc/rancid) and add the following line:
     
        fortiscp;script;fnrancid-scp

1.   Make sure that you have user and password stored in ~rancid/.cloginrc:

        add user       myhostname.mydomain   {admin}
        add password   myhostname.mydomain   {mypassword}

     (note that hostname matching with wildcards doesn't work here, so put your full hostname in .cloginrc)

1.   Add your devices to router.db and use the type 'fortiscp'. For example:

        myhostname.mydomain;fortiscp;up
