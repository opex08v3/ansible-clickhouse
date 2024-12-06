# Clickhouse

---
## Clickhouse config
```yaml
clickhouse_version: "22.2.2.1"
clickhouse_listen_host: "0.0.0.0"
clickhouse_http_port: 8123
clickhouse_tcp_port: 9000
clickhouse_path: /var/lib/clickhouse
clickhouse_zookeeper_nodes:
  - host: 127.0.0.1
    port: 2181
clickhouse_ssl_enabled: true
clickhouse_ssl_cert_path: /etc/clickhouse-server/server.crt
clickhouse_ssl_key_path: /etc/clickhouse-server/server.key
clickhouse_dhparam_path: /etc/clickhouse-server/dhparam.pem

clickhouse_log_level: "information"
clickhouse_log_size: "1000M"
clickhouse_log_count: 3
clickhouse_https_port: 8443
clickhouse_tcp_port_secure: 9440
clickhouse_interserver_http_port: 9009
clickhouse_max_server_memory_usage: 1073741824 # 1 GiB
clickhouse_max_size_to_drop: "10000M"

clickhouse_users:
  - name: default
    password: ""
    profile: default
    quota: default
    networks: ["::/0"]

# Custom clickhouse settings
clickhouse_custom_settings: {}

# Zookeper config
clickhouse_zookeeper_enabled: true
zookeeper_servers:
  - host: 127.0.0.1
    id: 1
  - host: zoo2
    id: 2
  - host: zoo3
    id: 3

# Backup and restore config
backup_retention_days: 1

aws_access_key: ""
aws_secret_key: ""
aws_bucket: ""
aws_region: ""
```

## Проверка работы бекапирования
```bash
crontab -u clickhouse -l
0 3 * * * /opt/scripts/backup_to_s3.sh
```
## Восстановление из бекапа
 Указываем дату которая имеется в /var/lib/clickhouse/backup, если такой даты в локальном хранилище, скачивается из S3 и восстанваливается.
```bash
/opt/scritps/restore_from_backup.sh 20241205 
```
