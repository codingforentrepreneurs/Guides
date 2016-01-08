# Instalar Django & Virtualenv con PIP en Windows

- **Pip** (Administrador de paquetes, en ingles 'Python Package Installer')  nos permite instalar todos tipo de software y código escritos en Python, como por ejemplo Virtual environments (virtualenv), Python Requests y mucho más.
- **Django** es un framework de desarrollo web de código abierto, escrito en Python
- **Virtualenv** es una herramienta de desarrollo en Python usada para crear entornos aislados para Python, en los que es posible instalar paquetes sin interferir con otros virtualenvs (basicamente, es aconsejable mantener separados los requisitos de tus proyectos diferentes porque es importante saber que versiones distintas de software no siempre "se llevan bien" entre sí).  


### Videos de configuración (en inglés):

[JoinCFE.com](https://codingforentrepreneurs.com/projects/#setup)
[YouTube](https://www.youtube.com/user/CodingEntrepreneurs/playlists?shelf_id=7&view=50&sort=dd)


### Descargar Python

1. Lo descargamos según nuestro sistema operativo (32 ó 64-bit)
    1. Para nuestros tutoriales la versión ideal de Python es 2.7 ya que muchos paquetes tanto de Python como de Django siguen siendo escritos en 2.7. Descargar [aqui](https://www.python.org/downloads/release/python-278/).

2. Ejecutamos la instalación estándar

3. 1.   Ya tenemos instalado Python, pero para que podamos utilizarlo dentro de 'Símbolo de sistema' (el intérprete de comandos, en inglés 'command prompt') tenemos que definir la ruta y lo hacemos de la siguiente manera(para Windows XP, 7, 8 y 10):
    1. Abrir Panel de control
    2. Seleccionar Sistema y seguridad  
    3. Seleccionar Sistema 
    4. Seleccionar Configuración avanzada del sistema
    5. En la pestaña 'Opciones avanzadas' seleccionar 'Variables de entorno'
    6. En 'Variables de usuario para' seleccionar la variable 'Path' y seleccionar 'edit'
    7. Si no existe la variable 'Path', seleccionar 'Nueva' y definir el nombre como 'PATH' y el valor así:
        ```
        C:\Python27;C:\Python27\python.exe;C:Python\27\Lib\site-packages;C;\Python27\Lib\site-packages\django\bin;c:\Python27\Scripts;
        ```

        Pero si ya existe la variable PATH y tiene algo escrito en la casilla que pone 'valor',  añades simplemente la ruta de arriba después de lo que ya está escrito en la casilla para el valor. El resultado final será parecido a esto:

        ```
        C:\Windows\System32;C:\Python27;C:\Python27\python.exe;C:Python\27\Lib\site-packages;C;\Python27\Lib\site-packages\django\bin\;c:\Python27\Scripts;
        ```



4. Abre el 'Símbolo de sistema' en una ventana nueva. Para asegurar que se ha instalado correctamente y que la ruta está bien definida hay que escribir 'python'. Si nos devuelve lo siguiente:

    ```
    Python 2.7.8 (default, Nov 13 2014, 13:18:45)
    >>> 
    ``` 

    Python se ha instalado correctamente. Ya puedes salir de Python con el siguiente comando:

    ```
    >>> exit()
    ```

### Instalar Pip

1. 1.   Guarda el archivo "get-pip.py" en el escritorio de tu ordenador. Lo puedes encontrar aquí (Debajo del título 'Install Pip', haz clic el archivo con el botón derecho y selecciona 'guardar enlace como...'). Descargar [aqui](http://pip.readthedocs.org/en/latest/installing.html)


2. Abre el 'Símbolo de sistema' y escribe:
    ```
    > cd Desktop
    > python get-pip.py
    ```

3. Ya está! Ahora puedes instalar virturalenv y Django usando Pip:
    ```
    > pip install virtualenv
    > pip freeze
    > pip install Django==1.8.2
    ```

* << pip freeze >> es un comando que nos permite ver todo lo que tenemos instalado 




### Has tenido problemas con las instalaciones? Sigue leyendo.


- Si no consigues empezar un virtualenv nuevo o simplemente no entiendes bien su función no pasa nada si de momento trabajas fuera de él. Pero si eso, es importante tomar en cuenta que versiones distintas de software no siempre "se llevan bien" con otras y que es muy recomendable volver a hacer la instalación cuando ya manejes mejor Django.
- Puede que el problema se resuelva abriendo una ventana nueva del 'Símbolo de sistema'
- No consigues instalar Pip? Intentemos usando las herramientas de configuración:



Suponemos que Python verisón 2.7 se ha instalado con éxito. Pero para probar, recuerda que puedes abrir el 'Símbolo de sistema' y escribir lo siguiente:
    ```
    > python	 
    >>> exit() 
    ```

Si puedes hacer esto, Python se ha instalado correctamente. Ahora a lo que íbamos:
1.  Guarda el archivo "ez_setup.py" en tu escritorio. Descargar ["ez_setup.py" aqui](https://bootstrap.pypa.io/ez_setup.py)
2.  Abre el 'Símbolo de sistema' y escribe lo siguiente:
    ```
    > cd Desktop
    > python ez_setup.py
    > easy_install pip
    ```

3. Ahora Pip debe de estar funcionando en tu ordenador. Estos comandos funcionarán:
    ```
    > pip install virtualenv
    > pip freeze
    > pip install Django==1.8.6
    ```


Ya está! Estás listo para empezar a utilizar Python Packages como Django.

Saludos.


#### Organized by TeamCFE