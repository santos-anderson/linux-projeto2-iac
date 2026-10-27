# Infraestrutura como Código (IaC) — Deploy de Aplicação Web

## 📌 Descrição do Projeto

Este projeto tem como objetivo automatizar a atualização de um servidor Linux e a implantação de uma aplicação web utilizando um script Bash.

A solução segue os princípios de **Infraestrutura como Código (IaC)**, permitindo automatizar tarefas de configuração e implantação, reduzindo a necessidade de intervenções manuais.

O script realiza a atualização dos pacotes do sistema operacional, instala a ferramenta `unzip`, baixa os arquivos da aplicação diretamente de um repositório GitHub e copia os arquivos para o diretório padrão de publicação do servidor Apache.

## 🎯 Objetivo

Automatizar o processo de implantação de uma aplicação web em um servidor Linux Ubuntu, garantindo:

- Padronização do processo de implantação.
- Redução de erros operacionais.
- Agilidade na disponibilização da aplicação.
- Facilidade de manutenção e reprodução do ambiente.
- Automatização de tarefas administrativas.

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Finalidade |
|---|---|
| Linux Ubuntu | Sistema operacional do servidor |
| Bash | Automação das tarefas |
| Apache2 | Servidor web para hospedagem da aplicação |
| APT | Gerenciamento de pacotes |
| Wget | Download dos arquivos |
| Unzip | Extração de arquivos ZIP |
| GitHub | Repositório da aplicação |

## 📋 Pré-requisitos

Antes de executar o script, é necessário:

- Possuir um servidor Ubuntu com acesso à internet.
- Ter permissões administrativas (`root` ou `sudo`).
- Ter o Apache2 instalado e configurado.
- Ter o `wget` instalado.
- Garantir que o diretório `/var/www/html/` esteja disponível.

**Observação:** o script não instala nem configura o Apache2. Esse serviço deve estar preparado antes da implantação.

## 📂 Estrutura do Projeto

```text
infraestrutura-como-codigo/
│
├── README.md
│
└── script-iac.sh
```

## 💻 Script de Automação

O script utilizado para realizar o deploy da aplicação é:

```bash
#!/bin/bash

echo "Atualizando o servidor..."
apt-get update
apt-get upgrade -y
apt-get install unzip -y

echo "Baixando e copiando os arquivos da aplicação..."
cd /tmp
wget https://github.com/denilsonbonatti/linux-site-dio/archive/refs/heads/main.zip

unzip main.zip

cd linux-site-dio-main

cp -R * /var/www/html/
```

## ⚙️ Funcionamento do Script

**1. Atualização do servidor**

```bash
apt-get update
apt-get upgrade -y
```

Atualiza a lista de pacotes disponíveis e instala as atualizações dos pacotes já existentes no sistema.

**2. Instalação de dependências**

```bash
apt-get install unzip -y
```

Instala o utilitário `unzip`, necessário para extrair os arquivos da aplicação.

**3. Download da aplicação**

```bash
cd /tmp
wget https://github.com/denilsonbonatti/linux-site-dio/archive/refs/heads/main.zip
```

Acessa o diretório temporário do sistema e realiza o download da aplicação hospedada no GitHub.

**4. Extração dos arquivos**

```bash
unzip main.zip
```

Extrai o conteúdo do arquivo ZIP para o diretório `linux-site-dio-main`.

**5. Publicação da aplicação**

```bash
cd linux-site-dio-main
cp -R * /var/www/html/
```

Copia os arquivos da aplicação para o diretório de publicação padrão do Apache.

## 🚀 Como Executar

**Passo 1 — Criar o arquivo do script**

```bash
nano script-iac.sh
```

Copie o conteúdo do script, salve e feche o editor.

**Passo 2 — Conceder permissão de execução**

```bash
chmod +x script-iac.sh
```

**Passo 3 — Executar o script**

```bash
sudo ./script-iac.sh
```

**Passo 4 — Validar a implantação**

Após a execução, verifique se os arquivos foram copiados:

```bash
ls -la /var/www/html/
```

Verifique também o status do Apache:

```bash
sudo systemctl status apache2
```

## 🌐 Acessando a Aplicação

Com o Apache em execução e a porta HTTP liberada, abra um navegador e acesse:

```text
http://IP_DO_SERVIDOR
```

Exemplo:

```text
http://192.168.1.100
```

A aplicação deverá ser exibida caso os arquivos tenham sido publicados corretamente.

## 🔒 Boas Práticas e Melhorias Futuras

Para tornar a automação mais robusta, recomenda-se:

- Implementar tratamento de erros durante a execução.
- Validar a disponibilidade dos diretórios antes da cópia.
- Verificar se o Apache está instalado e em execução.
- Utilizar diretórios temporários exclusivos para evitar conflitos.
- Implementar logs para rastrear as etapas do deploy.
- Validar os arquivos baixados antes da publicação.
- Utilizar versões específicas da aplicação para garantir implantações reproduzíveis.

## 📊 Resultados Esperados

Ao executar o script com sucesso, espera-se:

- Servidor Ubuntu com pacotes atualizados.
- Ferramenta `unzip` instalada.
- Arquivos da aplicação baixados e extraídos.
- Conteúdo publicado em `/var/www/html/`.
- Aplicação acessível pelo navegador, desde que o Apache esteja configurado e em funcionamento.

## 📚 Conceito de Infraestrutura como Código

Infraestrutura como Código (IaC) é uma prática que permite automatizar a configuração e o gerenciamento de infraestrutura por meio de arquivos de código.

Neste projeto, o Bash é utilizado para automatizar atividades de preparação do servidor e implantação da aplicação, demonstrando uma abordagem inicial de automação de infraestrutura.

Entre os benefícios estão a padronização, a redução de tarefas manuais e a possibilidade de versionar os procedimentos utilizados.

## 📌 Referências

- [Repositório da aplicação — GitHub](https://github.com/denilsonbonatti/linux-site-dio)
- [Documentação Ubuntu](https://ubuntu.com/)
- [Documentação Apache HTTP Server](https://httpd.apache.org/)

---

**Projeto desenvolvido para estudos de Linux, Shell Script, automação e Infraestrutura como Código (IaC).**
