# RabbitMQ Ansible Role
Forked from https://github.com/jasonroyle/ansible-role-rabbitmq on 2018-08-20
to support EL 7 and RabbitMQ 3.7+.

## Version

See:

- [RabbitMQ - Server Releases](https://www.rabbitmq.com/releases/rabbitmq-server/)

Set the `rabbitmq_version` variable to define the version of RabbitMQ to install.

```yaml
rabbitmq_version: '3.7.7'
```

## Users

See:

- [Ansible - RabbitMQ User Module](http://docs.ansible.com/ansible/rabbitmq_user_module.html)
- [RabbitMQ - Access Control](https://www.rabbitmq.com/access-control.html)

Set the `rabbitmq_users` variable to define an array of present users.

```yaml
rabbitmq_users:
  - user: admin
    password: admin
    tags: administrator
```

| parameter      | required | default | choices | comments |
| -------------- | -------- | ------- | ------- | -------- |
| configure_priv | no       | .*      |         |          |
| password       | yes      |         |         |          |
| read_priv      | no       | .*      |         |          |
| tags           | no       |         |         |          |
| user           | yes      |         |         |          |
| vhost          | no       | /       |         |          |
| write_priv     | no       | .*      |         |          |

### Remove Users

Set the `rabbitmq_users_absent` variable to define an array of absent users.

```yaml
rabbitmq_users_absent:
  - guest
```

## Virtual Hosts

See:

- [Ansible - RabbitMQ Virtual Host Module](http://docs.ansible.com/ansible/rabbitmq_vhost_module.html)
- [RabbitMQ - Virtual Hosts](https://www.rabbitmq.com/vhosts.html)

Set the `rabbitmq_vhosts` variable to define an array of present virtual hosts.

```yaml
rabbitmq_vhosts:
  - /one
  - name: /two
    node: rabbit
    tracing: no
```

| parameter  | required | default | choices                          | comments |
| ---------- | -------- | ------- | -------------------------------- | -------- |
| name       | yes      |         |                                  |          |
| node       | no       | rabbit  |                                  |          |
| tracing    | no       | no      | <ul><li>yes</li><li>no</li></ul> |          |

### Remove Virtual Hosts

Set the `rabbitmq_vhosts_absent` variable to define an array of absent virtual hosts.

```yaml
rabbitmq_vhosts_absent:
  - /vhost
```

## Plugins

See:

- [Ansible - RabbitMQ Plugin Module](http://docs.ansible.com/ansible/rabbitmq_plugin_module.html)
- [RabbitMQ - Plugins](https://www.rabbitmq.com/plugins.html)

Set the `rabbitmq_plugins` variable to define an array of enabled plugins.

```yaml
rabbitmq_plugins:
  - rabbitmq_management
  - name: rabbitmq_delayed_message_exchange
    url: http://www.rabbitmq.com/community-plugins/v3.6.x/rabbitmq_delayed_message_exchange-0.0.1.ez
```

| parameter | required | default | choices | comments            |
| --------- | -------- | ------- | ------- | ------------------- |
| name      | yes      |         |         |                     |
| url       | no       |         |         | Installs the plugin |

### Disable Plugins

Set the `rabbitmq_plugins_disabled` variable to disable plugins.

```yaml
rabbitmq_plugins_disabled:
  - rabbitmq_management
```

## Configuration

See:

- [Pico Trading - Config Encoder Macros](https://github.com/picotrading/config-encoder-macros)
- [RabbitMQ - Configuration File](https://www.rabbitmq.com/configure.html#configuration-file)

Set the `rabbitmq_config` variable to define the configuration.

```yaml
rabbitmq_config:
  - rabbit:
    - tcp_listeners:
      - "'0.0.0.0'": 5671
```

## Cluster

See:

- [RabbitMQ - Clustering Guide](https://www.rabbitmq.com/clustering.html)

Set the `rabbitmq_cluster` variable to enable clustering.

As the above clustering documentation is pretty hard to grasp I suggest reading of
[https://computingforgeeks.com/how-to-configure-rabbitmq-cluster-on-ubuntu-18-04-lts/](https://computingforgeeks.com/how-to-configure-rabbitmq-cluster-on-ubuntu-18-04-lts/)
for quick start. And then defined minimum varaibles as below where the
  `rabbitmq1` is the short hostname of the master node.

```yaml
rabbitmq_cluster: yes
# shortname dns only
rabbitmq_cluster_master: "rabbit@rabbitmq1"
```

### Erlang Cookie

Set the `rabbitmq_erlang_cookie` variable to define the Erlang cookie.

```yaml
rabbitmq_erlang_cookie: g9avtqdzdm2p5oe9
```

## License

MIT
