#Autor: Robson Vaamonde<br>
#Procedimentos em TI: http://procedimentosemti.com.br<br>
#Bora para Prática: http://boraparapratica.com.br<br>
#Robson Vaamonde: http://vaamonde.com.br<br>
#Facebook Procedimentos em TI: https://www.facebook.com/ProcedimentosEmTi<br>
#Facebook Bora para Prática: https://www.facebook.com/BoraParaPratica<br>
#Instagram Procedimentos em TI: https://www.instagram.com/procedimentoem<br>
#YouTUBE Bora Para Prática: https://www.youtube.com/boraparapratica<br>
#Data de criação: 07/03/2024<br>
#Data de atualização: 07/03/2024<br>
#Versão: 0.01<br>

OBSERVAÇÃO IMPORTANTE: COMENTAR NO VÍDEO DO ZABBIX SE VOCÊ CONSEGUIU FAZER O DESAFIO COM 
A SEGUINTE FRASE: Desafio do Zabbix realizado com sucesso!!! #BoraParaPrática

COMPARTILHAR O SELO DO DESAFIO NAS SUAS REDES SOCIAIS (LINKEDIN, FACEBOOK, INSTRAGRAM)
MARCANDO: ROBSON VAAMONDE COM AS HASHTAGS E CONTEÚDO DO DESAFIO ABAIXO: 

LINK DO SELO: https://github.com/vaamonde/ubuntu-2204/blob/main/selos/11-zabbix.png

#boraparapratica #boraparaprática #vaamonde #robsonvaamonde #procedimentosemti #ubuntuserver 
#ubuntuserver2204 #desafiovaamonde #desafioboraparapratica #desafiozabbix

Conteúdo estudado nesse desafio:<br>
#01_ Instalando as Dependências do Zabbix Server e Agent<br>
#02_ Adicionando o Repositório do Zabbixn no Ubuntu Server<br>
#03_ Instalando o Zabbix Server, Frontend e Agent<br>
#04_ Criando a Base de Dados no MySQL Server do Zabbix Server<br>
#05_ Testando o acesso a Base de Dados no MySQL Server do Zabbix Server<br>
#06_ Populando as Tabelas no Banco de Dados do Zabbix Server<br>
#07_ Editando os arquivos de Configurações do Zabbix Server e Agent<br>
#08_ Habilitando o Serviço do Zabbix Server e Agent<br>
#09_ Verificando o Serviço e Versão do Zabbix Server e Agent<br>
#10_ Configurando o Zabbix Server via Navegador<br>
#11_ Verificando a Porta de Conexão do Zabbix Server e Agent<br>
#12_ Localização dos diretórios principais do Zabbix Server e Agent<br>
#13_ Instalando os Agentes do Zabbix no Linux Mint e no Windows 10<br>
#14_ Criando os Hosts de Monitoramento dos Agentes no Zabbix Server<br>

Site Oficial do Zabbix: https://www.zabbix.com/<br>

Traduzido do inglês-O Zabbix é uma ferramenta de software de código aberto para monitorar<br>
a infraestrutura de TI, como redes, servidores, máquinas virtuais e serviços em nuvem. O <br>
Zabbix coleta e exibe métricas básicas.

[![Zabbix](http://img.youtube.com/vi//0.jpg)]( "Zabbix")

Link da vídeo aula: 

#01_ Instalando as Dependências do Zabbix Server e Agent<br>

	#atualizando as lista do apt
	sudo apt update

	#instalando as dependências do Zabbix
	sudo apt install traceroute nmap snmp snmpd snmp-mibs-downloader apt-transport-https \
	software-properties-common git vim

#02_ Adicionando o Repositório do Zabbixn no Ubuntu Server<br>

	#Link de referência do download: https://www.zabbix.com/download
	
	#OBSERVAÇÃO IMPORTANTE: NESSE VÍDEO ESTÁ SENDO INSTALADO E CONFIGURADO A VERSÃO 7.0
	#PRE-RELEASE (BETA - NÃO OFICIAL LTS), A VERSÃO LTS (Long Time Support) É: 6.4.

	#OBSERVAÇÃO IMPORTANTE: NAS CONFIGURAÇÕES DE DOWNLOAD DO REPOSITÓRIO DO ZABBIX SERVER
	#FOI SELECIONADO: 7.0 PRE-RELEASE, Ubuntu, 22.04 (Jammy), Server, Frontend, Agent, MySQL
	#e Apache.

	#download do repositório do Zabbix Server
	wget https://repo.zabbix.com/zabbix/6.5/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.5-1+ubuntu22.04_all.deb

	#instalação do repositório do Zabbix Server
	#opção do comando dpkg: -i (install)
	sudo dpkg -i zabbix-release_6.5*.deb

#03_ Instalando o Zabbix Server, Frontend e Agent<br>

	#OBSERVAÇÃO IMPORTANTE: para a instalação do Zabbix Server e necessário ter instalado e
	#configurado de forma correto o MySQL Server e o Apache2 Server, no caso do Banco de Dados
	#MySQL Server pode ficar em outro servidor (Recomendado).

	#atualizando as lista do apt com o novo repositório do Zabbix
	sudo apt update

	#instalando o Zabbix
	#opção do comando apt: --install-recommends (Consider suggested packages as a dependency for installing)
	sudo apt install --install-recommends zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf \
	zabbix-sql-scripts zabbix-agent

#04_ Criando a Base de Dados no MySQL Server do Zabbix Server<br>

	#opções do comando mysql: -u (user), -p (password)
	sudo mysql -u root -p

```sql
/* Criando o Banco de Dados Zabbix */
CREATE DATABASE zabbix CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;

/* Criando o Usuário Zabbix com a Senha Zabbix do Banco de Dados Zabbix*/
CREATE USER 'zabbix'@'localhost' IDENTIFIED WITH mysql_native_password BY 'zabbix';
GRANT USAGE ON *.* TO 'zabbix'@'localhost';
GRANT ALL PRIVILEGES ON zabbix.* TO 'zabbix'@'localhost';
FLUSH PRIVILEGES;

/* Habilitando a opção de Criação de Função log_bin_trust_function_creators no MySQL Server*/
SET GLOBAL log_bin_trust_function_creators = 1;

/* Listando os Bancos de Dados do MySQL */
SHOW DATABASES;

/* Verificando o Usuário Zabbix criado no Banco de Dados MySQL Server*/
SELECT user,host FROM mysql.user;

/* Saindo do Banco de Dados */
exit
```

#05_ Testando o acesso a Base de Dados no MySQL Server do Zabbix Server<br>

	#opções do comando mysql: -u (user), -p (password)
	sudo mysql -u zabbix -p

```sql
/* Listando os Bancos de Dados do MySQL */
SHOW DATABASES;

/* Acessando o Banco de Dados Zabbix */
USE zabbix;

/* Saindo do Banco de Dados */
exit
```

#06_ Populando as Tabelas no Banco de Dados do Zabbix Server utilizando o arquivo de Esquema<br>

	 #importando o esquema e os dados iniciais do banco de dados do Zabbix
	 #opções do comando mysql: -u (user), -p (password), zabbix (database)
	 sudo zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | sudo mysql --default-character-set=utf8mb4 \
	 -uzabbix -pzabbix zabbix 

	#opções do comando mysql: -u (user), -p (password)
	sudo mysql -u zabbix -p

```sql
/* Desabilitando a opção de Criação de Função log_bin_trust_function_creators no MySQL Server*/
SET GLOBAL log_bin_trust_function_creators = 0;

/* Acessando o Banco de Dados Zabbix */
USE zabbix;

/* Verificando as Tabelas criadas pelo Script*/
SHOW TABLES;

/* Saindo do Banco de Dados */
exit
```

#07_ Editando os arquivos de Configurações do Zabbix Server e Agent<br>

	#editando o arquivo de configuração do Zabbix Server
	sudo vim /etc/zabbix/zabbix_server.conf
	INSERT

		#decomentar e alterar o valor da variável DBPassword= na linha: 129
		DBPassword=zabbix
	
	#salvar e sair do arquivo
	ESC SHIFT : x <Enter>

	#editando o arquivo de configuração do Zabbix Agent
	sudo vim /etc/zabbix/zabbix_agentd.conf
	INSERT

		#deixar o padrão das variáveis Server= e ServerActive= nas linhas: 117 e 171
		Server=127.0.0.1
		ServerActive=127.0.0.1

		#alterar o valor da variável Hostname= na linha: 182
		Hostname=wsvaamonde
	
	#salvar e sair do arquivo
	ESC SHIFT : x <Enter>

#08_ Habilitando o Serviço do Zabbix Server e Agent<br>

	#habilitando o serviço do Zabbix Server e Agent
	sudo systemctl daemon-reload
	sudo systemctl enable zabbix-server zabbix-agent
	sudo systemctl restart zabbix-server zabbix-agent apache2

#09_ Verificando o Serviço e Versão do Zabbix Server e Agent<br>

	#verificando o serviço do Zabbix Server e Agent
	sudo systemctl status zabbix-server zabbix-agent
	sudo systemctl restart zabbix-server zabbix-agent
	sudo systemctl stop zabbix-server zabbix-agent
	sudo systemctl start zabbix-server zabbix-agent

	#verificando a versão do Zabbix Server e Agent
	#opção do comando dpkg-query: -W (show), -f (showformat), ${version} (package information), \n (newline)
	sudo dpkg-query -W -f '${version}\n' zabbix-agent
	sudo dpkg-query -W -f '${version}\n' zabbix-server-mysql

#10_ Configurando o Zabbix Server via Navegador<br>

	firefox ou google chrome: http://endereço_ipv4_ubuntuserver/zabbix

#11_ Verificando a Porta de Conexão do Zabbix Server e Agent<br>

	#opção do comando lsof: -n (network number), -P (port number), -i (list IP Address), -s (alone directs)
	sudo lsof -nP -iTCP:'10050,10051' -sTCP:LISTEN

#12_ Localização dos diretórios principais do Zabbix Server e Agent<br>

	/etc/zabbix/*     <-- Diretório dos arquivos de Configuração do serviço do Zabbix
	/var/log/zabbix*  <-- Diretório dos arquivos de Log's do serviço do Zabbix
	/usr/share/zabbix <-- Diretório dos arquivos do Site do serviço do Zabbix

#13_ Instalando os Agentes do Zabbix no Linux Mint e no Windows 10<br>

#14_ Criando os Hosts de Monitoramento dos Agentes no Zabbix Server<br>

#15_ DESAFIO-01: 


=========================================================================================

OBSERVAÇÃO IMPORTANTE: COMENTAR NO VÍDEO DO ZABBIX SE VOCÊ CONSEGUIU FAZER O DESAFIO COM 
A SEGUINTE FRASE: Desafio do Zabbix realizado com sucesso!!! #BoraParaPrática

COMPARTILHAR O SELO DO DESAFIO NAS SUAS REDES SOCIAIS (LINKEDIN, FACEBOOK, INSTRAGRAM)
MARCANDO: ROBSON VAAMONDE COM AS HASHTAGS E CONTEÚDO DO DESAFIO ABAIXO: 

LINK DO SELO: https://github.com/vaamonde/ubuntu-2204/blob/main/selos/11-zabbix.png

#boraparapratica #boraparaprática #vaamonde #robsonvaamonde #procedimentosemti #ubuntuserver 
#ubuntuserver2204 #desafiovaamonde #desafioboraparapratica #desafiozabbix 