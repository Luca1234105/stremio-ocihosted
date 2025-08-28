FROM python:3.10-slim-buster

WORKDIR /app

# Aggiorna i mirror e installa git
RUN sed -i 's|http://deb.debian.org/debian|http://archive.debian.org/debian|g' /etc/apt/sources.list && \
    sed -i 's|http://deb.debian.org/debian-security|http://archive.debian.org/debian-security|g' /etc/apt/sources.list && \
    sed -i '/deb.*security.debian.org/d' /etc/apt/sources.list && \
    apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

# Clona il repository
RUN git clone --branch main https://github.com/UrloMythus/MammaMia .

# Aggiungi configurazioni
ADD https://raw.githubusercontent.com/nihon77/stremio-selfhosted/refs/heads/main/mammamia/config.json config.json
ADD https://raw.githubusercontent.com/nihon77/stremio-selfhosted/refs/heads/main/mammamia/update_domains.py update_domains.py

# Installa i requirements
RUN pip install --no-cache-dir -r requirements.txt

# Espone la porta
EXPOSE 8080

# Comando di avvio
CMD python update_domains.py && python run.py
