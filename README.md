deploy-server
=============


## Description

this is chef script for deploy

## New Machine

eg: 
user: root
public IP: 10.111.20.111 

## Usage

1. upload your ssh public key

<pre>
ssh-copy-id root@10.111.20.111
</pre>

2. install chef for your server

<pre>
cd chef

bundle exec knife solo prepare root@10.111.20.111
</pre>

3. 执行完成后，会生成节点,  nodes/10.111.20.111.json 

vim 10.111.20.111.json

<pre>
{
  "run_list": [
      "role[server-base]",
      "role[rails-app]",
      "role[redis-server]",
      "role[memcached]",
      "role[mysql-server]",
      "role[nginx]"
  ],
  "automatic": {
    "ipaddress": "10.111.20.111"
  }
}
</pre>

4. deploy

<pre>
cd chef/

bundle exec knife solo cook root@10.111.20.111
</pre>