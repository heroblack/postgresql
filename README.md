# postgresql
installation and the most used commands

## Installation in Centos 7 and 8


    centos 8:
    sudo yum -y install https://download.postgresql.org/pub/repos/yum/reporpms/EL-8-x86_64/pgdg-redhat-repo-latest.noarch.rpm
    Disable the built-in PostgreSQL module:
    sudo dnf -qy module disable postgresql
    sudo dnf -y install postgresql12 postgresql12-server
    
    
    
    centos 7:
    sudo yum -y install https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
    sudo yum -y install epel-release yum-utils
    sudo yum-config-manager --enable pgdg12
    sudo yum install postgresql12-server postgresql12

    Initialize and start database service: 
    sudo /usr/pgsql-12/bin/postgresql-12-setup initdb
    sudo systemctl enable --now postgresql-12
    systemctl status postgresql-12
    
    firewall: 
    sudo firewall-cmd --add-service=postgresql --permanent
    sudo firewall-cmd --reload 
    
    ```bash
    $ sudo su - postgres 
    $ psql -c "alter user postgres with password 'StrongPassword'" 
    ALTER ROLE
    ```
    
    Enable remote access (Optional)
    
    Edit the file /var/lib/pgsql/12/data/postgresql.conf and set Listen address to your server IP address or “*” for all interfaces.
    
    listen_addresses = '192.168.10.10'
    Also set PostgreSQL to accept remote connections
    
    $ sudo vim /var/lib/pgsql/12/data/pg_hba.conf
    
    # Accept from anywhere
    host all all 0.0.0.0/0 md5
    
    # Accept from trusted subnet
    host all all 192.168.18.0/24 md5
    Restart database service after committing the change.
    
    sudo systemctl restart postgresql-12
