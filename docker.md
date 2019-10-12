# Docker

Exclusão de containers

```text
docker rm -f $(docker ps -aq)
```

\# Aprendendo Docker

\#\# Principais comandos

\| Comando \| Finalidade \|

\| ------ \| ------ \|

\|docker exec -it container\_id /bin/bash\| Conectar em um container em execução \|

\|docker build . \| Gerar uma nova imagem com base no arquivo Dockerfile no diretório corrente, sinalizado pelo . \|

\|docker build -t minha\_imagem . \| Acrescenta a tag minha\_imagem na imagem gerada com o build \|

\#\# O Dockerfile

&gt; A sintaxe básica é DIRETIVA e VALOR, separados por tab/espaço. A seguir um resumo sobre cada uma das diretivas.

\`\`FROM\`\` Imagem base para construção da nova imagem

\`\`MAINTAINER\`\` Nome e email do mantenedor da imagem

\`\`RUN\`\` Executa comandos na construção da imagem. Ex: update e instalação de pacotes

\`\`CMD\`\` Comando que o container vai executar ao ser instanciado. Só pode existir um por Dockerfile. Caso exista mais de um, somente o último terá validade.

\`\`COPY\`\` Copia um arquivo para dentro do container

\`\`ADD\`\` Copia um arquivo para o container

\`\`ENTRYPOINT\`\`

\`\`ENV\`\`

\`\`USER\`\`

\`\`WORKDIR\`\`

\`\`ARG\`\`

\`\`ONBUILD\`\`

\`\`STOPSIGNAL\`\`

\`\`HEALTHCHECK\`\`

\`\`SHELL\`\`

\`\`LABEL\`\`

\`\`EXPOSE\`\` Abre portas de comunicação entre containers, todas separadas por espaços. Ex: 80 443 8080

\# O docker-compose

\#\# Principais comandos

\#\# O docker-compose.yml

[http://blog.arungupta.me/docker-common-commands-cheatsheet-techtip59/](http://blog.arungupta.me/docker-common-commands-cheatsheet-techtip59/)

