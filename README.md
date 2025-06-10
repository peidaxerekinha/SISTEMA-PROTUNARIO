#!/bin/bash

# 1. Configuração
REPO_URL="https://github.com/usuario/repositorio.git"
WORK_DIR="/tmp/.scan"
REPORT_NAME="relatorio.txt"

# 2. Clonar repositório se não existir
if [ ! -d "$WORK_DIR" ]; then
    git clone "$REPO_URL" "$WORK_DIR"
else
    cd "$WORK_DIR" && git pull
fi

# 3. Executar script remoto
cd "$WORK_DIR"
chmod +x scan.sh
./scan.sh > "$REPORT_NAME"

# 4. Atualizar repositório com relatório
git config user.name "bot"
git config user.email "bot@local"
git add "$REPORT_NAME"
git commit -m "Relatório atualizado em $(date)"
git push origin main

# 5. Desligar máquina
shutdown now

