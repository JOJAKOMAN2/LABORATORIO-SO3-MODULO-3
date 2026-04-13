# LABORATORIO-SO3-MODULO-3
MODULO 3

# =========================
# PRACTICA 1 - GRUB + ROOT
# =========================

# Editar GRUB para cambiar tiempo a 20 segundos
sudo nano /etc/default/grub

# Cambiar o agregar esta línea:
GRUB_TIMEOUT=20

# Guardar y actualizar GRUB
sudo update-grub

# Mostrar resultado
cat /etc/default/grub | grep GRUB_TIMEOUT


# =========================
# METODO RECUPERAR PASSWORD ROOT
# =========================

# (Esto es procedimiento en GRUB, no comando directo)

# 1. Reiniciar
sudo reboot

# 2. En GRUB presionar 'e'
# 3. Buscar linea que contiene: linux /boot/vmlinuz...
# 4. Al final agregar:
rw init=/bin/bash

# 5. Presionar Ctrl + X

# 6. Cambiar contraseña root
passwd root

# 7. Reiniciar
exec /sbin/init


# =========================
# PRACTICA 2 - SCRIPTS
# =========================

# -------- SCRIPT BACKUP --------
nano backup.sh

# Contenido:
#!/bin/bash
fecha=$(date +"%d-%m-%Y:%H:%M")
tar -czvf backup_$fecha.tar.gz /home/$USER

# Guardar y dar permisos
chmod +x backup.sh

# Ejecutar
./backup.sh


# -------- SCRIPT IFCONFIG --------
nano red.sh

# Contenido:
#!/bin/bash
echo "Ingrese el nombre del archivo:"
read nombre
ifconfig > ~/Escritorio/$nombre.txt

# Guardar y permisos
chmod +x red.sh

# Ejecutar
./red.sh


# =========================
# PRACTICA 3 - RED + SSH
# =========================

# (CONFIGURAR BRIDGE SE HACE EN LA VM - VIRTUALBOX/VMWARE)
# Cambiar adaptador de NAT a BRIDGE

# Verificar IP
ip a

# Desde Windows (CMD o PowerShell)
# ping IP_DE_TU_VM


# -------- INSTALAR Y ACTIVAR SSH --------
sudo apt update
sudo apt install openssh-server -y

# Activar servicio
sudo systemctl enable ssh
sudo systemctl start ssh

# Verificar
sudo systemctl status ssh


# =========================
# DESDE WINDOWS (HOST)
# =========================

# Generar llaves (PowerShell)
ssh-keygen

# (Presionar ENTER todo, dejar passphrase vacio)

# Copiar llave publica al servidor
ssh-copy-id usuario@IP_DE_TU_VM

# Conectarse (ya sin contraseña)
ssh usuario@IP_DE_TU_VM
