WARNING: WORK IN PROGRESS, not usable yet.

# Puppet module: influxdb

This is a Puppet module for influxdb based on the second generation layout ("NextGen") of Example42 Puppet Modules.
Made by Yann Hamon
Official git repository: http://github.com/yannh/puppet-influxdb

Released under the terms of Apache 2 License.

This module requires functions provided by the Example42 Puppi module (you need it even if you don't use and install Puppi)

For detailed info about the logic and usage patterns of Example42 modules check the DOCS directory on Example42 main modules set.


## USAGE - Basic management

* Install influxdb with default settings

        class { 'influxdb': }

* Install a specific version of influxdb package

        class { 'influxdb':
          version => '1.0.1',
        }

* Disable influxdb service.

        class { 'influxdb':
          disable => true
        }

* Remove influxdb package

        class { 'influxdb':
          absent => true
        }

* Enable auditing without without making changes on existing influxdb configuration *files*

        class { 'influxdb':
          audit_only => true
        }

* Module dry-run: Do not make any change on *all* the resources provided by the module

        class { 'influxdb':
          noops => true
        }


## USAGE - Overrides and Customizations
* Use custom sources for main config file 

        class { 'influxdb':
          source => [ "puppet:///modules/example42/influxdb/influxdb.conf-${hostname}" , "puppet:///modules/example42/influxdb/influxdb.conf" ], 
        }


* Use custom source directory for the whole configuration dir

        class { 'influxdb':
          source_dir       => 'puppet:///modules/example42/influxdb/conf/',
          source_dir_purge => false, # Set to true to purge any existing file not present in $source_dir
        }

* Use custom template for main config file. Note that template and source arguments are alternative. 

        class { 'influxdb':
          template => 'example42/influxdb/influxdb.conf.erb',
        }

* Automatically include a custom subclass

        class { 'influxdb':
          my_class => 'example42::my_influxdb',
        }


## USAGE - Example42 extensions management 
* Activate puppi (recommended, but disabled by default)

        class { 'influxdb':
          puppi    => true,
        }

* Activate puppi and use a custom puppi_helper template (to be provided separately with a puppi::helper define ) to customize the output of puppi commands 

        class { 'influxdb':
          puppi        => true,
          puppi_helper => 'myhelper', 
        }

* Activate automatic monitoring (recommended, but disabled by default). This option requires the usage of Example42 monitor and relevant monitor tools modules

        class { 'influxdb':
          monitor      => true,
          monitor_tool => [ 'nagios' , 'monit' , 'munin' ],
        }

* Activate automatic firewalling. This option requires the usage of Example42 firewall and relevant firewall tools modules

        class { 'influxdb':       
          firewall      => true,
          firewall_tool => 'iptables',
          firewall_src  => '10.42.0.0/24',
          firewall_dst  => $ipaddress_eth0,
        }

