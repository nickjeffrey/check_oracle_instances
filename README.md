# check_oracle_instances
nagios check to confirm Oracle databases in /etc/oratab are running

# Requirements
perl, ssh  on nagios server

# Configuration

This script is executed remotely on a monitored system by the NRPE or check_by_ssh  methods available in nagios.

If you hare using the check_by_ssh method, you will need a section in the services.cfg file on the nagios server that looks similar to the following.
This assumes that you already have ssh key pairs configured.
```
    # Define service for checking state of running oracle database instances
    define service{
       use                             generic-24x7-service
       host_name                       unix11
       service_description             oracle instances
       check_command                   check_by_ssh!"/usr/local/nagios/libexec/check_oracle_instances"
       }
```

Alternatively, if you are using the NRPE method, you should have a section similar to the following in the services.cfg file:
```
    define service{
       use                             generic-24x7-service
       host_name                       unix11
       service_description             oracle instances
       check_command                   check_nrpe!check_oracle_instances -t 30
       }
```

If you are using the NRPE method, you will also need a command definition similar to the following on each monitored host in the /usr/local/nagios/nrpe/nrpe.cfg file:
```
    command[check_oracle_instances]=/usr/local/nagios/libexec/check_oracle_instances
```
