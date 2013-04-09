check_munin_rrd
===============

A Nagios command and service plugin to read Munin data files for use by pnp4nagios.

Forked from http://code.google.com/p/nagios-munin/

Assumptions
===========
* You have Nagios (http://nagios.org/) and Munin (http://munin-monitoring.org/) installed on the same server.
* You have pnp4nagios installed (http://www.pnp4nagios.org/).

Usage
=====

Add the following to your Nagios commands.cfg. Make sure to set the path correctly for the location of your plugins directory.

```
define command {
        command_name check_munin
        command_line /usr/local/nagios/etc/plugins/check_munin_rrd/check_munin_rrd.pl -H $ARG3$ -M $ARG1$ -d $ARG2$ -i idle -N
}
```

Add the following to your host monitoring configuration for each element you want to monitor.

```
define service {
        use                     generic-service,srv-pnp
        host_name               <hostname>
        service_description     <service description for graphs>
        process_perf_data       1
        check_command           check_munin!<munin module>!<munin host group>!<munin hostname>
}
```
