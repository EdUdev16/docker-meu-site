# docker-meu-site

Laboratório de estudo de Docker: uma página web servida por nginx e um banco PostgreSQL, orquestrados com Docker Compose.

## O que demonstra
- **Dockerfile** próprio: imagem baseada em `nginx` com uma página HTML personalizada.
- **Docker Compose**: sobe o site e o banco com um único comando.
- **Volume** (`dados-banco`): os dados do Postgres sobrevivem à remoção do container.
- **Rede**: os serviços se encontram pelo nome (`site` acessa `banco`), sem configurar rede manualmente.
- **Segredos fora do código**: a senha do banco vem do arquivo `.env`, que não vai para o Git.

## Como rodar
Requisitos: Docker com o plugin Compose.

```bash
cp .env.example .env        # edite e troque a senha
docker compose up -d --build
```

Abra http://localhost:8080.

Verificar a comunicação entre os serviços:
```bash
docker compose exec site getent hosts banco
```

Derrubar (mantém o volume) ou derrubar apagando os dados:
```bash
docker compose down
docker compose down -v
```

## Estrutura
| Arquivo | Função |
|---|---|
| `Dockerfile` | Monta a imagem do site |
| `index.html` | Página servida pelo nginx |
| `compose.yaml` | Define os serviços, o volume e a rede |
| `.env.example` | Modelo das variáveis de ambiente |

## Autor
Eduardo Sena Santos Gomes · estudante de ADS · em transição para DevOps.
