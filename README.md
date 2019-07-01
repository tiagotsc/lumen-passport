PASSO A PASSO PARA USO:

1 - Através do Powershell ou CMD, acesse a pasta do projeto (aonde esta o arquivo docker-compose.yaml), e executar o comando: docker-compose up --build

2- Depois abra outro terminal no mesmo diretório e execute o comando para acessar o container: docker-compose exec php-fpm bash

3 - Já dentro do container, entre na pasta do projeto 'api' através do comando: cd api

4 - Dentro da pasta api rode o comando: composer install

5 - Dentro da pasta api, executar o migrate para criar as tabelas: php artisan migrate

6 - Executar o seed para popular o banco: php artisan db:seed

7 - Caso queira executar os testes do CRUD de produtos, é só executar o seguinte comando dentro da pasta 'api': vendor/bin/phpunit

OBS: 
Caso queirar gerar novos contratos passport é só executar o seguinte comando dentro da pasta 'api': php artisan passport:client --client.
Criei uma pequena aplicação client com jquery para demonstrar o uso da API na prática, acesse pelo navegador: http://localhost/testa_api.html

Acessos:

Banco Mysql:
- Host: 127.0.0.1
- Usuário: test
- Senha: test
- Banco de dados: api

Usuário cadastrado no banco:
- Login: usuario.teste@teste.com.br
- Senha: 123

Métodos disponíveis e respectivos exemplos de uso:

- Login user passport:
	- URL: http://localhost/oauth/token
	- Método: POST
	- Header: [{"key":"Content-Type","value":"application/json"]
	- Body raw: {
			 "grant_type": "password",
			 "scope": "*",
			 "client_id": "2",
			 "client_secret": "1VUPQqxNSCVuYY00vhQ3obSTJeh5JpoAKipGwNOm",
			 "username": "usuario.teste@teste.com.br",
			 "password": "123"
			}
			
- Login client passport:
	- URL: http://localhost/api/v1/oauth/token
	- Método: POST
	- Header: [{"key":"Content-Type","value":"application/json"]
	- Body raw: {
			"grant_type": "client_credentials",
			"scope": "*",
			"client_id": "1",
 			"client_secret": "VUMapUL7yGM29M9gGbE1SfMTSik9wEER22YOrE73"
			}
			
- Lista produtos com filtros, ordenação e paginação:
	- URL: http://localhost/api/v1/products
	- Authorization: Bearer Token ...
	- Método: GET
	- Header: [{"key":"Content-Type","value":"application/json"]
	- Body raw: {
			"data": "name=seringa",
			"order": "quantity|desc",
			"items": "2"
			}
			
- Cadastra produto:
	- URL: http://localhost/api/v1/products
	- Authorization: Bearer Token ...
	- Método: POST
	- Header: [{"key":"Content-Type","value":"application/json"]
	- Body raw: {
			"name": "Teste",
			"brand": "marca",
			"price": "5.89",
			"quantity": "45"
			}
			
- Altera produto:
	- URL: http://localhost/api/v1/products/3
	- Authorization: Bearer Token ...
	- Método: PUT
	- Header: [{"key":"Content-Type","value":"application/json"]
	- Body raw: {
			"name": "Teste22",
			"brand": "marca",
			"price": "10.89",
			"quantity": "45"
			}
			
- Lista um único produto:
	- URL: http://localhost/api/v1/products/3
	- Authorization: Bearer Token ...
	- Método: GET
	- Header: [{"key":"Content-Type","value":"application/json"]
			
- Apaga produto:
	- URL: http://localhost/api/v1/products/3
	- Authorization: Bearer Token ...
	- Método: DELETE
	- Header: [{"key":"Content-Type","value":"application/json"]