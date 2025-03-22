# cron DAEMON
`cron` is a  daemon to execute scheduled commands

## Checking whether `cron` is running

Since `cron` is started automatically from /etc/init.d it must be running so you can check as following

```bash 
$ systemctl status cron
```

The output must show:

> $ systemctl status cron\
> $${\color{lightgreen}●}$$ cron.service - Regular background program processing daemon\
>    Loaded: loaded (/usr/lib/systemd/system/cron.service; $${\color{green}enabled}$$; preset: $${\color{green}enabled}$$)\
>    Active: $${\color{green}active (running)}$$ since Fri 2025-03-21 23:12:25 CST; 48min ago

- The following directories must exist in **`/etc`** directory:

```
/etc/cron.hourly
/etc/cron.daily
/etc/cron.weekly
/etc/cron.monthly
```
Los directorios anteriores están predefinidos para correr los scripts en el periodo de tiempo indicado por su nombre
> Es importante hacer notar que los nombres de scripts **no deben llevan extensión** de lo contrario no se ejecutarán

En el archivo `/etc/crontab` está definido el tiempo para cada una de las carpetas anteriores

## Personalizar el tiempo de ejecución con ***`crontab`***

Existen dos modos:
- crontab -e
- sudo crontab -e

Con el primer comando se edita o se crea el crontab en el ámbito del usuario actual.\
Con el segundo comando se edita o se crea el crontab para el usuario root.

Ambos modos crean un archivo en donde la última línea se deberá especificar el tiempo

    # m h dom mon dow coomand

En donde:
- m --> minuto
- h --> hora
- dom --> day of month
- mon --> month
- dow --> day of week
- command --> comando o script a ejecutar en el tiempo indicado

Un `*` en los campos anteriores indica "cualquiera"

Para mayor información visitr la página web [crontab guru][guru]

[guru]: https://crontab.guru
