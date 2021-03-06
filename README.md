# CICD
Material do ambiente do curso de Integração e Entrega Continua com Git, Jenkins, Nexus e Sonar


## Aula00 - Apresentando ambiente com Vagrant
## Aula01 - Iniciando ambiente com maquina repo
### Maquina Host	
sudo vagrant up repo --provision
### Maquina Repo
Instalando Gitlab-CE
```sh
# curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
# yum install -y gitlab-ce
```
Configurando Gitlab-CE
```sh
# vim /etc/gitlab/gitlab.rb

...
external_url 'http://192.168.88.10'
alertmanager['enable'] = false
gitlab_monitor['enable'] = false
node_exporter['enable'] = false
postgres_exporter['enable'] = false
prometheus['enable'] = false
redis_exporter['enable'] = false
...
```
Carregando novas configurações
```sh
# gitlab-ctl reconfigure
```

Com Gitlab-CE instalado e configurado podemos acessa-lo plo endereço http://192.168.88.10.


## Aula02 - Iniciando maquina pipeline
Iniciando a maquina pipeline via vagrant.
```sh
$ vagrant up pipeline --provision
```
### Instalando serviços na maquina pipeline
Instalando Jenkins
```sh
# curl http://pkg.jenkins-ci.org/redhat/jenkins.repo -o /etc/yum.repos.d/jenkins.repo
# rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
# yum install jenkins -y
# systemctl enable jenkins
# systemctl start jenkins
```
### Instalando Docker na maquina pipeline
```sh
# yum install -y yum-utils device-mapper-persistent-data lvm2
# yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
# yum install -y docker-ce docker-ce-cli containerd.io
# systemctl enable docker
# systemctl start docker
```
### Rodando SonarQube no Docker
```sh
# docker run -dti --name sonarqube --restart always -p 9000:9000 sonarqube
``` 

### Rodando SonatypeNexus OSS no Docker
```sh
# docker run -dti --name nexus --restart always -p 8081:8081 sonatype/nexus3
``` 

