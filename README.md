```
    ____             __      ___        ____             __  
   / __ \____  _____/ /__   ( _ )      / __ \____  _____/ /__
  / / / / __ \/ ___/ //_/  / __ \/|   / / / / __ \/ ___/ //_/
 / /_/ / /_/ / /__/ ,<    / /_/  <   / /_/ / /_/ / /__/ ,<
/_____/\____/\___/_/|_|   \____/\/  /_____/\____/\___/_/|_|  
```

# DockNode & DockNginx

**Why this project ?**  
_Just for create and deploy quickly my project and experience on NodeJS & Nginx environment thanks to `Dockerfile`_

---

## Install Image thanks to `Dockerfile`

After we have clone the repository, you should go to the folder. If you want change configuration of your server or your VPS, you can into the file `default` before construct your image.  
After that, you will execute the commands below:

```bash
#Launch command for install all the packages
$ docker build -t <NAME_IMAGE> <PATH_DOCKERFILE>

#Example
$ docker build -t env/node .
```

**Some parameters**

| Parameter       | Character | Description                            |
| --------------- | --------- | -------------------------------------- |
| NAME_IMAGE      | Mandatory | The name of your futur image           |
| PATH_DOCKERFILE | Mandatory | The path who contains the `Dockerfile` |

_Well, your picture is ready. Now we can get down to business and launch our container_

&nbsp;

## Launch the container

Basically, it's very easy to launch container with Docker, only some lines and your environment is mounted. The evidence:

```bash
#Launch basis container
$ docker container run -p 80:80 -it <NAME_IMAGE> /bin/bash

#Or if you are on Windows, you should go to the folder
#that you want share between the container and the host
$ docker container run -p 80:80 -it -v "/$(pwd)":/var/www/html <NAME_IMAGE>

#TIPS: You can give a name to your container
$ docker container run -p 80:80 --name=enjoy -it <NAME_IMAGE>
```

**WARNING:** the folder `/var/www/html` should be conserve. Only your local folder can be modify.

&nbsp;

> ### **We are Genius !**
>
> _But I want the picture with the example..._

&nbsp;

### NodeJS Container

Ok, let's go, launch the container for NodeJS Environment

```bash
#NodeJS Environment
#Mount your work folder with argument -v
$ docker container run -p 80:80 -it -v /path/of/host:/var/www/html <NAME_IMAGE>
```

### Nginx Container

Now, same pain, launch the container for Nginx Environment

```bash
#Nginx Environment
#Mount your work folder with argument -v and open the port of your MySql
$ docker container run -p 80:80 -p 3306:3306 -it -v /path/of/host:/var/www/html <NAME_IMAGE>
```

&nbsp;

## Prerequisites & utils:

* [**Folder structure**](#folder-structure)
* [**Packages list NodeJS**](#packages-list-nodejs)
* [**Packages List Nginx**](#packages-list-nginx)

---

### Folder Structure

```
.
├── node
│   ├── www
│       └── ...
│   ├── Dockerfile
│   └── default
├── nginx
│   ├── www
│       └── ...
│   ├── Dockerfile
│   └── default
└── README.md
```

### Packages List NodeJS

_Coming soon, MangoDB, i hope !_

* Nginx
* PM2
* NodeJS _v.9.3.0_
* NPM _v.5.5.1_

### Packages List Nginx

* Nginx
* MySql _v.5.5_
* PHP _v.7.0_

&nbsp;

## Tips _aware_

### Options `-d` Docker Container

**This argument detach your container**

```bash
#Launch container with -d
$ docker container run -dit --name=hello nodejs
```

If you want rattach your container and enter commands, follow this command

```bash
#Attach the terminal on the container who call hello
$ docker container attach hello
```

Again in the _Matrix_ and you want to re-detach ?  
**Tips:** `Ctrl`+`p`+`Ctrl`+`q`
