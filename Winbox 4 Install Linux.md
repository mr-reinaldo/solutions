# Instalação do WinBox no Linux (Linux Mint 22.1)

Este guia descreve o processo de instalação do **WinBox 4** no Linux Mint 22.1 para que funcione corretamente, incluindo sua exibição no menu de aplicativos.

---

## Passo 1: Extraia o arquivo

1. Baixe o arquivo `.zip` do **WinBox** no site oficial da [MikroTik](https://mikrotik.com/download).

2. Extraia o arquivo `.zip` enviado para um diretório temporário.

   ```bash
   unzip WinBox_Linux.zip -d WinBox
   ```

3. Verifique se os arquivos extraídos incluem o executável `WinBox` e uma pasta chamada `assets`.

---

## Passo 2: Mova os arquivos para o local de instalação

1. Crie um diretório dedicado em `/opt` para armazenar os arquivos do programa:

   ```bash
   sudo mkdir -p /opt/WinBox
   ```

2. Mova o executável e a pasta `assets` para o diretório criado:

   ```bash
   sudo mv /caminho/destino/WinBox /opt/WinBox/
   sudo mv /caminho/destino/assets /opt/WinBox/
   ```

3. Ajuste as permissões para que o usuário atual possa gerenciar os arquivos:

   ```bash
   sudo chown -R $USER:$USER /opt/WinBox
   ```

---

## Passo 3: Torne o executável funcional

1. Acesse o diretório onde o `WinBox` foi movido:

   ```bash
   cd /opt/WinBox
   ```

2. Torne o arquivo `WinBox` executável:

   ```bash
   chmod +x WinBox
   ```

3. Teste a execução para garantir que está funcionando:

   ```bash
   ./WinBox
   ```

---

## Passo 4: Adicione o programa ao menu de aplicativos

1. Crie um arquivo `.desktop` no diretório de atalhos do usuário:

   ```bash
   nano ~/.local/share/applications/winbox.desktop
   ```

2. Adicione o seguinte conteúdo ao arquivo, ajustando os caminhos conforme necessário:

   ```ini
   [Desktop Entry]
   Name=WinBox
   Comment=Gerenciador de configurações MikroTik
   Exec=/opt/WinBox/WinBox
   Icon=/opt/WinBox/assets/img/winbox.png
   Terminal=false
   Type=Application
   Categories=Internet;
   ```

3. Salve e feche o arquivo.

4. Certifique-se de que o arquivo `.desktop` tenha permissões corretas:

   ```bash
   chmod +x ~/.local/share/applications/winbox.desktop
   ```

5. Atualize os bancos de dados do menu:

   ```bash
   update-desktop-database ~/.local/share/applications
   ```

---

## Passo 5: Acesse o programa pelo menu

1. Abra o menu de aplicativos.
2. Procure por **WinBox** na categoria **Internet** e clique para abrir.

---

## Passo 6: Atualizações futuras

Se o programa exibir mensagens como "installed directory is read-only" durante uma atualização:

1. Certifique-se de que os arquivos estão em `/opt/WinBox` e que você tem permissões de escrita:

   ```bash
   sudo chown -R $USER:$USER /opt/WinBox
   ```

2. Reinstale ou substitua os arquivos manualmente, seguindo os passos acima.
