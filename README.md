# Roteiro Engenharia de Software - Serviços de Computação em Núvem AWS

Integrantes: Alanis Viana, André Oliveira e Lucas da Silveira

O presente roteiro tem como funcionalidade apresentar um serviço de computação em núvem oferecidos pela Amazon no Amazon Web Service(AWS). A AWS oferece diferentes serviços de computação, podemos citar banco de dados, armazenamento, servidores, DNS, entre outros. Neste relatório, optamos por utilizar o serviço de Banco de Dados relacional da AWS, conhecido como RDS. Vamos mostrar o passo a passo para a criação da instância do banco de dados, alterar as políticas para que a instância seja acessada de modo público e como acessá-la a partir de uma aplicação simples utilizando a linguagem Python. 

## Criando uma conta na AWS: 
Nosso primeiro passo para seguirmos o roteiro é criar uma conta na AWS. 

  - Acesse o site: https://aws.amazon.com/pt/console/ 
  - Clique em <b> Faça login no console </b> na parte superior direita do site
  - Desça até o final da página e clique em criar uma nova conta na AWS
  - Siga os passos até o final para criar a conta.


## Criando a Instância do banco de dados: 

  - Acesse o site: https://aws.amazon.com/pt/console/ 
  - Clique em <b> Faça login no console </b> na parte superior direita do site
  - Entre com o usuário e senha criados na etapa anterior
  - Na parte superior de pesquisa, pesquise por RDS
![Screenshot from 2022-09-29 13-24-00](https://user-images.githubusercontent.com/84134732/193086812-e130bdcd-003f-43dc-86ba-9de94f3d1996.png)
  - Clique na primeira opção
  - No menu lateral, clique em banco de dados
    ![image](https://user-images.githubusercontent.com/84134732/193087214-b0f2b331-2442-4e12-b444-a8b9daf26c2e.png)
  
  - Na nova página que apareceu, clique em criar banco de dados 
  - Por tratar de um exemplo simples, a opção de criação padrão nos atende
  - Na opção de mecanismo, iremos utilizar a opção MySQL
  ![image](https://user-images.githubusercontent.com/84134732/193087729-f638356d-57d1-49d5-8453-66c6cd518e28.png)
  
  - Na parte de modelos, escolheremos a opção <b> Nível Gratuito</b>
  ![image](https://user-images.githubusercontent.com/84134732/193088014-f69dcbc6-4307-4d1d-a8d3-5ab0ad9fe11e.png)
  
  - Na parte de identificação da instância, podemos escolher um nome para identificar a instância. Escolheremos algo simples como: database-1
  - Na parte de usuários, deixaremos como usuário o admin e a senha: Teste1234
  - Seguindo, não mexeremos na configuração da instância, pois ela foi alterada para o nível gratuito.
  - A próxima alteração é no Acesso Público, onde marcaremos a caixa <b>Sim</b>
	- Após isso, é só descer até embaixo e clicar em <b>Criar banco de dados</b>
 
 Depois de todos os passos seguidos, a instância deverá aparecer na tela principal da seguinte forma: 
 ![image](https://user-images.githubusercontent.com/84134732/193089365-e9f56194-3ce6-4b2b-b022-d29a35dc2645.png)
 
 O processo de criar a intância, por parte da Amazon, pode demorar um pouco. 
 Quando terminar, deverá aparecer o status como disponível do seguinte modo: 
 ![image](https://user-images.githubusercontent.com/84134732/193091189-ac12f505-d1b8-44f0-bd11-fc201d1ddab4.png)

## Criando grupo de segurança

  - Clique novamente na barra de pesquisa e pesquise por EC2 e clique na primeira opção
    ![image](https://user-images.githubusercontent.com/84134732/193092426-fda325b1-01b6-4382-aa48-c3ef44e71c76.png)
  
  - No menu lateral, clique em <b>Security Group</b>
  ![image](https://user-images.githubusercontent.com/84134732/193092619-328cf240-d23f-40b3-8c28-657904f11562.png)
  
  - Clique em criar grupo de segurança
  - Coloque um nome e descrição para o grupo de segurança como: 
  ![image](https://user-images.githubusercontent.com/84134732/193092977-499ee765-eb6e-4c0e-9387-d57ae2efc38e.png)
  
  - Na parte de regras de entrada, cique em adicionar regra
  - Adicione as seguintes informações: 
  ![image](https://user-images.githubusercontent.com/84134732/193093296-5d3f284d-b4c3-432d-938c-3c564507e72d.png)
  
  - Clique em criar grupo de segurança

## Alterando as permissões na instância do banco de dados

  - Volte para a página do RDS
  - Clique em Banco de dados
  - Clique na sua instância de banco de dados
  - Clique em modificar 
  - Desça até a parte de conectividade e altere o grupo de segurança para o que acabamos de criar
  ![image](https://user-images.githubusercontent.com/84134732/193094104-d8f6d626-2b0e-4b37-8ca3-9dbbd4f60cbf.png)
  
  - Desça até o final da página e clique em continuar
  - Altere a opção de modificação para aplicar imediatamente 
  - Clique em <b>Modificar instância de banco de dados</b>

A instância entrará em estado de modificando até que as alterações sejam feitas.

## Realizando a conexão
Utilizaremos a linguagem python por ser mais simples a implementação de conexão. Utilizando a biblioteca mysql-conector-python na versão 8.0.29.
Para obter a biblioteca, utilize o seguinte comando: pip3 install mysql-connector-python==8.0.29

Em um arquivo python coloque o seguinte código: 
```
import mysql.connector
try:
	mydb = mysql.connector.connect(
	  host="SEU_HOST",
	  user="admin",
	  password="Teste1234"
	)
except:
	print(error)
print(mydb)
```
A informação do Host, poderá ser encontrada na página da sua instância na parte de <b> EndPoint e porta </b>
Geralmente o endpoint é um endereço com o nome do seu banco na frente. Então seu endpoint será do formato:

Após executar o arquivo python, deverá aparecer a seguinte mensagem: <br>
![image](https://user-images.githubusercontent.com/84134732/193096676-18ce9c45-eda4-426c-b7b6-d74c815370cf.png)<br>
Que é justamente o objeto da conexão, em outras palavras, a conexão com o banco de dados criado está estabelecida!
