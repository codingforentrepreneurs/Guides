Kill your Local Server (Localhost)
================

Sometimes your server hangs and you see errors. This is a simple guide to help you eliminate those errors.

## For Mac

Have you seen the following error:

```
Error: That port is already in use.
```

If so, this is how you would kill the server that's running.

```
$ lsof -i :8000
```

`8000` is the port. So, if your using django and you run `python manage.py runserver` it's likely your port will be "8000" 

That command will yield something like:
```
COMMAND  PID   USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
python  1158 jmitch    3u  IPv4 0x4ae303085ae91559      0t0  TCP localhost:irdmi (LISTEN)
```

Except under "jmitch" it would have your username. Do you see the value under "PID" this is the number you need. Now you just kill that process.

```
$ kill -9 1158
```

Let's do that one more time:

```
$ lsof -i :8000

COMMAND  PID   USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
python  4894 jmitch    3u  IPv4 0x4ae3030864c1dd41      0t0  TCP localhost:irdmi (LISTEN)

$ kill -9 4894

```

And that's it. You can kill this server without an error running.

Alternatively we can use the `fg` command in linux, which brings our processes to the foreground, and than press `ctrl + c` to quit the server.
For more help on fg use :

```
$ help fg
```

Please share questions/comments! (We're always looking for better ways to improve).

Cheers!

-CodingForEntrepreneurs.com




