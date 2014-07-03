Whaler
======

Whaler is a tool to make using docker containers dead simple.

- init whaler
- change settings in .yml file
- run whaler
- magic

Version
----
0.1.0

Tech
-----------

Whaler uses a number of open source projects to work properly:

* [Ansible] - simplest way to automate IT

Installation
--------------

```sh
pip install whaler
```

Config
------
Whaler uses yml for its config files, supports most of the [run] commands.

Supports variables from ansible and few extra:
* ```working_dir``` directory whaler is ran from

```yml
# Copy files from git repo to dest when building container
git:
    repo: git@bitbucket.org:skiuoros/node_app.git
    dest: git_code/
    
# Same as above but copys file from machine whaler is run from
local_files:
    dir: "{{ working_dir }}/"
    dest: local_code/

image: skiouros/node_app
base_image: node

name: node_app
command: node app.js

env:
    NODE_ENV: production

links:
    node_db: db

expose:
    - 8080

# host port : container port
ports:
    3000: 8080

# all services support the same options as above
services:
    postgres:
        image: postgres
        name: node_db

        tag: latest
```

Usage
-----

```sh
whaler init # creates .whaler folder with necessary files
```

```sh
whaler deploy --hosts local # deploys container to specified host
```

License
----

MIT

[ansible]:http://www.ansible.com/home
[run]:https://docs.docker.com/reference/run/