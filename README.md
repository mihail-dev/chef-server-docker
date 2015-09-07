# [chef-server-docker](https://github.com/xmik/chef-server-docker)

Used Chef Server 11.1.6-1_amd64 on an Ubuntu Trusty 14.04 LTS.

This is a fork of: [c-buisson/chef-server](https://github.com/c-buisson/chef-server) but I took run_chef_server.sh from [tmc/dockerfiles](https://github.com/tmc/dockerfiles/tree/master/chef-server) available on docker registry [base/chef-server](https://registry.hub.docker.com/u/base/chef-server/).

I forked it in order to avoid Chef Server being reconfigured on container each restart. For me it kept reconfiguring endlessly and was temporarily unavailable through web browser. 



## Usage
Use the `--privileged` option or else the shared memory max cannot be set and some of Chef Server components may not start (rabbitmq server and/or postgresql).  
```
$ docker run --privileged -dti --name chef_server -p 443:443 xmik/chef-server-docker:0.0.2
```

To confirm that you have connected to Chef Server, list users specifying path to knife.rb:
```bash
user@host:~$ knife user list -c knife.rb
```

To export or restore Chef Server backup see [mdxp/knife-backup](https://github.com/mdxp/knife-backup).

## Build
Build an image using the tag from script/image_metadata.txt. Use rake task:
```ruby
rake chef_server:build
```

Size of [xmik/chef-server-docker](https://hub.docker.com/r/xmik/chef-server-docker/):0.0.2 is 1.003 GB.


