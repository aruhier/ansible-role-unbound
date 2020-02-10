Ansible Role: Unbound
=====================

[![Build Status](https://travis-ci.org/Anthony25/ansible-role-unbound.svg?branch=master)](https://travis-ci.org/Anthony25/ansible-role-unbound)

Ansible role to install and configure Unbound.

Role default variables
----------------------

As there is a lot of options in unbound, only the default values will be listed
here.
Some variables are override depending on the distribution.

```yaml
unbound_conf_path: "/etc/unbound/unbound.conf"
unbound_enable_service: true
unbound_service_name: "unbound"
unbound_packages:
  - "unbound"

### Server ###

unbound_verbosity: 1
unbound_username: "unbound"
unbound_directory: "/etc/unbound"

unbound_port: 53
unbound_num_threads: 1
unbound_interfaces:
  - 127.0.0.1
  - ::1
unbound_outgoing_interfaces: []
unbound_do_ip4: "yes"
unbound_do_ip6: "yes"
unbound_do_udp: "yes"
unbound_do_tcp: "yes"

# list of strings, as the order impact how policies are interpreted
unbound_outgoing_policies: []

unbound_access_control: []
unbound_access_control_tag: []
unbound_access_control_tag_action: []
unbound_access_control_tag_data: []
unbound_access_control_view: []

unbound_private_addresses: []
unbound_private_domains: []
unbound_domains_insecure: []
unbound_do_not_query_addresses: []
unbound_local_zones: []
unbound_local_datas: []
unbound_local_data_ptrs: []
unbound_local_zone_tags: []
unbound_local_zone_overrides: []

unbound_trust_anchors: []
unbound_trusted_keys_files: []

### Remote Control ###

unbound_control_enable: "no"
unbound_control_interface: []

### Stub, forward zones and others ###

unbound_stub_zones: []  # list of dicts
unbound_forward_zones: []  # list of dicts

# For stub and forward zones, if a key inside one of the dict is an iterable,
# it will iterate inside it to duplicate the option with all the contained
# values.
# Can be useful in case of multiple forward-addr for a same zone:
#   Example:
#     unbound_forward_zones:
#       - {name: "test.tld", "forward-addr": ["192.0.2.5", "192.0.2.6"]}

unbound_views: []  # list of strings, as options can be multiples
```

Look at the Unbound documentation to get a complete list of options.

When wanting to use an option non listed in the default variables, add the
prefix `unbound_` and replace all dash by an underscore.
If the option can be specified multiple times in `unbound.conf`, it normally
has been transformed in a list for the template. Therefore it should be part of
the default variables.

Check in the `unbound.conf.j2` template if the option is listed, otherwise do
not hesitate to open an issue and I will include it (it is possible that
options brought by a new unbound release would be missing here).

Dependencies
------------

None

Authors
-------

  * Anthony Ruhier (Anthony25)
  * Jonathan Wright (neonardo1)

License
-------

Tool under the BSD license. Do not hesitate to report bugs, ask me some
questions or do some pull request if you want to!
