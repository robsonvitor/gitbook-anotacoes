# grub

**Editar o arquivo de configuração do GRUB**

```text
# vim /etc/default/grub
```

**Alterar o número do sistema operacional 0,1,2... padrão para saved**

```text
GRUB_DEFAULT=saved
```

**Executar o comando**

```text
# update-grub
```

**Escolhendo o boot padrão. Lembrando que começa em 0. Exemplo, temos o Linux como 0 e Windows como 1. Supondo que deseje iniciar no Windows apenas no próximo boot, execute o comando:**

```text
# grub-reboot 1
```

**Alterando permanentemente o sistema operacional padrão na inicialização, onde N é o número na lista**

```text
# grub-set-default N
```

**Após alteração, reiniciar para que o sistema desejado seja inicializado**

