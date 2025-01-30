# SOLUÇÃO PARA PROMISCUOUS MODE NO VMWARE WORKSTATION PRO 17 (Linux Mint 22.1)

Este documento tem como objetivo apresentar uma solução simples para habilitar o modo promíscuo em uma máquina virtual no VMWare Workstation Pro. Com isto, é possível a comunicação entre máquinas virtuais e o host, bem como a comunicação entre máquinas virtuais.

## Verificando se todos os módulos necessários estão carregados

1; Abra o terminal e execute o comando abaixo:

```bash
sudo vmware-modconfig --console --install-all
```

2; Inicia as interfaces vmnet:

```bash
sudo vmware-networks --start
```

## Criando um grupo para o vmware e adicionando o usuário ao grupo

1; Abra o terminal e execute o comando abaixo para criar o grupo vmware:

```bash
sudo groupadd vmware
```

2; Execute o comando abaixo para adicionar o usuário ao grupo vmware:

```bash
sudo usermod -aG vmware $USER
```

3; Use o comando newgrp para ativar o grupo vmware:

```bash
newgrp vmware
```

4; Adicionando as interfaces vmnet ao grupo vmware:

```bash
chgrp vmware /dev/vmnet*
chmod g+rw /dev/vmnet*
```

## Habilitando as configurações de forma permanente

1; Abra o terminal e execute o comando:

```bash
 sudo vim /etc/init.d/vmware
```

2; Procure pela linha abaixo:

```bash
# Start the virtual ethernet kernel service
vmwareStartVmnet() {
   vmwareLoadModule $vnet
   "$BINDIR"/vmware-networks --start >> $VNETLIB_LOG 2>&1
}

```

3; Adicione o comando abaixo logo após a linha acima:

```bash

# Start the virtual ethernet kernel service
vmwareStartVmnet() {
   vmwareLoadModule $vnet
   "$BINDIR"/vmware-networks --start >> $VNETLIB_LOG 2>&1

   chgrp vmware /dev/vmnet*
   chmod g+rw /dev/vmnet*
}

```

4; Salve o arquivo e saia do editor.

5; Por fim, reinicie o serviço do vmware ou reinicie o sistema:

```bash
sudo service vmware restart
```

ou

```bash
sudo reboot
```
