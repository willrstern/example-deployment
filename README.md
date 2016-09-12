# Continuous Deployment with SemaphoreCI

### Create an SSH key
```
ssh-keygen -C semaphore
```
- save it as ~/.ssh/id_rsa.semaphore
- don't give it a password

### Setup your server
- paste the contents of your `~/.ssh/id_rsa.semaphore.pub` to your server's `~/.ssh/authorized_keys` file:
- on your machine:
```
cat ~/.ssh/id_rsa.semaphore.pub | pbcopy
```
- on the server:
echo "<paste the key you just copied>" >> ~/.ssh/authorized_keys
- clone your git repo to be the html directory on your server
```bash
git clone https://<yourtoken>@github.com/willrstern/example-deployment.git html
```

### Setup Semaphore
- create a new project
- setup test command (or just do `echo ok` if you don't have tests)
- setup a server
- add these 2 deployment commands
```
ssh-keyscan -H -p 22 45.55.153.229 >> ~/.ssh/known_hosts
ssh root@45.55.153.229 'bash -s' < deploy.sh
```
- paste the contents of `~/.ssh/id_rsa.semaphore` as your private key
