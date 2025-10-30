# An example of setup: jenkins & nexus configuration

## Запуск jenkins сервера

### Прописать dns IP
```
echo -e "<IP1> bitbucket.lcl\n<IP2> nexus.lcl\n<IP3> jenkins.lcl" | tee -a /etc/hosts
```

### Bitbucket Pull
```
GIT_SSL_NO_VERIFY=true git clone https://bitbucket.lcl/scm/sre/sre.example.git
```

### Настройки Docker
```
nano /etc/docker/daemon.json
{
  "insecure-registries": ["nexus.lcl"]
}

service docker restart
```

## Сборка jenkins агента
```
docker build . -f deploy/Dockerfile.agent -t nexus.lcl/jenkins-agent:main
```
