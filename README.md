Deploy exporter to the node
===========================

Variables
---------

We define this as part of the role, but can be overwritten if needed:

 * `exporters_dest` - where to extract/install exporters on the node

When calling the role, configure these variables:

 * `exporter_name` - name of the exporter
 * `exporter_url` - where to download the exporter tarball
 * `exporter_port` - port used by the exporter which will be opened on the node (also used by `add-prometheus-target` role)
 * `exporter_commandline` - how to start the exporter
 * `exporter_commandline_environment` - dict of environment for the exporter
 * `exporter_extra_roles` - list of roles to run after we have unpacked exporter archive - meant for config specific to one exporter
 * `prometheus_config` - file where to add new target to scrape (needed by `add-prometheus-target` role we use)

In inventory file, you also need `prometheus` group with one server (for `add-prometheus-target` role).

Example
-------

    - name: "Deploy Node exporter"
      include_role:
        name: deploy-exporter
      vars:
        exporter_name: node_exporter
        exporter_url: https://github.com/prometheus/node_exporter/releases/download/v1.0.1/node_exporter-1.0.1.linux-amd64.tar.gz
        exporter_port: 9100
        exporter_commandline: /usr/lib/node_exporter-1.0.1.linux-amd64/node_exporter
        prometheus_config: /root/prometheus/targets/cluster.yml
