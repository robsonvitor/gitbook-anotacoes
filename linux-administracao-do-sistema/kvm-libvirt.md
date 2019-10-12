# KVM - libvirt

### **Clonar máquina virtual**

```text
virt-clone --original NOME_ORIGEM --name NOME_DESTINO --auto-clone
```

[https://www.cyberciti.biz/faq/how-to-clone-existing-kvm-virtual-machine-images-on-linux/](https://www.cyberciti.biz/faq/how-to-clone-existing-kvm-virtual-machine-images-on-linux/)

### **Snapshots de Máquinas Virtuais**

#### **Criar um snapshot**

```text
virsh snapshot-create-as --domain {VM-NAME} --name "{SNAPSHOT-NAME}"
```

#### **Listar snapshots**

```text
virsh snapshot-list --domain {VM-NAME}
```

#### **Restaurar um snapshot**

```text
virsh snapshot-revert --domain {VM-NAME} --snapshotname {SNAPSHOT-NAME} --running
```

#### **Apagar um snapshot**

```text
virsh snapshot-delete --domain {VM-NAME} --snapshotname {SNAPSHOT-NAME}
```

[https://www.cyberciti.biz/faq/how-to-create-create-snapshot-in-linux-kvm-vmdomain/](https://www.cyberciti.biz/faq/how-to-create-create-snapshot-in-linux-kvm-vmdomain/)

**Montar imagem de disco para acesso aos dados**



[https://www.unixarena.com/series/linux-kvm/](https://www.unixarena.com/series/linux-kvm/)

```text
apt install libguestfs-tools
```

```text
guestmount -a /caminho/imagem -m /dev/sda1 /caminho/montagem
```

**Redimensionar disco qcow2**

```text
qemu-img resize image.qcow2 +SIZE
```

Após redimensionar a imagem, utilizar o GParted Live para redimensionar o disco no Sistema Operacional

[https://maunium.net/blog/resizing-qcow2-images/](https://maunium.net/blog/resizing-qcow2-images/)

**Reduzir tamanho de imagem qcow2**

Documentar assim que tiver tempo. Está no link acima.

