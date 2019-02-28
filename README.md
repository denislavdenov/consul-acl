# Sample repo showing how to use Consul ACL

We use ACL in Consul so we can have another layer of security.
We are using 3 tokens in this example:
- Agent token that we use as Default token type into the configuration file so it allows node join/leave, service registration and discovery and DNS interface to work.
```
consul acl policy create  -name "agent-token" -description "Agent Token Policy" -rules @/vagrant/policy/agent-policy.hcl
consul acl token create -description "Agent Token" -policy-name "agent-token" > /vagrant/keys/agent.txt
```

- KV token that we use for inserting values into KV store and for Consul-template that reads from KV store and updades website's homepage
```
consul acl policy create  -name "kv-token" -description "KV token policy" -rules @/vagrant/policy/kv.hcl
consul acl token create -description "KV Token" -policy-name "kv-token" > /vagrant/keys/kv.txt
```

- Snapshot token that we use for consul snapshot commands 
```
consul acl policy create  -name "snapshot-token" -description "Snapshot token policy" -rules @/vagrant/policy/snapshot.hcl
consul acl token create -description "Snapshot Token" -policy-name "snapshot-token" > /vagrant/keys/snapshot.txt
```

We store the tokens into text files for later usage. Ideally they are kept in Vault.

# What to do:

You only need to do `vagrant up` and you will have 2 Consul server cluster and 1 Consul agent registering nginx web service.

