# 主要用于国内办公室与海外阿里云内网互通


## Update on 2018.12

## Update on July 20,2016

You can login with two group (`Route`/`ALL`) from now on.

## How to use this image

Get the docker image by running the following commands:

```bash
docker pull img/ocserv
```

Start an ocserv instance:

```bash
docker run --name ocserv --privileged -p 443:443 -p 443:443/udp -d tommylau/ocserv
```

### Environment Variables

All the variables to this image is optional, which means you don't have to type in any environment variables, and you can have a OpenConnect Server out of the box! However, if you like to config the ocserv the way you like it, here's what you wanna know.

`CA_CN`, this is the common name used to generate the CA(Certificate Authority).

`CA_ORG`, this is the organization name used to generate the CA.

`CA_DAYS`, this is the expiration days used to generate the CA.

`SRV_CN`, this is the common name used to generate the server certification.

`SRV_ORG`, this is the organization name used to generate the server certification.

`SRV_DAYS`, this is the expiration days used to generate the server certification.

`NO_TEST_USER`, while this variable is set to not empty, the `test` user will not be created. You have to create your own user with password. The default value is to create `test` user with password `test`.

### Running examples

```bash
docker run --name ocserv --privileged -p 443:443 -p 443:443/udp -d img/ocserv
```

### User operations

All the users opertaions happened while the container is running. If you used a different container name other than `ocserv`, then you have to change the container name accordingly.

#### Add user

If say, you want to create a user named `username`, type the following command

```bash
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -g "Route,All" username
Enter password:
Re-enter password:
```

When prompt for password, type the password twice, then you will have the user with the password you want.

>`-g "Route,ALL"` means add user `username` to group `Route` and group `All`

#### Delete user

Delete user is similar to add user, just add another argument `-d` to the command line

```bash
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -d test
```

The above command will delete the default user `test`, if you start the instance without using environment variable `NO_TEST_USER`.

#### Change password

Change password is exactly the same command as add user, please refer to the command mentioned above.
