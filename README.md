🚀 Projeto — Deploy Completo em Kubernetes

Aplicação composta por Frontend (React), Backend (Flask) e Banco de Dados PostgreSQL, implantada em Kubernetes utilizando Deployments, StatefulSet, ConfigMaps, Secrets, PVC e Ingress.

🧩 Componentes da Aplicação
🔵 Frontend (React)

Servido via Nginx

Variável de ambiente: VITE_API_URL

Exposto via NodePort na porta 30080

🔴 Backend (Flask)

API REST (GET e POST)

Conecta ao PostgreSQL utilizando variáveis de ambiente

Exposto via NodePort na porta 30081

🟢 Banco de Dados (PostgreSQL)

Implantado como StatefulSet

Volume persistente (PVC)

Credenciais gerenciadas via Secret

📦 Pré-requisitos

Instalar Docker:

sudo apt update
sudo apt install -y docker.io
sudo systemctl enable --now docker
sudo usermod -aG docker $USER
newgrp docker


Instalar Minikube:

curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube


Instalar kubectl:

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/

🚀 Como Executar a Aplicação
1️⃣ Iniciar o Minikube
minikube start --driver=docker --cpus=2 --memory=3072

2️⃣ Clonar o Repositório
git clone https://github.com/MatheusCMaia/projeto-k8s-deploy.git
cd projeto-k8s-deploy

3️⃣ Criar os Namespaces
kubectl apply -f namespace.yaml

4️⃣ Aplicar ConfigMap, Secret e PVC
kubectl apply -f backend/configmap.yaml
kubectl apply -f database/secret.yaml
kubectl apply -f database/pvc.yaml

5️⃣ Subir o Banco de Dados
kubectl apply -f database/statefulset.yaml

Aguarde 10–20 segundos até o banco inicializar.

6️⃣ Subir Backend e Frontend
kubectl apply -f backend/deployment.yaml
kubectl apply -f frontend/deployment.yaml

7️⃣ (Opcional) Aplicar Ingress
kubectl apply -f ingress/ingress.yaml

🔍 Verificar Status da Aplicação

Ver Pods
kubectl get pods -n app-ns
kubectl get pods -n db-ns

Ver Serviços
kubectl get svc -n app-ns

🌐 Acesso à Aplicação
Frontend (React)
http://localhost:30080/

Backend (Flask)
http://localhost:30081/api/

🧪 Testes da API
Listar mensagens:
curl http://localhost:30081/api/messages

Inserir mensagem:
curl -X POST http://localhost:30081/api/messages \
     -H "Content-Type: application/json" \
     -d '{"conteudo": "Mensagem via Kubernetes"}'

📚 Tecnologias Utilizadas

- Kubernetes
- Docker
- Minikube
- React
- Flask
- PostgreSQL
- ConfigMaps
- Secrets
- Persistent Volumes (PVC)
- StatefulSet
- NodePort Services
- Ingress (opcional)

