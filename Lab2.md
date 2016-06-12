# Agregando RHEV como proveedor de Infraestructura

    [root@rhevm-6a77 ~]# vi /var/lib/pgsql/data/pg_hba.conf

Antes : 
    #IPv4 local connections:
    host      all       all     127.0.0.1/32    ident

Despues:

    # IPv4 local connections:
    host      all       all      0.0.0.0/0        md5

---------

cambiar ident por trust

    # IPv6 local connections:
    host        all       all       ::1/128       trust

---------

    [root@rhevm-6a77 ~]# vi /var/lib/pgsql/data/postgresql.conf

Descomentar :

    listen_addresses = '*'

--------

    [root@rhevm-6a77 ~]# service postgresql restart
    Stopping postgresql service:                               [  OK  ]
    Starting postgresql service:                               [  OK  ]

    [root@rhevm-6a77 ~]# psql -U postgres -h localhost
    psql (8.4.20)
    Type "help" for help.

    postgres=# create role cloudforms_history LOGIN unencrypted password 'redhat' superuser valid until 'infinity';
    CREATE ROLE
    postgres=# \q
