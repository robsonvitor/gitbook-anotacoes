# Alternar em placas de vídeo

Quando o computador possui placa gráfica embutida, como é o caso do meu Dell Inspiron 5548, para ativar a segunda placa, é necessário definir na variável de ambiente DRI\_PRIME o número da segunda placa. 

```text
# echo "DRI_PRIME=1" > /etc/environment.d/80-video.conf
```

Após reiniciar verificar se foi ativada com o comando:

```text
glxinfo -B
```

