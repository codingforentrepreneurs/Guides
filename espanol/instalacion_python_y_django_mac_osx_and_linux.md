# Instalar Django & Virtualenv con PIP en Mac OS  / Linux 

- **Pip** (Administrador de paquetes, en ingles 'Python Package Installer')  nos permite instalar todos tipo de software y código escritos en Python, como por ejemplo Virtual environments (virtualenv), Python Requests y mucho más.
- **Django** es un framework de desarrollo web de código abierto, escrito en Python
- **Virtualenv** es una herramienta de desarrollo en Python usada para crear entornos aislados para Python, en los que es posible instalar paquetes sin interferir con otros virtualenvs (basicamente, es aconsejable mantener separados los requisitos de tus proyectos diferentes porque es importante saber que versiones distintas de software no siempre "se llevan bien" entre sí).  


## Videos de configuración (en inglés):

[JoinCFE.com](https://codingforentrepreneurs.com/projects/start-with-windows/)

### Instalar Pip

Cuando ves este código:
```
ls
```

significa que debes escribir dentro de la aplicación que mencionamos abajo. (De todas maneras, recomendamos que veas estos videos gratuitos de configuración para que sea más fácil)

1.  Abre 'Terminal' (Aplicaciones > Utilidades*> Terminal)

2.  Escribe los siguientes comandos en el Terminal: (el comando 'sudo' requiere contraseña de administrador del ordenador. Es la misma contraseña que introduces para instalar otros programas en tu sistema)

    1. Instalar Pip
    ```
    sudo easy_install pip
    ```
    2. Instalar virtualenv
    ```
    sudo pip install virtualenv
    ```
    3. Navegar (dentro del Terminal) adónde quieres dejar tu código. Tienes dos opciones
        1. Opción fácil (en el escritorio)
        ```
        cd ~/Desktop

        ```
        2. Opción más específica (saltas la opción de arriba)
        ```
        mkdir Development
        cd Development
        ```

        Lo tradicional es guardar tu código dentro de la carpeta llamada "Development" para tener todo en un mismo directorio.

        NOTA: También se puede utilizar 'Dropbox' o 'Google Drive' para almacenar tu código. Si eliges utilizar servicios como estos, tu código será sincronizado pero siempre existe la posibilidad de que virtualenv no funcione correctamente en otros ordenadores. 

    4. Crear un virtualenv nuevo
    ```
    virtualenv yourenv
    ```
    *el nombre 'yourenv' es un ejemplo. Dale el nombre que quieras

    5. Activar el virtualenv
    ```
    source bin/activate
    ```
    El resultado en 'Terminal' debe de ser algo parecido a:

        ```
        (yourenv) Justins-iMac-2:~ jmitch$
        ```
        *pero con el nombre de usuario/administrador del ordenador


    6. Instalar Django
    ```
    pip install django
    ```
    *pip install django instalará la última versión disponible de Django. Si necesitas versiones anteriores hay que escribir: pip install django==1.8.6 (por ejemplo)


Ya está! 

Saludos.




#### Organized by TeamCFE