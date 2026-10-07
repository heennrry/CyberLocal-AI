# CyberLocal-AI
CyberLocal AI, un asistente especializado en ciberseguridad. Mi objetivo es ayudarte en actividades legítimas de seguridad, como defensa, análisis, threat hunting, detección, respuesta a incidentes, análisis de malware, análisis forense, hardening, secure coding, auditorías, pentesting autorizado y simulaciones Red Team autorizadas.

//1. En el PC nuevo
Copia esos dos archivos al nuevo PC. Puedes hacerlo con un USB, disco externo o scp.
Por ejemplo, deberían acabar en:
/home/TU_USUARIO/
├── cyberlocal-ai-project.tar.gz
└── ollama_data.tar.gz

//2. Instala Docker en el PC nuevo
Comprueba:
docker --version
docker compose version

//3. Extrae el proyecto
cd ~
tar -xzvf cyberlocal-ai-project.tar.gz
Comprueba:
ls ~/cyberlocal-ai
Deberías ver:
Dockerfile
app/
docker-compose.yml
nginx.conf

4//. Restaura el modelo de Ollama
Primero crea el volumen:
docker volume create ollama_data
Después restaura el backup:
docker run --rm \
  -v ollama_data:/destination \
  -v "$HOME:/backup:ro" \
  alpine \
  tar -xzvf /backup/ollama_data.tar.gz -C /destination
Espera a que termine.

5//. Levanta CyberLocal AI
cd ~/cyberlocal-ai
docker compose up -d
Comprueba:
docker compose ps
Deberías tener:
ollama    Up
app       Up
nginx     Up

6//. Comprueba que has recuperado el modelo
docker exec cyberlocal-ollama ollama list
Debería aparecer:
dagbs/qwen2.5-coder-7b-instruct-abliterated:q4_k_m

7//. Abre la aplicación
En el PC nuevo:
http://localhost

///Feliz Hacking :D
