# Comandos de ssh

## Comandos básicos de ssh

- Conectarte a un servidor utilizando ssh, nos pedira contraseña del servidor

    $ ssh <user>@<ip-servidor>

- Generar una key ssh para conectarse a un servidor sin contraseña

    $ ssh-keygen -t rsa -b 4096 -C "tu@email.com"

- Copiar la key publica de ssh al servidor, pegando el contenido de la key en el archivo .ssh/authorized_keys del servidor al que nos queremos conectar.

    $ sudo vim .ssh/authorized_keys

- Otra opción que podemos utilizar para copiar la key publica al servidor, nos pedira contraseña del servidor

    $ ssh-copy-id <user>@<ip-servidor>

- Utilizar ssh como un proxy SOCKS

    $ ssh -D <puerto> <user>@<ip-servidor>

- Conectarse al servidor utilizando una interfaz grafica, para mac y windows se puede utilizar XQuartz.app

    $ ssh -X <user>@<ip-servidor>



