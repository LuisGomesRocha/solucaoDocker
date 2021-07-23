# solucaoDocker
Inicialmente vou configurar docker-compose.yaml com as configurações para o mercado livre.
No arquivo de composição, começaremos definindo a versão do esquema. Na maioria dos casos, é melhor usar a versão mais recente com suporte: version: "3.7"
Em seguida vou definir dois serviços trazendo duas imagens : 
“image: postgres:9.6” 
e  
“image: dpage/mercado4:4.10”.
Primeira imagem é referente ao banco de dados postgres;
Segundo é sobre pgAdmin, uma plataforma opensource de administração e desenvolvimento para PostgreSQL e seus sistemas de gerenciamento de banco de dados relacionados.

Vou mapear a porta   ports:  - "5433:5432", bem como   colocar na rede networks:    - postgres-ml-network
Para a imagem postgres:9.6 vou definir o nome do container de "mercadolivre-postgres" e configurar o ambiente denominando o nome do banco de dados, seu usuário e senha:

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

Em seguida vou configurar docker-compose.yaml com as configurações para casa do código.
No arquivo de composição, começaremos definindo a versão do esquema. Na maioria dos casos, é melhor usar a versão mais recente com suporte: version: "3.7"
Em seguida vou definir dois serviços trazendo duas imagens: 
“image: postgres:9.6” 
e  
“image: dpage/casaCodigo4:4.10”.
Primeira imagem é referente ao banco de dados postgres;
Segundo é sobre pgAdmin, uma plataforma opensource de administração e desenvolvimento para PostgreSQL e seus sistemas de gerenciamento de banco de dados relacionados.

Vou mapear a porta   ports:  - "5434:5434", bem como   colocar na rede networks:    - postgres-ml-network
Para a imagem postgres:9.6 vou definir o nome do container de " casaDoCodigo-postgres " e configurar o ambiente denominando o nome do banco de dados, seu usuário e senha:

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

Lembrando que ambas as aplicações estão configuradas para utilizarem a porta 8080, vou configurar as portas internas dos contêineres com 8080 e as externas como 8080 e 8081. Não terá conflito pelo fato de ambas as API´s rodarem dentro dos containers junto com os bancos de dados.


Docker: Criando containers sem dor de cabeça
Cenário:
Agora que você já desenvolveu os sistemas que simulam a Casa do Código e o Mercado Livre imagine que é necessário preparar essas aplicações para serem executadas em um ambiente real, seja por você mesmo ou por outra equipe da sua empresa.
Sabendo que já existe um ambiente preparado com Docker, como você faria para gerar as imagens referentes a cada uma das aplicações? Cada uma das aplicações também precisa de um banco de dados para funcionar corretamente, o que você faria para garantir a existência do banco de dados no momento da criação dos contêineres a partir das imagens criadas?
Lembrando que ambas as aplicações estão configuradas para utilizarem a porta 8080, existe algum problema ao subir contêineres de ambas as imagens criadas ao mesmo tempo?
E como você faria para executar as imagens criadas?

O que seria bom ver nessa resposta?
•	Peso 5: Criação dos arquivos Dockerfile de cada uma das aplicações
•	Peso 3: Criação do docker-compose.yml para orquestrar a subida da aplicação e do banco de dados
•	Peso 2: Mapeamento das portas das aplicações nos contêineres para as portas do host
Resposta do Especialista:
•	Objetivo de aprendizado: Configurar as imagens docker das aplicações desenvolvidas através do Dockerfile e orquestrar o build e execução delas através do docker-compose.yml
•	Motivo da escolha: Através do Dockerfile configuro como serão as imagens criadas para cada uma das aplicações e utilizo o docker-compose para orquestrar a execução dessas imagens com os bancos de dados necessários para cada aplicação.
•	Crio o Dockerfile de cada uma das aplicações para definir como serão geradas as imagens das mesmas
•	Para cada uma das aplicações também crio um arquivo docker-compose.yml, onde defino uma sessão de configuração do container da aplicação, mapeando o Dockerfile criado anteriormente, e uma sessão para o banco de dados a ser utilizado pela aplicação
•	Uma vez que cada aplicação estará isolada em seu próprio contêiner, não há problema se as mesmas utilizarem a mesma porta. Porém a porta do host deverá ser mapeada para garantir acesso a aplicação: em cada um dos Dockerfiles mapeio as portas do host:contêiner (8081:8080 para Casa do Código e 8082:8080 para Mercado Livre, por exemplo).


