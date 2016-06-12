4.3. Data Collection for Red Hat Enterprise Virtualization 3.3 and 3.4

To collect capacity and utilization data for Red Hat Enterprise Virtualization 3.3 and 3.4, you must add CloudForms Management Engine as a user to the RHEV-M database.

Perform this procedure on the PostgreSQL server where the history database is located. Usually, this is the RHEV-M server.

    Using SSH, access the RHEV-M database server as the root user:

    $ ssh root@example.postgres.server

    Switch to the postgres user:

    # su - postgres

    Access the database prompt:

    -bash-4.1$ psql

    Create a new user for the CloudForms Management Engine:

    postgres=# CREATE ROLE cfme LOGIN UNENCRYPTED PASSWORD 'smartvm' SUPERUSER VALID UNTIL 'infinity';

    Exit to the RHEV-M database server prompt:

    postgres=# \q
    -bash-4.1$ exit

    Update the server’s firewall to accept TCP communication on port 5432:

    # iptables -I INPUT -p tcp -m tcp --dport 5432 -j ACCEPT
    # service iptables save

    Enable external md5 authentication by appending the following line to /var/lib/pgsql/data/pg_hba.conf:

    host    all      all    0.0.0.0/0     md5

    Enable PostgreSQL to listen for remote connections by updating the listen_addresses line in /var/lib/pgsql/data/postgresql.conf:

    listen_addresses  =  '*'

    Reload the PostgreSQL configuration:

    service postgresql reload
