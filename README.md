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
