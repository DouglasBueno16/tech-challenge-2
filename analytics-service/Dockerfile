# syntax=docker/dockerfile:1

#iniciando a imagem
FROM python:3.11-slim

# Criando usuario

RUN groupadd -r dockeruser && useradd -r -g dockeruser -d /home/dockeruser -m -s /usr/sbin/nologin dockeruser

# Definição de diretorio de trabalho
WORKDIR /app

# Copiar arquivos
COPY app.py .
COPY requirements.txt .

# Instalar dependências
RUN pip install setuptools
RUN pip install --no-cache-dir -r requirements.txt

# Ajustar permissões para o usuário 
RUN chown -R dockeruser:dockeruser /app 

# Trocar para o usuário 

USER dockeruser

# Expondo porta

EXPOSE 8005

# Comando de inicialização
CMD ["gunicorn", "--bind", "0.0.0.0:8005", "app:app"]
