#Use an official Python runtime as a parent image
FROM python:3.10-slim-buster

# Set the working directory in the container to /app
WORKDIR /app

# Install git
RUN sed -i 's|http://deb.debian.org/debian|http://archive.debian.org/debian|g' /etc/apt/sources.list && \
    sed -i 's|http://deb.debian.org/debian-security|http://archive.debian.org/debian-security|g' /etc/apt/sources.list && \
    sed -i '/deb.*security.debian.org/d' /etc/apt/sources.list

# Clone the repository
RUN git clone --branch main https://github.com/UrloMythus/MammaMia .

# Add Refreshed sites config by https://pastebin.com/raw/VrC4D65J (thanks!!!)
ADD https://raw.githubusercontent.com/nihon77/stremio-selfhosted/refs/heads/main/mammamia/config.json config.json
ADD https://raw.githubusercontent.com/nihon77/stremio-selfhosted/refs/heads/main/mammamia/update_domains.py update_domains.py
# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Expose the port, for now default is 8080 cause it's the only one really allowed by HuggingFace
EXPOSE 8080

# Run run.py when the container launches
#CMD ["python", "run.py"]
CMD python update_domains.py && python run.py
