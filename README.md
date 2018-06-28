# GPG
GNU Privacy Guard

## Cifrado simétrico
Es el cifrado más sencillo que ofrece **gpg**, solicitando una contraseña al cifrar un archivo. Es el método menos seguro.
```bash
#cifrar fichero
gpg -c mensaje.txt
#idem al anterior
gpg --symmetric mensaje.txt

#descifrar fichero
gpg -d mensaje.txt.gpg
#idem
gpg --decrypt mensaje.txt.gpg
```

## Cifrado asimétrico
En este tipo de cifrado crearemos el par de claves (pública y privada) junto con la firma para cifrar y descifrar los ficheros que queramos.

### Generar claves
```bash
# --generate-key          generate a new key pair
# --full-generate-key     full featured key pair generation

#Generar el par de claves con las opciones por defecto
gpg --generate-key

#Generar el par de claves estableciendo todas las opciones por nosotros
gpg --full-generate-key
```
### Importar claves
```bash
#importar una clave pública
gpg --import joskalpublic.key

#importar una clave privada
gpg --allow-secret-key-import --import joskalprivate.key
```
### Exportar claves
```bash
# --export                export keys

#exportar la clave pública de Juan Garcia a un fichero llamado juan_public.key
# --export                export keys
# -a, --armor                 create ascii armored output
gpg --export -a "Juan Garcia" > juan_public.key

#exportar la clave privada de Juan Garcia a un fichero llamado juan_private.key
gpg --export-secret-key -a "Juan Garcia" > juan_private.key
```

### Listar claves
```bash
#listar claves privadas
gpg --list-secret-keys

#listar claves públicas
gpg --list-keys
```

### Eliminar claves
```bash
# --delete-keys           remove keys from the public keyring
# --delete-secret-keys    remove keys from the secret keyring
#eliminar una clave privada
gpg --delete-secret-key "Nombre de Usuario"

#eliminar una clave pública.
#si existe una clave privada asociada a la clave pública que
#queremos eliminar debemos borrar antes la primera.
gpg --delete-key "Nombre de Usuario"
```

### Encriptar y desencriptar ficheros
```bash
#encriptar un fichero con la clave pública del destinatario
# -e, --encrypt               encrypt data
# -r, --recipient USER-ID     encrypt for USER-ID
gpg -e -r "USER-ID" nombre_fichero

#encriptar un fichero con la clave pública del destinatario y firmarlo con nuestra clave privada
# -u, --local-user USER-ID    use USER-ID to sign or decrypt
gpg -e -u "Sender User Name" -r "Receiver User Name" nombre_fichero

#desencriptar un fichero con clave pública
#al hacerlo, gpg selecciona automáticamente la clave privada
# -d, --decrypt               decrypt data (default)
# -o, --output FILE           write output to FILE
gpg -o nombrefichero.ext -d nombre_fichero.gpg
```

### Firmas
Siempre que firmemos un archivo lo haremos con una clave privada.
```bash
#firmar el fichero einstein.txt con nuestra clave privada
#fichero de salida: einstein.txt.gpg
# -s, --sign                  make a signature
gpg --sign einstein.txt

#firmar einstein.txt en un formato legible
#fichero de salida: einstein.sig
# --clear-sign            make a clear text signature
gpg -o einstein.sig --clear-sign einstein.txt
```

Una firma acompañante es aquella que va unida intrínsecamente al fichero que se pretende autentificar.
A la hora de verificarla se ha de hacerlo junto con el fichero que lo acompaña.
```bash
# Encriptar el fichero einstein.txt y Crear una firma acompañante
# del fichero ya encriptado con la clave privada de joskal
# -b, --detach-sign           make a detached signature
gpg -e einstein.txt
gpg -u joskal -o einstein.sig --detach-sign einstein.txt.gpg

# verificar el fichero de firma (ha de hacerse junto con el fichero que lo acompaña)
gpg --verify einstein.sig einstein.txt.gpg
```
