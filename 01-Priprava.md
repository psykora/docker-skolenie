# Príprava a prvé príkazy

## Prerequisites

* Ubuntu 22.04 (Jammy)

## Inštalácia dockera

```sh
apt-get update
apt-get upgrade
apt install docker.io docker-compose
```

## Vytvorenie nového uživateľa

```sh
root@prvy:~# adduser petos
Adding user `petos' ...
Adding new group `petos' (1000) ...
Adding new user `petos' (1000) with group `petos' ...
Creating home directory `/home/petos' ...
Copying files from `/etc/skel' ...
New password:
Retype new password:
passwd: password updated successfully
Changing the user information for petos
Enter the new value, or press ENTER for the default
        Full Name []: Peter
        Room Number []:
        Work Phone []:
        Home Phone []:
        Other []:
Is the information correct? [Y/n] Y
```

Pridanie do skupiny docker a sudo

```sh
root@prvy:~# usermod petos -a -G docker,sudo
```

## Spustenie prvého kontainera
```sh
docker run hello-world
```

## Zoznam bežiacich kontainerov

```sh
petos@prvy:~$ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

## Zoznam všetkých kontainerov

```bash
petos@prvy:~$ docker container ls --all
# alebo -> petos@prvy:~$ docker ps --all
CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                      PORTS     NAMES
d13d5c157b81   hello-world   "/hello"   47 minutes ago   Exited (0) 47 minutes ago             nice_feistel

```

## Zoznam obrazov

```sh
petos@prvy:~$ docker image ls
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    feb5d9fea6a5   13 months ago   13.3kB
```

## Odstránenie kontainera

```sh
petos@prvy:~$ docker rm nice_feistel
nice_feistel
```

alebo (**POZOR**) odstránenie všetkých stopnutých kontainerov

```sh
petos@prvy:~$ docker container prune
WARNING! This will remove all stopped containers.
Are you sure you want to continue? [y/N]
```

## Odstránenie image

Ako si môžeme všimnúť image nebol zmazaný
```sh
petos@prvy:~$ docker image ls
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    feb5d9fea6a5   13 months ago   13.3kB
```
```sh
petos@prvy:~$ docker image rm hello-world:latest
Untagged: hello-world:latest
Untagged: hello-world@sha256:faa03e786c97f07ef34423fccceeec2398ec8a5759259f94d99078f264e9d7af
Deleted: sha256:feb5d9fea6a5e9606aa995e879d862b825965ba48de054caab5ef356dc6b3412
Deleted: sha256:e07ee1baac5fae6a26f30cabfe54a36d3402f96afda318fe0a96cec4ca393359
```
