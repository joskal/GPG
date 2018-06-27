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

### Generar una clave
```bash
#Generar el par de claves con las opciones por defecto
gpg --generate-key
#idem al anterior
gpg --gen-key

#Generar el par de claves estableciendo todas las opciones por nosotros
gpg --full-generate-key
#idem al anterior
gpg --full-gen-key
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
#exportar la clave pública de Juan Garcia a un fichero llamado juan_public.key 
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
