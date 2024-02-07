# cplusplus---unrealengine
# Use a base image com as dependências do Ubuntu
FROM ubuntu:latest

# Atualize os pacotes e instale as dependências
RUN apt-get update && apt-get install -y \
    build-essential \
    git \
    cmake \
    clang \
    unzip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Baixe a Unreal Engine (substitua o link pelo link real)
RUN mkdir /unreal_engine && cd /unreal_engine && \
    git clone https://github.com/EpicGames/UnrealEngine.git && \
    cd UnrealEngine && \
    ./Setup.sh && \
    ./GenerateProjectFiles.sh && \
    make

# Defina o diretório de trabalho
WORKDIR /workspace

# Exemplo de como adicionar seu código fonte
# COPY . /workspace

# Exemplo de como compilar seu projeto
# RUN cmake . && make

# Comando padrão ao iniciar o contêiner
CMD ["bash"]
