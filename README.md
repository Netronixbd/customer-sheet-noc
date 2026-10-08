# NOC Client & Bandwidth Tracker (Debian 12 + Docker Compose)

## Deploy
    sudo apt update && sudo apt install -y docker.io docker-compose-plugin
    cp .env.example .env     # fill DB_PASSWORD, JWT_SECRET, ADMIN_PASSWORD
    # generate FERNET_KEY (needed for router password encryption):
    docker run --rm python:3.12-slim sh -c "pip -q install cryptography && python -c 'from cryptography.fernet import Fernet;print(Fernet.generate_key().decode())'"
    docker compose up -d --build
Open http://SERVER_IP/  (login with ADMIN_USER / ADMIN_PASSWORD). API docs: /api/docs

Back up FERNET_KEY and the pgdata volume - without the key, stored router passwords cannot be decrypted.
SSL: mount certs into nginx, add a 443 server block, publish 443.
