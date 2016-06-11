# configuración inicial APPLIANCE en KVM

### 1.-  Login RHEV-M
### 2.- Dentro de Export Domain
### 3.- Copiar appiance de CF
### 4.- Extraer contenido de CF.ova
$ tar xvf cfme-rhevm-5.3-15.x86_64.rhevm.ova
### 5.- Cambiar los permisos
chown -R 36:36 images/
chown -R 36:36 master/
