# GPG
GNU Privacy Guard

## Cifrado simétrico
Es el cifrado más sencillo que ofrece **gpg**, solicitando una contraseña al cifrar un archivo. Es el método menos seguro.
```bash
#cifrar fichero
gpg -c mensaje.txt

#descifrar fichero
gpg -d mensaje.txt.gpg
```

## Cifrado asimétrico
En este tipo de cifrado crearemos el par de claves (pública y privada) junto con la firma para cifrar y descifrar los ficheros que queramos.

### Generar una clave
```bash
#Generar el par de claves con las opciones por defecto
gpg --gen-key
```
