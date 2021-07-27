# solucaoDocker

<h4 align="center"> 
	🚧  Orange Talents  🚀 Em construção...  🚧
</h4>

<p align="center">🚀 Formulário de proposta de solução - Health Check, Readiness & Liveness Check e Spring Boot Actuator 🚀 </p>


<h1 align="center">
    <a href="https://www.youtube.com/watch?v=Kzcz-EVKBEQ">🔗Docker em 22 minutos - teoria e prática (Rápido!)</a>
</h1>

<h1 align="center">
    <a href="https://www.youtube.com/watch?v=yb2udL9GG2U">🔗Docker e Docker Compose do zero ao Deploy</a>
</h1>



### Liveness and Readiness

<p align="justify"> :robot: Imaginando que as API's criadas até agora utilizando Spring Boot estão sendo executadas em um ambiente gerenciado e capaz de monitorar a saúde de API's, como podemos prepará-las para fornecerem as informações necessárias para que esse mecanismo de monitoramento funcione corretamente? :robot: </p>


<p align="justify"> :robot: Inicialmente vou configurar docker-compose.yaml com as configurações para o mercado livre. No arquivo de composição, começaremos definindo a versão do esquema. Na maioria dos casos, é melhor usar a versão mais recente com suporte: :robot: </p>
  
 ```
 version: "3.7"
  
 ```
 
<p align="justify"> :robot: Em seguida vou definir dois serviços trazendo duas imagens : :robot: </p>
 
 ```
“image: postgres:9.6” 
e  
“image: dpage/mercado4:4.10”.

 ```
 
 <p align="justify"> :robot: Primeira imagem é referente ao banco de dados postgres; Segundo é sobre pgAdmin, uma plataforma opensource de administração e desenvolvimento para PostgreSQL e seus sistemas de gerenciamento de banco de dados relacionados. :robot: </p>
 
 <p align="justify"> :robot: Vou mapear a porta   :robot: </p>
  
   ```
  ports:  - "5433:5432"
  
   ```
 <p align="justify"> :robot: bem como colocar na rede: :robot: </p>
  
 ```
 networks:   
- postgres-ml-network
 
 ```

<p align="justify"> :robot: Para a imagem :robot: </p>

 ```
postgres:9.6 

 ```

<p align="justify"> :robot: vou definir o nome do container de "mercadolivre-postgres" e configurar o ambiente denominando o nome do banco de dados, seu usuário e senha: :robot: </p>

 ```
 
mercadolivredb:
  image: postgres:9.6
  container_name: "mercadolivre-postgres"
  environment:
    POSTGRES_DB: "mercadolivredb"
    POSTGRES_USER: "postgres"
    POSTGRES_PASSWORD: "postgres"
    TZ: "GMT"
  volumes:
    - mercadodb-volume:/var/lib/postgresql/data
  ports:
    - "5433:5432"
  networks:
    - postgres-ml-network
    
 ```
 
 ```

pgadmin4:
  image: dpage/pgadmin4:4.10
  container_name: "pgadmin4"
  environment:
    PGADMIN_DEFAULT_EMAIL: "admin@gmail.com"
    PGADMIN_DEFAULT_PASSWORD: "secret"
  ports:
    - "8082:80"
  networks:
    - pgadmin4-network
 
  ```

<p align="justify"> :robot: Em seguida vou configurar docker-compose.yaml com as configurações para casa do código.
No arquivo de composição, começaremos definindo a versão do esquema. Na maioria dos casos, é melhor usar a versão mais recente com suporte: version: "3.7"
Em seguida vou definir dois serviços trazendo duas imagens:  :robot: </p>

```
“image: postgres:9.6” 

```
```
“image: dpage/casaCodigo4:4.10”.

```
<p align="justify"> :robot: Primeira imagem é referente ao banco de dados postgres;
Segundo é sobre pgAdmin, uma plataforma opensource de administração e desenvolvimento para PostgreSQL e seus sistemas de gerenciamento de banco de dados relacionados.:robot: </p>

<p align="justify"> :robot: Vou mapear a porta: :robot: </p>

```
ports:  - "5434:5434"

```

<p align="justify"> :robot:
bem como   colocar na rede
:robot: </p>

```
networks:    - postgres-ml-network

```

<p align="justify"> :robot:
Para a imagem postgres:9.6 vou definir o nome do container de " casaDoCodigo-postgres " e configurar o ambiente denominando o nome do banco de dados, seu usuário e senha:
:robot: </p>

```
mercadolivredb:
  image: postgres:9.6
  container_name: "casaDoCodigo-postgres"
  environment:
    POSTGRES_DB: " casadocodigodb"
    POSTGRES_USER: "postgres"
    POSTGRES_PASSWORD: "postgres"
    TZ: "GMT"
  volumes:
    - mercadodb-volume:/var/lib/postgresql/data
  ports:
    - "5434:5434"
  networks:
    - postgres-ml-network
```

```
pgadmin4:
  image: dpage/pgadmin4:4.10
  container_name: "pgadmin4"
  environment:
    PGADMIN_DEFAULT_EMAIL: "admin@gmail.com"
    PGADMIN_DEFAULT_PASSWORD: "secret"
  ports:
    - "8080:80"
  networks:
    - pgadmin4-network
 
 ```

<p align="justify"> :robot:
Lembrando que ambas as aplicações estão configuradas para utilizarem a porta 8080, vou configurar as portas internas dos contêineres com 8080 e as externas como 8080 e 8081. Não terá conflito pelo fato de ambas as API´s rodarem dentro dos containers junto com os bancos de dados.
:robot: </p>
