### Создание инстанса виртуальной машины в Yandex Compute Cloud. SSH-ключ включён в команду.

`Windows PowerShell`
`Copyright (C) Microsoft Corporation. All rights reserved.`

`Try the new cross-platform PowerShell https://aka.ms/pscore6`

`PS C:\Users\Work> yc compute instance create otus-pg-on-ubuntu --zone ru-central1-a --network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4 --preemptible --platform standard-v3 --cores 4 --core-fraction 20 --memory 4GB --create-boot-disk image-folder-id=standard-images,image-family=ubuntu-2204-lts --ssh-key "C:\Users\Work/.ssh/id_ed25519.pub"`
`done (31s)`
`id: fhmuq1dhoqbabdki90qk`
`folder_id: b1gc61l3oggfamsi4ivu`
`created_at: "2022-11-16T14:21:03Z"`
`name: otus-pg-on-ubuntu`
`zone_id: ru-central1-a`
`platform_id: standard-v3`
`resources:`
  `memory: "4294967296"`
  `cores: "4"`
  `core_fraction: "20"`
`status: RUNNING`
`metadata_options:`
  `gce_http_endpoint: ENABLED`
  `aws_v1_http_endpoint: ENABLED`
  `gce_http_token: ENABLED`
  `aws_v1_http_token: ENABLED`
`boot_disk:`
  `mode: READ_WRITE`
  `device_name: fhmteu8vp4deg8l9lbf2`
  `auto_delete: true`
  `disk_id: fhmteu8vp4deg8l9lbf2`
`network_interfaces:`

  - `index: "0"`
    `mac_address: d0:0d:1e:d0:5b:1c`
    `subnet_id: e9bul6bokkqmqdciclni`
    `primary_v4_address:`
      `address: 10.128.0.9`
      `one_to_one_nat:`
        `address: 51.250.68.139`
        `ip_version: IPV4`
    `fqdn: fhmuq1dhoqbabdki90qk.auto.internal`
    `scheduling_policy:`
    `preemptible: true`
    `network_settings:`
    `type: STANDARD`
    `placement_policy: {}`

`There is a new yc version '0.98.0' available. Current version: '0.97.0'.`
`See release notes at https://cloud.yandex.ru/docs/cli/release-notes`
`You can install it by running the following command in your shell:`
        `$ yc components update`



### Остановка и перезапуск инстанса  для расширения загрузочного диска.

##### При создании инстанса из публичного образа через CLI нельзя задать желаемый размер диска, а размер по умолчанию слишком мал.



`PS C:\Users\Work> yc compute instance stop otus-pg-on-ubuntu`
`done (21s)`
`PS C:\Users\Work> yc compute disk resize fhmteu8vp4deg8l9lbf2 --size 15GB`
`done (12s)`
`id: fhmteu8vp4deg8l9lbf2`
`folder_id: b1gc61l3oggfamsi4ivu`
`created_at: "2022-11-16T14:21:17Z"`
`type_id: network-hdd`
`zone_id: ru-central1-a`
`size: "16106127360"`
`block_size: "4096"`
`product_ids:`

  - `f2ead5vf1k2850mdb0cq`
`status: READY`
`source_image_id: fd8ch5n0oe99ktf1tu8r`
`instance_ids:`
  - `fhmuq1dhoqbabdki90qk`
`disk_placement_policy: {}`

`PS C:\Users\Work> yc compute instance start otus-pg-on-ubuntu`
`done (15s)`
`id: fhmuq1dhoqbabdki90qk`
`folder_id: b1gc61l3oggfamsi4ivu`
`created_at: "2022-11-16T14:21:03Z"`
`name: otus-pg-on-ubuntu`
`zone_id: ru-central1-a`
`platform_id: standard-v3`
`resources:`
  `memory: "4294967296"`
  `cores: "4"`
  `core_fraction: "20"`
`status: RUNNING`
`metadata_options:`
  `gce_http_endpoint: ENABLED`
  `aws_v1_http_endpoint: ENABLED`
  `gce_http_token: ENABLED`
  `aws_v1_http_token: ENABLED`
`boot_disk:`
  `mode: READ_WRITE`
  `device_name: fhmteu8vp4deg8l9lbf2`
  `auto_delete: true`
  `disk_id: fhmteu8vp4deg8l9lbf2`
`network_interfaces:`
  - `index: "0"`
    `mac_address: d0:0d:1e:d0:5b:1c`
    `subnet_id: e9bul6bokkqmqdciclni`
    `primary_v4_address:`
      `address: 10.128.0.9`
      `one_to_one_nat:`
        `address: 51.250.95.226`
        `ip_version: IPV4`
    `fqdn: fhmuq1dhoqbabdki90qk.auto.internal`
    `scheduling_policy:`
    `preemptible: true`
    `network_settings:`
    `type: STANDARD`
    `placement_policy: {}`



#### Вход на новый инстанс по SSH (консоль 1):

`PS C:\Users\Work> ssh yc-user@51.250.95.226`
`The authenticity of host '51.250.95.226 (51.250.95.226)' can't be established.`
`ECDSA key fingerprint is SHA256:hfdWv7oLujU82pcCvYJkZB9k8RsRwpFkFskEaICfe1s.`
`Are you sure you want to continue connecting (yes/no/[fingerprint])? yes`
`Warning: Permanently added '51.250.95.226' (ECDSA) to the list of known hosts.`
`Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-52-generic x86_64)`

 * `Documentation:  https://help.ubuntu.com`
 * `Management:     https://landscape.canonical.com`
 * `Support:        https://ubuntu.com/advantage`

  `System information as of Wed Nov 16 02:41:44 PM UTC 2022`

  `System load:  0.0                Processes:             145`
  `Usage of /:   27.9% of 14.68GB   Users logged in:       0`
  `Memory usage: 5%                 IPv4 address for eth0: 10.128.0.9`
  `Swap usage:   0%`

`0 updates can be applied immediately.`



`The programs included with the Ubuntu system are free software;`
`the exact distribution terms for each program are described in the`
`individual files in /usr/share/doc/*/copyright.`

`Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by`
`applicable law.`

`yc-user@fhmuq1dhoqbabdki90qk:~$`



#### Установка PostgreSQL из дистрибутива по умолчанию.

`yc-user@fhmuq1dhoqbabdki90qk:~$ sudo apt-get -y install postgresql`
`Reading package lists... Done`
`Building dependency tree... Done`
`Reading state information... Done`
`The following packages were automatically installed and are no longer required:`
  `libflashrom1 libftdi1-2`
`Use 'sudo apt autoremove' to remove them.`
`The following additional packages will be installed:`
  `libcommon-sense-perl libjson-perl libjson-xs-perl libllvm14 libpq5 libsensors-config libsensors5`
  `libtypes-serialiser-perl postgresql-14 postgresql-client-14 postgresql-client-common postgresql-common ssl-cert`
  `sysstat`
`Suggested packages:`
  `lm-sensors postgresql-doc postgresql-doc-14 isag`
`The following NEW packages will be installed:`
  `libcommon-sense-perl libjson-perl libjson-xs-perl libllvm14 libpq5 libsensors-config libsensors5`
  `libtypes-serialiser-perl postgresql postgresql-14 postgresql-client-14 postgresql-client-common postgresql-common`
  `ssl-cert sysstat`
`0 upgraded, 15 newly installed, 0 to remove and 0 not upgraded.`
`Need to get 42.4 MB of archives.`
`After this operation, 161 MB of additional disk space will be used.`
`Get:1 http://ru.archive.ubuntu.com/ubuntu jammy/main amd64 libcommon-sense-perl amd64 3.75-2build1 [21.1 kB]`
`Get:2 http://ru.archive.ubuntu.com/ubuntu jammy/main amd64 libjson-perl all 4.04000-1 [81.8 kB]`
`Get:3 http://ru.archive.ubuntu.com/ubuntu jammy/main amd64 libtypes-serialiser-perl all 1.01-1 [11.6 kB]`
`Get:4 http://ru.archive.ubuntu.com/ubuntu jammy/main amd64 libjson-xs-perl amd64 4.030-1build3 [87.2 kB]`
`Get:5 http://ru.archive.ubuntu.com/ubuntu jammy/main amd64 libllvm14 amd64 1:14.0.0-1ubuntu1 [24.0 MB]`
`Get:6 http://ru.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libpq5 amd64 14.5-0ubuntu0.22.04.1 [140 kB]`
`Get:7 http://ru.archive.ubuntu.com/ubuntu jammy/main amd64 libsensors-config all 1:3.6.0-7ubuntu1 [5,274 B]`
`Get:8 http://ru.archive.ubuntu.com/ubuntu jammy/main amd64 libsensors5 amd64 1:3.6.0-7ubuntu1 [26.3 kB]`
`Get:9 http://ru.archive.ubuntu.com/ubuntu jammy/main amd64 postgresql-client-common all 238 [29.6 kB]`
`Get:10 http://ru.archive.ubuntu.com/ubuntu jammy-updates/main amd64 postgresql-client-14 amd64 14.5-0ubuntu0.22.04.1 [1,219 kB]`
`Get:11 http://ru.archive.ubuntu.com/ubuntu jammy/main amd64 ssl-cert all 1.1.2 [17.4 kB]`
`Get:12 http://ru.archive.ubuntu.com/ubuntu jammy/main amd64 postgresql-common all 238 [169 kB]`
`Get:13 http://ru.archive.ubuntu.com/ubuntu jammy-updates/main amd64 postgresql-14 amd64 14.5-0ubuntu0.22.04.1 [16.1 MB]`
`Get:14 http://ru.archive.ubuntu.com/ubuntu jammy/main amd64 postgresql all 14+238 [3,288 B]`
`Get:15 http://ru.archive.ubuntu.com/ubuntu jammy/main amd64 sysstat amd64 12.5.2-2build2 [487 kB]`
`Fetched 42.4 MB in 0s (93.1 MB/s)`
`Preconfiguring packages ...`
`Selecting previously unselected package libcommon-sense-perl:amd64.`
`(Reading database ... 109046 files and directories currently installed.)`
`Preparing to unpack .../00-libcommon-sense-perl_3.75-2build1_amd64.deb ...`
`Unpacking libcommon-sense-perl:amd64 (3.75-2build1) ...`
`Selecting previously unselected package libjson-perl.`
`Preparing to unpack .../01-libjson-perl_4.04000-1_all.deb ...`
`Unpacking libjson-perl (4.04000-1) ...`
`Selecting previously unselected package libtypes-serialiser-perl.`
`Preparing to unpack .../02-libtypes-serialiser-perl_1.01-1_all.deb ...`
`Unpacking libtypes-serialiser-perl (1.01-1) ...`
`Selecting previously unselected package libjson-xs-perl.`
`Preparing to unpack .../03-libjson-xs-perl_4.030-1build3_amd64.deb ...`
`Unpacking libjson-xs-perl (4.030-1build3) ...`
`Selecting previously unselected package libllvm14:amd64.`
`Preparing to unpack .../04-libllvm14_1%3a14.0.0-1ubuntu1_amd64.deb ...`
`Unpacking libllvm14:amd64 (1:14.0.0-1ubuntu1) ...`
`Selecting previously unselected package libpq5:amd64.`
`Preparing to unpack .../05-libpq5_14.5-0ubuntu0.22.04.1_amd64.deb ...`
`Unpacking libpq5:amd64 (14.5-0ubuntu0.22.04.1) ...`
`Selecting previously unselected package libsensors-config.`
`Preparing to unpack .../06-libsensors-config_1%3a3.6.0-7ubuntu1_all.deb ...`
`Unpacking libsensors-config (1:3.6.0-7ubuntu1) ...`
`Selecting previously unselected package libsensors5:amd64.`
`Preparing to unpack .../07-libsensors5_1%3a3.6.0-7ubuntu1_amd64.deb ...`
`Unpacking libsensors5:amd64 (1:3.6.0-7ubuntu1) ...`
`Selecting previously unselected package postgresql-client-common.`
`Preparing to unpack .../08-postgresql-client-common_238_all.deb ...`
`Unpacking postgresql-client-common (238) ...`
`Selecting previously unselected package postgresql-client-14.`
`Preparing to unpack .../09-postgresql-client-14_14.5-0ubuntu0.22.04.1_amd64.deb ...`
`Unpacking postgresql-client-14 (14.5-0ubuntu0.22.04.1) ...`
`Selecting previously unselected package ssl-cert.`
`Preparing to unpack .../10-ssl-cert_1.1.2_all.deb ...`
`Unpacking ssl-cert (1.1.2) ...`
`Selecting previously unselected package postgresql-common.`
`Preparing to unpack .../11-postgresql-common_238_all.deb ...`
`Adding 'diversion of /usr/bin/pg_config to /usr/bin/pg_config.libpq-dev by postgresql-common'`
`Unpacking postgresql-common (238) ...`
`Selecting previously unselected package postgresql-14.`
`Preparing to unpack .../12-postgresql-14_14.5-0ubuntu0.22.04.1_amd64.deb ...`
`Unpacking postgresql-14 (14.5-0ubuntu0.22.04.1) ...`
`Selecting previously unselected package postgresql.`
`Preparing to unpack .../13-postgresql_14+238_all.deb ...`
`Unpacking postgresql (14+238) ...`
`Selecting previously unselected package sysstat.`
`Preparing to unpack .../14-sysstat_12.5.2-2build2_amd64.deb ...`
`Unpacking sysstat (12.5.2-2build2) ...`
`Setting up postgresql-client-common (238) ...`
`Setting up libsensors-config (1:3.6.0-7ubuntu1) ...`
`Setting up libpq5:amd64 (14.5-0ubuntu0.22.04.1) ...`
`Setting up libcommon-sense-perl:amd64 (3.75-2build1) ...`
`Setting up postgresql-client-14 (14.5-0ubuntu0.22.04.1) ...`
`update-alternatives: using /usr/share/postgresql/14/man/man1/psql.1.gz to provide /usr/share/man/man1/psql.1.gz (psql.1.gz) in auto mode`
`Setting up ssl-cert (1.1.2) ...`
`Setting up libsensors5:amd64 (1:3.6.0-7ubuntu1) ...`
`Setting up libllvm14:amd64 (1:14.0.0-1ubuntu1) ...`
`Setting up libtypes-serialiser-perl (1.01-1) ...`
`Setting up libjson-perl (4.04000-1) ...`
`Setting up sysstat (12.5.2-2build2) ...`

`Creating config file /etc/default/sysstat with new version`
`update-alternatives: using /usr/bin/sar.sysstat to provide /usr/bin/sar (sar) in auto mode`
`Created symlink /etc/systemd/system/sysstat.service.wants/sysstat-collect.timer → /lib/systemd/system/sysstat-collect.timer.`
`Created symlink /etc/systemd/system/sysstat.service.wants/sysstat-summary.timer → /lib/systemd/system/sysstat-summary.timer.`
`Created symlink /etc/systemd/system/multi-user.target.wants/sysstat.service → /lib/systemd/system/sysstat.service.`
`Setting up libjson-xs-perl (4.030-1build3) ...`
`Setting up postgresql-common (238) ...`
`Adding user postgres to group ssl-cert`

`Creating config file /etc/postgresql-common/createcluster.conf with new version`
`Building PostgreSQL dictionaries from installed myspell/hunspell packages...`
`Removing obsolete dictionary files:`
`Created symlink /etc/systemd/system/multi-user.target.wants/postgresql.service → /lib/systemd/system/postgresql.service.`
`Setting up postgresql-14 (14.5-0ubuntu0.22.04.1) ...`
`Creating new PostgreSQL cluster 14/main ...`
`/usr/lib/postgresql/14/bin/initdb -D /var/lib/postgresql/14/main --auth-local peer --auth-host scram-sha-256 --no-instructions`
`The files belonging to this database system will be owned by user "postgres".`
`This user must also own the server process.`

`The database cluster will be initialized with locale "en_US.UTF-8".`
`The default database encoding has accordingly been set to "UTF8".`
`The default text search configuration will be set to "english".`

`Data page checksums are disabled.`

`fixing permissions on existing directory /var/lib/postgresql/14/main ... ok`
`creating subdirectories ... ok`
`selecting dynamic shared memory implementation ... posix`
`selecting default max_connections ... 100`
`selecting default shared_buffers ... 128MB`
`selecting default time zone ... Etc/UTC`
`creating configuration files ... ok`
`running bootstrap script ... ok`
`performing post-bootstrap initialization ... ok`
`syncing data to disk ... ok`
`update-alternatives: using /usr/share/postgresql/14/man/man1/postmaster.1.gz to provide /usr/share/man/man1/postmaster.1.gz (postmaster.1.gz) in auto mode`
`Setting up postgresql (14+238) ...`
`Processing triggers for man-db (2.10.2-1) ...`
`Processing triggers for libc-bin (2.35-0ubuntu3.1) ...`
`Scanning processes...`
`Scanning linux images...`

`Running kernel seems to be up-to-date.`

`No services need to be restarted.`

`No containers need to be restarted.`

`No user sessions are running outdated binaries.`

`No VM guests are running outdated hypervisor (qemu) binaries on this host.`
`yc-user@fhmuq1dhoqbabdki90qk:~$`



#### Вход по SSH второй консолью.

`PS C:\Users\Work> ssh yc-user@51.250.95.226`
`Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-52-generic x86_64)`

 * `Documentation:  https://help.ubuntu.com`
 * `Management:     https://landscape.canonical.com`
 * `Support:        https://ubuntu.com/advantage`

  `System information as of Wed Nov 16 02:57:54 PM UTC 2022`

  `System load:  0.009765625        Processes:             163`
  `Usage of /:   29.5% of 14.68GB   Users logged in:       1`
  `Memory usage: 6%                 IPv4 address for eth0: 10.128.0.9`
  `Swap usage:   0%`

 * `Strictly confined Kubernetes makes edge and IoT secure. Learn how MicroK8s`
   `just raised the bar for easy, resilient and secure K8s cluster deployment.`

   `https://ubuntu.com/engage/secure-kubernetes-at-the-edge`

`0 updates can be applied immediately.`

`Last login: Wed Nov 16 14:54:03 2022 from 89.109.51.150`
`yc-user@fhmuq1dhoqbabdki90qk:~$`



#### Запуск psql из-под пользователя postgres (в обоих консолях)

`yc-user@fhmuq1dhoqbabdki90qk:~$ sudo -u postgres psql`
`could not change directory to "/home/yc-user": Permission denied`
`psql (14.5 (Ubuntu 14.5-0ubuntu0.22.04.1))`
`Type "help" for help.`

`postgres=#`



#### Выключение autocommit

`postgres=# \set AUTOCOMMIT OFF`



#### Создание и заполнение таблицы (консоль 1)

`postgres=# create table persons(id serial, first_name text, second_name text); insert into persons(first_name, second_name) values('ivan', 'ivanov'); insert into persons(first_name, second_name) values('petr', 'petrov'); commit;`
`CREATE TABLE`
`INSERT 0 1`
`INSERT 0 1`
`COMMIT`

#### Текущий уровень изоляции:

`postgres=# show transaction isolation level;`

 `transaction_isolation`

 `read committed`
`(1 row)`

#### Добавление новой записи в таблицу persons в консоли 1

`postgres=*# insert into persons(first_name, second_name) values('sergey', 'sergeev');`
`INSERT 0 1`

#### Выборка из таблицы persons в консоли 2. Новая строка не выбрана, т.к. в консоли 1 не выполнен commit и текущий уровень изоляции не позволяет видеть не зафиксированные изменения.

`postgres=# select * from persons;`
 `id | first_name | second_name`
`----+------------+-------------`
  `1 | ivan       | ivanov`
  `2 | petr       | petrov`
`(2 rows)`

#### COMMIT в первой консоли:

`postgres=*# commit;`
`COMMIT`

#### Повторение выборки в консоли 2. Новая строка попадает в выборку в соответствии с текущим уровнем изоляции.

`postgres=*# select * from persons;`
 `id | first_name | second_name`
`----+------------+-------------`
  `1 | ivan       | ivanov`
  `2 | petr       | petrov`
  `3 | sergey     | sergeev`
`(3 rows)`

#### Выполнение транзакции с уровнем REPEATABLE READ. В консоли 1 создаётся новая запись в persons

`postgres=# begin`
`postgres-# TRANSACTION ISOLATION LEVEL REPEATABLE READ;`
`BEGIN`
`postgres=*# show transaction isolation level;`

 `transaction_isolation`

 `repeatable read`
`(1 row)`

`postgres=*# insert into persons(first_name, second_name) values('sveta', 'svetova');`
`INSERT 0 1`

#### В консоли 2 новая запись не попадает в выборку из persons. REPEATABLE READ не позволяет читать не зафиксированные данные.

`postgres=# begin TRANSACTION ISOLATION LEVEL REPEATABLE READ;`
`BEGIN`
`postgres=*# show transaction isolation level;`

 `transaction_isolation`

 `repeatable read`
`(1 row)`

`postgres=*# select * from persons;`
 `id | first_name | second_name`
`----+------------+-------------`
  `1 | ivan       | ivanov`
  `2 | petr       | petrov`
  `3 | sergey     | sergeev`
`(3 rows)`

#### COMMIT в консоли 1;

`postgres=*# commit;`
`COMMIT`

#### В консоли 2 новая строка по-прежнему не попадает в выборку. Уровень REPEATABLE READ не позволяет видеть внутри одной транзакции изменения, которые зафиксированы другой транзакцией после начала первой транзакции.

`postgres=*# select * from persons;`
 `id | first_name | second_name`
`----+------------+-------------`
  `1 | ivan       | ivanov`
  `2 | petr       | petrov`
  `3 | sergey     | sergeev`
`(3 rows)`

#### Завершение транзакции в консоли 2

`postgres=*# commit;`
`COMMIT`

#### После завершения транзакции в консоли 2 в выборку попадает новая строка. Новая транзакция получает доступ к ранее зафиксированным изменениям в соответствии с уровнем изоляции REPEATABLE READ.

`postgres=# select * from persons;`
 `id | first_name | second_name`
`----+------------+-------------`
  `1 | ivan       | ivanov`
  `2 | petr       | petrov`
  `3 | sergey     | sergeev`
  `4 | sveta      | svetova`
`(4 rows)`