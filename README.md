Como compartilhar pasta no Ubuntu 24.04 e Configurar Wings

Instale esses pacotes:

  sudo apt update && sudo apt upgrade -y
  sudo apt install cifs-utils smbclient -y

/mnt/
Criar o ponto de montagem:

Bash: sudo mkdir -p /mnt/backups


Crie um arquivo com as credenciais:

Bash: sudo nano /etc/smb_credentials


Cole (Edite os dados): 

username=usuario
password=senha_do_usuario
  

Dê as devidas permissões:

Bash: sudo chmod 600 /etc/smb_credentials

Acesse o fstab:

Bash: sudo nano /etc/fstab

Cole e Edite o comando abaixo com as devidas informações, como endereço de IP/path, UID do usuário criado e onde foi criada a pasta /mnt:

Edite o "//192.168.X.XXX/XXX" para sua configuração de rede e "uid=XXX,gid=XXX" para o ID dos usuários informados lá no arquivo: "smb_credentials" em /etc

Bash: //192.168.X.XXX/XXX /mnt/backups cifs credentials=/etc/smb_credentials,uid=XXX,gid=XXX,file_mode=0775,dir_mode=0775,_netdev,vers=3.0  0  0

Como saber o UID, rode esse comando no servidor onde foi criado o usuário SMB servidor onde está o compartilhamento:

Bash: id nome do usuário


Rode comando para reiniciar o serviço:

Bash: sudo mount -a


Reinicie a máquina para ver se é montado automaticamente.

Editar o arquivo das Wings para configurar os backups:

Bash: nano /etc/pelican/config.yml


Procure por: 

Bash: backup_directory: /var/lib/pelican/backups


Altere para o caminho antes configurado no caso:

Bash: /mnt/backups/backups/wings02


Reinicie o Servidor Wings.
