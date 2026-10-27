# Infraestrutura como Código (IaC) — Provisionamento de Servidor Web Apache

## 📌 Descrição do Projeto

Este projeto tem como objetivo automatizar o provisionamento de um servidor web Apache2 e a implantação de uma aplicação web em um ambiente Linux Ubuntu, utilizando Shell Script (Bash).

A solução aplica conceitos de **Infraestrutura como Código (IaC)**, permitindo configurar o ambiente e publicar a aplicação de forma automatizada, padronizada e reproduzível.

O script realiza a atualização do sistema operacional, instala o Apache2 e as dependências necessárias, baixa os arquivos da aplicação de um repositório GitHub e realiza sua publicação no diretório padrão do servidor web.

## 🎯 Objetivos

- Automatizar a atualização dos pacotes do Ubuntu.
- Instalar o servidor web Apache2.
- Instalar as dependências necessárias para a implantação.
- Realizar o download da aplicação hospedada no GitHub.
- Extrair e copiar os arquivos para o diretório do Apache.
- Reduzir tarefas manuais e erros de configuração.
- Padronizar o processo de provisionamento e deploy.

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Finalidade |
|---|---|
| Linux Ubuntu | Sistema operacional |
| Bash | Automação de tarefas |
| Apache2 | Servidor web |
| APT | Gerenciamento de pacotes |
| Wget | Download da aplicação |
| Unzip | Extração de arquivos ZIP |
| GitHub | Repositório do código-fonte |

## 📋 Pré-requisitos

Para executar o projeto, é necessário:

- Servidor ou máquina virtual com Ubuntu.
- Conexão com a internet.
- Permissões administrativas (`root` ou `sudo`).
- Utilitário `wget` instalado.
- Porta TCP 80 liberada para acesso HTTP, caso necessário.

**Observação:** não é necessário instalar o Apache2 manualmente, pois o script realiza sua instalação automaticamente.

## 📂 Estrutura do Projeto

```text
infraestrutura-como-codigo/
│
├── README.md
│
└── script-iac.sh
```

## 💻 Script de Automação

```bash
#!/bin/bash

echo "Atualizando o servidor..."
apt-get update
apt-get upgrade -y
apt-get install apache2 -y
apt-get install unzip -y

echo "Baixando e copiando os arquivos da aplicação..."
cd /tmp
wget https://github.com/denilsonbonatti/linux-site-dio/archive/refs/heads/main.zip

unzip main.zip

cd linux-site-dio-main

cp -R * /var/www/html/
```

## ⚙️ Funcionamento do Script

### 1. Atualização do servidor

```bash
apt-get update
apt-get upgrade -y
```

Atualiza a lista de pacotes disponíveis nos repositórios e instala as atualizações dos pacotes existentes.

### 2. Instalação do Apache2

```bash
apt-get install apache2 -y
```

Instala automaticamente o servidor web Apache2, responsável por disponibilizar a aplicação através do protocolo HTTP.

O parâmetro `-y` confirma automaticamente as solicitações de instalação.

### 3. Instalação do Unzip

```bash
apt-get install unzip -y
```

Instala a ferramenta necessária para descompactar o arquivo ZIP da aplicação.

### 4. Download da aplicação

```bash
cd /tmp
wget https://github.com/denilsonbonatti/linux-site-dio/archive/refs/heads/main.zip
```

Acessa o diretório temporário do Linux e baixa os arquivos da aplicação diretamente do GitHub.

### 5. Extração dos arquivos

```bash
unzip main.zip
```

Descompacta os arquivos da aplicação, criando o diretório `linux-site-dio-main`.

### 6. Publicação no Apache

```bash
cd linux-site-dio-main
cp -R * /var/www/html/
```

Copia os arquivos da aplicação para o diretório padrão de publicação do Apache2.

Após a cópia, o conteúdo estará disponível para ser servido pelo Apache, desde que o serviço esteja em execução.

## 🚀 Como Executar o Projeto

### Passo 1 — Criar o script

```bash
nano script-iac.sh
```

Insira o conteúdo do script e salve o arquivo.

### Passo 2 — Conceder permissão de execução

```bash
chmod +x script-iac.sh
```

### Passo 3 — Executar o script

```bash
sudo ./script-iac.sh
```

O processo realizará automaticamente a atualização do Ubuntu, instalação do Apache2 e Unzip, download e publicação da aplicação.

## 🔍 Validação da Instalação

Após a execução, verifique o status do Apache:

```bash
sudo systemctl status apache2
```

Para verificar se o serviço está ativo:

```bash
sudo systemctl is-active apache2
```

O retorno esperado é:

```text
active
```

Caso o Apache não esteja em execução, utilize:

```bash
sudo systemctl start apache2
```

Para configurar a inicialização automática do Apache:

```bash
sudo systemctl enable apache2
```

Verifique os arquivos publicados:

```bash
ls -la /var/www/html/
```

## 🌐 Acessando a Aplicação

Primeiro, descubra o endereço IP do servidor:

```bash
hostname -I
```

Em seguida, abra o navegador e acesse:

```text
http://IP_DO_SERVIDOR
```

Exemplo:

```text
http://192.168.1.100
```

Se a instalação e a publicação ocorrerem corretamente, a aplicação web será exibida no navegador.

## 🔒 Boas Práticas e Melhorias Futuras

Para aumentar a confiabilidade da automação, recomenda-se:

- Adicionar tratamento de erros ao script.
- Verificar se o `wget` está instalado antes do download.
- Utilizar diretórios temporários exclusivos.
- Evitar conflitos com arquivos existentes durante novas execuções.
- Verificar se o serviço Apache está ativo após a instalação.
- Implementar logs de execução.
- Adicionar validações para confirmar o sucesso do download.
- Fixar uma versão da aplicação para garantir implantações reproduzíveis.
- Configurar HTTPS em ambientes de produção.

## 📊 Resultados Esperados

Ao finalizar a execução do script, o ambiente deverá apresentar:

| Componente | Resultado esperado |
|---|---|
| Ubuntu | Pacotes atualizados |
| Apache2 | Instalado |
| Unzip | Instalado |
| Aplicação | Baixada do GitHub |
| Arquivos web | Copiados para `/var/www/html/` |
| Servidor HTTP | Disponível se o Apache estiver ativo |
| Acesso web | Via endereço IP do servidor |

## 📚 Infraestrutura como Código (IaC)

Infraestrutura como Código é uma abordagem que permite automatizar o provisionamento, a configuração e o gerenciamento de ambientes de infraestrutura utilizando arquivos de código.

Neste projeto, o Shell Script é utilizado para executar automaticamente as tarefas de preparação de um servidor Linux e implantação de uma aplicação web.

**Principais benefícios:**

- **Automação:** reduz a necessidade de executar comandos manualmente.
- **Padronização:** permite repetir o mesmo procedimento em diferentes servidores.
- **Agilidade:** diminui o tempo de preparação do ambiente.
- **Versionamento:** permite armazenar e controlar alterações no GitHub.
- **Manutenção:** facilita a evolução e a documentação do processo.

## 📌 Referências

- [Repositório da aplicação — GitHub](https://github.com/denilsonbonatti/linux-site-dio)
- [Documentação oficial do Ubuntu](https://ubuntu.com/)
- [Documentação do Apache HTTP Server](https://httpd.apache.org/)

---

**Projeto desenvolvido para estudos de Linux, Shell Script, Apache2, automação de servidores e Infraestrutura como Código (IaC).**
