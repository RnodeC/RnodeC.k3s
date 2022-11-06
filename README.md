RnodeC.k3s
=========

This role will deploy k3s.  (linux amd64 only) 

Requirements
------------

At least a single vm.  The `k3s_role: server|agent` host or group var determines how the node gets deployed.  

Role Variables
--------------

No variables are required for this role.  See `defaults/main.yaml` for full list of available variables and their default values.  Here are a few that you might likely want to apply:

```
k3s_channel: stable
k3s_upgrade: false
k3s_token: badsecret 
k3s_api_hostname: server
ks3_api_domain: local
```

#### k3s_channel 

This variable can be "stable", "latest", "testing", or a valid kubernetes major/minor version (i.e. "v1.24").  The ansible role will pull down the latest available k3s version that corresponds to the channel.  

Dependencies
------------
None.  Optionally, apply the `RnodeC.lockdown` role (**coming soon**) to apply some added security to the cluster nodes.  

Example Playbook
----------------

```bash
---
- name: Setup k3s cluster
  hosts: cluster

  vars: 
    k3s_channel: v1.23
  
  roles:
  - role: RnodeC.k3s 
```

If this is an upgrade scenario, be sure to set `k3s_upgrade` to true. This will trigger a rolling restart of the cluster.  


Author Information
------------------

RnodeC