# configuración inicial APPLIANCE en KVM

### 1.-  Login RHEV-M
### 2.- Dentro de Export Domain
### 3.- Copiar appiance de CF
### 4.- Extraer contenido de CF.ova

    $ tar xvf cfme-rhevm-5.3-15.x86_64.rhevm.ova

### 5.- Cambiar los permisos

    chown -R 36:36 images/
    chown -R 36:36 master/

### Una vez que ya iniciamos nuestro vm procedemos a cambiar las configuraciones default

    [root@localhost ~]# ssh 192.168.122.176
    root@192.168.122.176's password: 
    Last login: Sat Jun 11 15:19:54 2016 from 192.168.122.1
    Welcome to the Appliance Console

    For a menu, please type: appliance_console

### Ingresamos a la consola de configuración.

    [root@localhost ~]# appliance_console

    Welcome to the CFME Virtual Appliance.

    To modify the configuration, use a web browser to access the management page.

    Hostname:          localhost        
    IP Address:        192.168.122.176  
    Netmask:           255.255.255.0    
    Gateway:           192.168.122.1    
    Primary DNS:       192.168.122.1    
    Secondary DNS:                      
    Search Order:                       
    MAC Address:       52:54:00:33:fb:bc
    Timezone:          America/New_York 
    Local Database:    not running      
    CFME Database:     not configured   
    Database/Region:   not configured   
    External Auth:     not configured   
    CFME Version:      5.5.4.2          
    CFME Console:      not configured   
    Press any key to continue:
    
Comenzaremos con la personalización del appliance.

    Advanced Setting
    1) Set DHCP Network Configuration
    2) Set Static Network Configuration
    3) Test Network Configuration
    4) Set Hostname
    5) Set Timezone
    6) Set Date and Time
    7) Restore Database From Backup
    8) Setup Database Region
    9) Configure Database
    10) Extend Temporary Storage
    11) Configure External Authentication (httpd)
    12) Generate Custom Encryption Key
    13) Harden Appliance Using SCAP Configuration
    14) Stop EVM Server Processes
    15) Start EVM Server Processes
    16) Restart Appliance
    17) Shut Down Appliance
    18) Summary Information
    19) Quit

Choose the advanced setting:

### 1.1 Cambiamos Nombre de host

    Hostname Configuration

    Enter the new hostname: |localhost| cloudforms.poc.redhat.com
    Applying new hostname...

    Press any key to continue.

### 1.2  Cambiamos a ip estatica

    Static Network Configuration.
    Enter the new static network configuration settings.
    Enter the IP Address: |192.168.122.176| 
    Enter the Netmask: |255.255.255.0| 
    Enter the Gateway: |192.168.122.1| 
    Enter the Primary DNS: |192.168.122.1| 
    Enter the Secondary DNS (Enter 'none' for no value): 
    Enter the Domain search order: || poc.redhat.com

-------

    Static Network Configuration

      IP Address:      192.168.122.176
      Netmask:         255.255.255.0
      Gateway:         192.168.122.1
      Primary DNS:     192.168.122.1
      Secondary DNS:   
      Search Order:    poc.redhat.com

    Apply static network configuration? (Y/N)
    Y
    
--------

    Applying static network configuration...
    After completing the appliance configuration, please restart CFME server
    processes.

    Press any key to continue.


### 1.3 Cambiamos la Zona Horaria

    Set Timezone

    Geographic Location

    1) United States
    2) Canada
    3) Africa
    4) America
    5) Asia
    6) Atlantic Ocean
    7) Australia
    8) Europe
    9) Indian Ocean
    10) Pacific Ocean
    11) Cancel
  
---------- 

    Choose the geographic location: |4|
    (...)
    83) Mendoza
    84) Menominee
    85) Merida
    86) Metlakatla
    87) Mexico_City
    88) Miquelon
    89) Moncton
    90) Monterrey
    91) Montevideo
    92) Montreal
    93) Montserrat
    (...)
  
----------

    Timezone Configuration

        Timezone area: America
        Timezone city: Mexico_City
        
    Apply timezone configuration? (Y/N):  
    
----------    

    Activate starting
    Applying timezone to America/Mexico_City...
    Activate complete
    Timezone configured
    
    Press any key to continue.
### 1.4 Acontinuación configuraremos la hora y fecha 

    Set Date and Time

    Automatic time synchronization must be disabled to manually set date or time
    Yes to disable Automatic time synchronization and prompt for date and time.
    No to enable  Automatic time synchronization.  (Y/N):
    Y

      Enter the current date (YYYY-MM-DD): 2016-06-11
      Enter the current time in 24 hour format (HH:MM:SS): 14:38:00 
      
---------

    Date and Time Configuration

      Date: 2016-06-11
      Time: 14:39:30

    Apply manual time configuration? (Y/N): Y
    Applying time configuration...
    Date and time configured
    Press any key to continue.



### 1.5 Acontinuación continuaremos con la configuración de la DB 

    Configure Database

    No encryption key found.
    For migrations, copy encryption key from a hardened appliance.
    For worker and multi-region setups, copy key from another appliance.
    If this is your first appliance, just generate one now.

    Encryption Key

    1) Create key
    2) Fetch key from remote machine

    Choose the encryption key: |1|
  
--------- 

    Encryption key now configured.

    Database Location

    1) Internal
    2) External

    Choose the database location: 1
    database disk

    1) /dev/vdb: 102400 MB
    2) Don't partition the disk

    Choose the database disk: |1|
----------------

    Setup Database Region
    Each database region number must be unique.
    Enter the database region number:01
----------------

    Enter the database password on 127.0.0.1: ******
    Enter the database password again: ******
-----------------

    Activating the configuration using the following settings...
    Host:     127.0.0.1
    Username: root
    Database: vmdb_production
    Region:   1

    Initialize postgresql disk starting
    Initialize postgresql disk complete
    Initialize postgresql starting
    Initialize postgresql complete
    Create region starting

    Create region complete

    Configuration activated successfully.

    Press any key to continue.


### 1.6 Configurando autenticacion vía IPA

    Configure External Authentication (httpd)

    IPA Server Parameters:

    Enter the IPA Server Hostname: idm.poc.redhat.com
    Enter the IPA Server Domain: poc.redhat.com
    Enter the IPA Server Realm: |POC.REDHAT.COM| 
    Enter the IPA Server Principal: |admin| 
    Enter the IPA Server Principal Password: **********

    External Authentication (httpd) Configuration:
    IPA Server Details:
      Hostname:       idm.poc.redhat.com
      Domain:         poc.redhat.com
      Realm:          POC.REDHAT.COM
      Naming Context: dc=poc,dc=redhat,dc=com
      Principal:      admin

    Proceed? (Y/N): Y

----------

    Checking connectivity to idm.poc.redhat.com ... Succeeded.

    Configuring IPA (may take a minute) ...
    Configuring the IPA Client ...
    Configuring pam ...
    Configuring sssd ...
    Configuring IPA HTTP Service and Keytab ...
    Configuring httpd ...
    Configuring SELinux ...

    Restarting sssd and httpd ...
    Configuring sssd to start upon reboots ...

    External Authentication configured successfully.

    Press any key to continue.

----------------

    Welcome to the CFME Virtual Appliance.

    To modify the configuration, use a web browser to access the management page.

    Hostname:                  cloudforms.poc.redhat.com
    IP Address:                192.168.122.176          
    Netmask:                   255.255.255.0            
    Gateway:                   192.168.122.1            
    Primary DNS:               192.168.122.10           
    Secondary DNS:             192.168.122.1            
    Search Order:              poc.redhat.com           
    MAC Address:               52:54:00:33:fb:bc        
    Timezone:                  America/Mexico_City      
    Local Database:            running                  
    CFME Database:             postgresql @ localhost   
    Database/Region:           vmdb_production / 1      
    External Auth:             idm.poc.redhat.com       
    CFME Version:              5.5.4.2                  
    CFME Console:              https://192.168.122.176  

    Press any key to continue.

-------------------



















