# gobox
Easy vagrant. Configure box in gobox.yaml. Vhosts will be created and hosts file will be updated automagically.

## Installation
From your project folder, run:

```
git clone git@github.com:Useful-Innovation/gobox.git .vagrant && make -C .vagrant
```

A Vagrantfile and a sample gobox.yaml will be created.

## Sample `gobox.yaml`

`projectName` = Base name of project folder.

```yaml
---
machine:                          # all or some can be omitted
    box:        ubuntu/trusty64   # default, can be omitted
    memory:     1024              # default, can be omitted
    ip:         192.168.13.37     # can be omitted, defaults to 192.168.200.{hashed projectName}
    hostname:   MYBOX             # can be omitted, defaults to project directory name
folders:                          # object of target => source, defaults to /home/vagrant/{projectName} => ./
    /home/vagrant/foo: foo
    /home/vagrant/bar: bar
sites:                            # object of target => alias/-es, defaults to /home/vagrant/{projectName} => {projectName}
    /home/vagrant/foo:
        -   foo.dev
        -   www.foo.dev
    /home/vagrant/bar: api.foo.dev
versions:                         # all or some can be omitted
    apache:     2.4.*             # default, can be omitted, has to be compatible with apt-get
    php:        5.5.*             # default, can be omitted, has to be compatible with apt-get
    mysql:      5.5.*             # default, can be omitted, has to be compatible with apt-get
databases:                        # str/array, can be omitted, defaults to one database named {projectName}
    - foo
provisioners:                     # all or some can be omitted
    always:                       # array, will run every 'up' as user
    - "do stuff"
    always_root:                  # array, will run every 'up' as root
    - "do stuff"
    provision:                    # array, will run on first 'up' or explicit provision as user
    - "do stuff"
    provision_root:               # array, will run on first 'up' or explicit provision as root
    - "do stuff"
```
