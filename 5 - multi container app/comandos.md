criando rede

1. docker network create goals-net

frontend

1. cd frontend
2. docker build -t goals-react .
3. docker run --name goals-front --rm -p 3000:3000 -it goals-react

- aqui precisa expor a porta pq o localhost precisa acessar a porta 3000 do container e não precisa de network pq nao tem comunicacao entre containers, já que o localhost que vai requisitar o backend

backend

1. cd backend
2. docker build -t goals-node .
3. docker run --name goals-backend --rm -d -p 80:80 --network goals-net -v logs:/app/logs goals-node

- aqui precisa expor a porta para o localhost(frontend) conseguir acessar a aplicação rodando na porta 80 do container

mongo

1. docker run --name mongodb --rm -d --network goals-net -v data:/data/db -e MONGO_INITDB_ROOT_USERNAME=vitor -e MONGO_INITDB_ROOT_PASSWORD=secret mongo

- aqui nao precisa expor a porta pq os containers do backend e mongodb estao na mesma rede
- named volumes(-v data:/data/db) sao para mapear os dados do mongo(/data/db) especificados na documentacao da imagem para um volume no pc criado pelo docker, assim nao perdemos os dados quando paramos e removemos o container
