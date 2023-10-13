# Como um Strapi com docker e docker-compose


- Valide [aqui](./Dockerfile) se esse arquivo existe (Dockerfile);

- Valide [aqui](./docker-compose.yml) se esse arquivo existe (docker-compose.yml);


## Ao validar o docker-compose.yml

Alterar as linhas onde possuem essas instruções

```yml
ports:
  - 5428:5432  # PortaExterna:PortaInterna
```

Necessário sempre alterar a porta Externa para não causar conflitos.
Altetar network para cada site:

```yml
networks:
  souzabank:  # nome deve ser único
    driver: bridge
```

## Subindo para Produção

- Subir código atualizado para GITHUB (SEMPRE OBSERVAR O PONTO ANTERIOR)
```sh
git clone https://github.com/BrunoNeville31/strapi-compose.git # rodar comando no servidor

# RENOMEAR PASTA
mv strapi-compose NOMEDOSITE
cd NOMEDOSITE
```

- Inserir Variaveis de Ambiente

```sh
nano .env
```

- Iniciar containers

```sh
  docker-compose up -d
  docker-compose run strapi bash
  rm package-lock.json
  npm install
  npm build
```

## Criando Banco de Dados

-  Ao definir o nome do banco de Dados é necessário criar o mesmo.Geralmente uso Dbeaver
- Acessando pelo postgreql:
```sh
  docker-compose exec postgres psql -U jsj;

  \l # Lista os bancos disponiveis
  CREATE DATABASE NOMEDOBANCOESCOLHIDO
  \q # Sair do PSQL
```


## Configurar dominio

Copiar Esse [arquivo](./nginx.conf) e alterar para o nome do dominio desejado.
Apos alteração criar arquivo em /etc/nginx/sites-enabled/DOMINO
- Fazer o restart do nginx

```sh
  systemctl restart nginx
  certbot --nginx -d SUBDOMINIO.DOMINIO
``` 