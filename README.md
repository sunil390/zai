# zai

## Dify

1. git clone https://github.com/langgenius/dify.git --branch 0.15.3
2. cd dify/docker
3. cp .env.example .env
4. docker compose up -d
5. docker compose ps

## Dify Upgrade
1. cd dify/docker
2. docker compose down
3. git pull origin main
4. docker compose pull
5. docker compose up -d

## SSL

1. DIFY_HOST="www.dify.znext.ai"
2. openssl req -x509 -nodes -days 3650 -newkey rsa:4096 -out dify.crt -keyout dify.key -subj "/CN=${DIFY_HOST}/O=${DIFY_HOST}" -addext "subjectAltName = DNS:${DIFY_HOST}"
