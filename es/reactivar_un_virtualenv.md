# Reactivar un Entorno Virtual (virtualenv)
Si has cerrado tu terminal (Linux/Mac) o Simbolo de Sistema (Windows) y no sabes como regresar a trabajar a tu proyecto, checa esta guía de como reactivar tu entorno virtual (virtualenv).


## Asumiendo que has seguido los pasos de los [videos de instalación](https://codingforentrepreneurs.com/projects/#setup)... 

Deberías ir a tu escritorio y después al directorio con tu virtualenv

En la Terminal de Mac/Linux:
```
Last login: Thu Jul  3 17:34:42 on ttys000
$ pwd
/Users/yourusername 
$ cd Desktop
$ ls
$ otherfolders otherfiles.png venv
$ cd venv 
```


En el Simbolo de Sistema de Windows:
```
> dir
\User\yourusername
> cd Desktop
> cd venv
```

*venv hace referencia al nombre de tu entorno virtual*


Con lo anterior ya estarías en tu *venv* entorno virtual. ahora para reactivarlo solo tecleamos:

En la Terminal de Mac/Linux:
```
$ source bin/activate
```

En el Simbolo de Sistema de Windows:
```
> .\Scripts\activate
```


## Si no seguiste los  [videos de instalación](https://codingforentrepreneurs.com/projects/#setup)...

Primero necesitas encontrar el directorio donde está ubicado tu entorno virtual, una vez que lo encontraste, ingresa a tu directorio usando algo como esto:

```
$ cd ~/path/to/your/virtualenv/
```
or
```
> cd \path\to\your\virtualenv\
```

una vez dentro, puedes reactivar tu entorno virtual como lo vimos arriba.

Saludos!


#### Organizado por CodingForEntrepreneurs