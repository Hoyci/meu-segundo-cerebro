Docker compose é uma ferramenta para definir e rodar aplicações multi-containers juntas em um ambiente isolado. Esse arquivo pode ser usado para rodar todos os serviços necessários da aplicação (como: banco de dados, fila de mensagens, etc). Dessa maneira, com um simples comando pode-se criar e iniciar todo os serviços a partir do arquivo de configuração
## Principais funcionalidades do docker compose
* **Definição de serviços**: Você pode definir todos os serviços (containers) que compõem a sua aplicação em um único arquivo
* **Configurações de redes**: Docker compose permite configurar redes personalizadas para que os containers possam se comunicar de forma isola e segura
* **Definição de volumes**: Facilita a criação e o gerenciamento de volumes para persistência de dados.
* **Escalabilidade**: Você pode facilmente escalar o número de containers para cada serviço
## Estrutura básica de um arquivo docker-compose.yml

Estrutura:
```yaml
version: '3.8'
sevices:
	# definição dos serviços
networks::
	# definição de redes
volumes:
	# definição de volumes
```

Exemplo:
```yaml
version: '3.8'
sevices:
	web:
		image: nginx:latest
		ports:
			- "8080:80"
		networks:
			- mynetwork
		volumes:
			- myvolume:/usr/share/nginx/html
	app:
		image: myapp:latest
		depends_on:
			- db
		networks:
			- mynetwork
		volumes:
			- myappdata:/var/lib/myapp/data
	db:
		image: postgres:13
		environment:
			POSTGTES_USER: user
			POSTGRES_PASSWORD: password
		volumes:
			- dbdata:/var/lib/postgresql/data
		networks:
			- mynetwork
networks:
	mynetwork:
		driver: bridge
volumes:
	myvolume:
	myappdata:
	dbdata:
```