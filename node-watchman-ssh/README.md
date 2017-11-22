# node-watchman-ssh

See [debian-ssh](https://github.com/krlmlr/debian-ssh) to learn how to open the ssh server.

- build image
```sh
docker run -t server .
```

- run container
```sh
docker run -d \
  --rm --name server \
  -p 22:22 \
  -e SSH_KEY="$(cat ~/.ssh/id_rsa.pub)" \
  server
```
