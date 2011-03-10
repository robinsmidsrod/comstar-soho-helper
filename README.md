Administrative helper scripts for use with COMSTAR
==================================================

COMSTAR is an advanced SCSI target implementation originally developed by
Sun.  It is included in recent Solaris versions and other derived operating
systems, like Nexenta.  The problem is that iSCSI and the underlying
protocols are quite complex, and it is hard to understand how everything
fits together.

This software package contains a set of scripts that help simplify
management of a COMSTAR server.  The perspective is that of a home/small
business user/administrator with a single storage server that serves a small
amount of heterogenous clients.

Installation
============

Copy all the files in the `bin/` directory to any directory in your path.
Copy the files in `etc/` to `/etc` and customize accordingly.  See comments
in the configuration file for details.

Scripts part of this package
============================

For adding volumes, targets, clients and views (I call them links):

    iscsi_target_create <volume> <size>
    iscsi_client_add <host-group/hostname> <client-iqn>
    iscsi_link_add <target-group/volume> <host-group/hostname>

For removing things added above:

    iscsi_client_remove <host-group/hostname> <client-iqn>
    iscsi_link_remove <target-group/volume>

For disconnecting/reconnecting a ZFS volume to a target group:

    iscsi_volume_connect <volume>
    iscsi_volume_disconnect <target-group/volume>

iSCSI Terminology
=================

If you are struggling with iSCSI terminology, the excellent [tutorial by
tek-blog.com](http://tek-blog.com/main/index.php?blog=2&title=comstar_howto&more=1&c=1&tb=1&pb=1)
helped me understand more of it.

Below I've added my understanding of some common iSCSI terms:

* **Logical Unit:** link to actual storage device, e.g. zvol
* **Target:** identifier for a specific storage unit, e.g. named iqn.YYYY-MM.com.example:hostname.zvol
* **Target Portal Group:** network interface/port to listen for iSCSI target connections
* **Target Group:** a collection of multiple Targets, for redundancy etc.
* **Host Group:** multiple identifiers, usually IQNs, linking a single client, I tend to use hostname here
* **View:** a connection between a Host Group, Target Group and Logical Unit, binds everything together

Tools used to administer the different entities:

* Logical Units: sbdadm
* Targets: itadm
* Target Portal Groups: itadm
* Target Groups: stmfadm
* Host Groups: stmfadm
* Views: stmfadm

Author
======

Robin Smidsrød <robin@smidsrod.no>

Copyright
=========

Robin Smidsrød <robin@smidsrod.no>

License
=======

This code is licensed according to the [Artistic License
2.0](http://www.perlfoundation.org/artistic_license_2_0).
