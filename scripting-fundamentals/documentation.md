Un script sirve para automatizar tareas repetitivas. Se pueden crear con múltiples lenguajes de programacion pero también se pueden crear con el bash. En este ejemplo se creará con el BASH Shell por defecto en las distribuciones linux.

1. Tenemos que crear un archivo con la extensión `.sh` que es la extensión por defecto para los bash scripts.

```bash
nano first_script.sh
```

1. Todo script debe empezar con Shebang. Es una combinación de caracteres que se añaden al principio del script y empiezan por `#!` seguido del nombre del interprete a usar para ejecutar el script. Al abrir con nano el archivo añadimos al principio:

```bash
#!/bin/bash
```

1. VARIABLES. Una variable almacena un valor dentro. Entonces vamos a hacer una pregunta con `echo` despues el comando `read name` almacenará en name el input que ingrese el usuario y posteriormente escribirá el saludo con echo + nombre introducido de la siguiente manera:

```bash
# Defining the Interpreter 
#!/bin/bash
echo "Hey, what’s your name?"
read name
echo "Welcome, $name"
```

1. Despues guardamos el script pulsando CTRL + X, Confirmamos con Y y pulsamos ENTER. Para ejecutar el script primero tenemos que darle permisos de ejecución. Para ello ingresamos lo siguiente

```bash
chmod +x first_script.sh
```

1. Para ejecutar un script añadimos delante del nombre `./` y luego el nombre del archivo.

```bash
./first_script.sh

Hey, what's your name?
Victor
Welcome, Victor
```

1. BUCLES. Para repetir acciones. Haremos otro script para aplicar los bucles. Primero creamos el archivo como en el caso anterior y escribimos la cabecera del interprete y luego vamos a hacer un código para enviar un mensaje a una lista de amigos.

```bash
# Defining the Interpreter 
#!/bin/bash
for i in {1..10};
do
echo $i
done
```

En este caso, `do` indica el inicio del bucle y `done` el final. En medio va lo que hará el bucle que en este caso es imprimir el valor de `i` en cada iteración.

1. Si ejecutamos el script obtendremos lo siguiente:

```bash
user@tryhackme:~$ ./loop_script.sh 
1
2
3
4
5
6
7
8
9
10
```

1. Otro script con CONDICIONALES. Te permiten ejecutar partes del código si cumplen cierta condición.  Vamos a crear otro script diferente para este caso:

```bash
nano conditional_script.sh
```

1. El script tendrá el siguiente contenido:

```bash
#!/bin/bash
echo "Please enter your name first:"
read name
if [ "$name" = "Victor" ]; then
        echo "Welcome Victor! Here is the secret: (O_o)"
else
        echo "Sorry! You are not authorized to access the secret."
fi
```

1. Pongamos todo esto en practica para un nuevo script que ha de comprobar si un usuario puede acceder a su caja de un banco. El usuario tendrá que añadir su nombre, el nombre de su compañia y su código pin. 

```bash
# Defining the Interpreter 
#!/bin/bash 

# Defining the variables
username=""
companyname=""
pin=""

# Defining the loop
for i in {1..3}; do
# Defining the conditional statements
        if [ "$i" -eq 1 ]; then
                echo "Enter your Username:"
                read username
        elif [ "$i" -eq 2 ]; then
                echo "Enter your Company name:"
                read companyname
        else
                echo "Enter your PIN:"
                read pin
        fi
done

# Checking if the user entered the correct details
if [ "$username" = "Victor" ] && [ "$companyname" = "Tryhackme" ] && [ "$pin" = "8701" ]; then
        echo "Authentication Successful. You can now access your locker, John."
else
        echo "Authentication Denied!!"
fi
```

