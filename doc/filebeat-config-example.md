# Example configuration Filebeat

`/etc/filebeat/filebeat.yml`
```yaml
filebeat.config:
  inputs:
    enabled: false
    path: /etc/filebeat/inputs.d/*.yml
    reload.enabled: true
    reload.period: 10s
  modules:
    enabled: true
    path: /etc/filebeat/modules.d/*.yml
    reload.enabled: true
    reload.period: 10s

output:
  elasticsearch:
    hosts: 'elk.by:9200'
    username: 'elastic'
    password: 'secret2'
    indices:
      - index: "filebeat-apache2-domains2-by-%{[agent.version]}-%{+yyyy.MM.dd}"
        when.contains:
          log.file.path: "/var/log/apache2/domains2.by"

      - index: "filebeat-app-%{[agent.version]}-%{+yyyy.MM.dd}"
        when.contains:
          log.file.path: "/app/var/log/"

      - index: "filebeat-mysql-%{[agent.version]}-%{+yyyy.MM.dd}"
        when.contains:
          log.file.path: "/var/log/mysql"

      - index: "filebeat-apache2-domain-by-%{[agent.version]}-%{+yyyy.MM.dd}"
        when.contains:
          log.file.path: "/var/log/apache2/domain.by"

      - index: "filebeat-system-%{[agent.version]}-%{+yyyy.MM.dd}"
        when.contains:
          event.module: "system"
```

`/etc/filebeat/inputs.d/app.yml`
```yaml
- type: log
  paths:
    - /app/var/log/*.log
  json:
    keys_under_root: true
    message_key: message
    overwrite_keys: true
```

`/etc/filebeat/modules.d/apache.yml`
```yaml
- module: apache
  access:
    enabled: true
    var.paths:
      - /var/log/apache2/domain.by.log*
      - /var/log/apache2/domains2.by.log*
  error:
    enabled: true
    var.paths:
      - /var/log/apache2/domain.by.error.log*
      - /var/log/apache2/domains2.by.error.log*
```

`/etc/filebeat/modules.d/mysql.yml`
```yaml
- module: mysql
  error:
    enabled: true
    var.paths:
      - /mnt/logs/mysql/error.log*
  slowlog:
    enabled: true
    var.paths:
      - /mnt/logs/mysql/mysql-slow.log*
```

`/etc/filebeat/modules.d/system.yml`
```yaml
- module: system
  syslog:
    enabled: true
    var.paths:
      - /var/log/syslog*
  auth:
    enabled: true
    var.paths:
      - /var/log/auth.log*
```
