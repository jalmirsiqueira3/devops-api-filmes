# API de Filmes - Trabalho de Gestão de Configuração

[![Docker](https://badgen.net/badge/icon/Docker?icon=docker&label)](https://hub.docker.com/r/joelmirsiqueira/api-filmes-gc2)

Este é um projeto simples de uma API para gerenciar filmes, desenvolvido como parte da disciplina de Gestão de Configuração de Software 2.

## Execução local

Estas instruções permitirão que você obtenha uma cópia do projeto em operação na sua máquina local para fins de desenvolvimento e teste.

### Pré-requisitos

O que você precisa para instalar o software:

*   [Node.js](https://nodejs.org/en/)
*   [npm](https://www.npmjs.com/) (geralmente vem com o Node.js)

### Instalação e Execução (local)

Um passo a passo que te diz como ter um ambiente de desenvolvimento rodando:

**1. Clone o repositório:**

```bash
git clone https://github.com/jalmirsiqueira3/devops-api-filmes.git
```

**2. Navegue até o diretório da API:**
    
```bash
cd api-filmes
```

**3. Instale as dependências do projeto:**
    
```bash
npm install
```

**4. Faça build do projeto**
    
```bash
npm run build
```

**5. Inicie o servidor:**
    
```bash
npm start
```

O servidor estará rodando em `http://localhost:3000` (ou na porta que você configurar).

## Infraestrutura com Vagrant e Ansible

### Requisitos:

- VirtualBox
- Vagrant
- Ansible (será instalado na VM)

### Passo a Passo:
**1. Iniciar as máquinas virtuais:**

No terminal da máquina hospedeira execute esse comando na pasta `api-filmes/vagrant` do projeto, ele vai baixar a Box necessária, configurar as redes privadas, sincronizar as pastas e instalar as dependências automaticamente.

```bash
vagrant up
```

**2. Verificar Status das VMs:**

Para ter a certeza que ambas as máquinas estão rodando, checar o status delas.

```bash
vagrant status
```

**3. Acessar a VM1:**

Entrar na máquina (VM1) via SSH:

```bash
vagrant ssh vm1
```

**4. Navegue para a pasta `/vagrant`:**

Após entrar na VM1, navegue para a pasta `/vagrant` com o comando cd:

```bash
cd /vagrant
```

**5. Execute o Playbook do Ansible:**

```bash
ansible-playbook -i inventory.ini configura-node.yaml
```

Confirme que quer continuar a conexão (caso seja solicitado) digite: `yes` e precione Enter.

O playbook realiza a configuração do servidor, faz o clone do repositório da aplicação e executa a API utilizando Docker.

**6. Teste da Aplicação:**

Para verificar se a aplicação está funcionando corretamente, execute na VM1:

```bash
curl http://192.168.56.11:3000/filmes
```

ou

```bash
wget -qO- http://192.168.56.11:3000/filmes
```
se a configuração foi realizada com sucesso, a API retornará a lista de filmes em formato JSON.


## Monitoramento com NetData

### Ferramenta Utilizadas (na VM):

- Netdata
- mailutils
- stress-ng

### Passo a passo:

Certifique-se de ainda está na VM1 e com teminal na pasta `/vagrant`.

**1. Execute o Playbook de monitoramento:**

```bash
ansible-playbook -i inventory.ini data/configurar-monitoramento.yml
```

O playbook instala as ferramentas e faz as configurações necessárias para o monitoramento.

**2. Sair da VM1:**

Para testar o alerta é necessário sair da VM1 e acessar a VM2 via ssh. Para sair da VM1 execute:

```bash
exit
```

**3. Acessar a VM2:**

Para acessar a VM2 execute:

```bash
vagrant ssh vm2
```

**3. Testando o alerta:**

Execute esse comando para utilizar o stress-ng:

```bash
stress-ng --cpu 4 --cpu-load 85 --timeout 15s
```

O consumo de CPU ultrapassará 80%.

O alerta poderá ser visualizado no painel web do Netdata acessando http://192.168.56.11:19999 pelo seu navegador web da maquina host.

**7. Alertas:**

Foi configurado um alerta para:

- CPU acima de 80%

Quando o limite for atingido, o Netdata enviará um e-mail para o destinatário configurado em:

`/etc/netdata/health_alarm_notify.conf`

## 📖 Rotas da API

A API possui as seguintes rotas:

*   **GET `/filmes`**: Retorna uma lista de todos os filmes.
*   **POST `/filmes`**: Adiciona um novo filme à lista. O corpo da requisição deve ser um JSON com os detalhes do filme. Ex: `{"titulo": "O Poderoso Chefão", "ano": 1972}`.

## 🌊 Fluxo de Trabalho (Workflow)

Este projeto utiliza o **GitLab Flow** como fluxo de trabalho de desenvolvimento. É um fluxo mais simples que o Git Flow, baseado em *feature branches* e ambientes múltiplos (produção, pré-produção, etc.), é mais adequado do que o github flow para projetos que tem pretensão de escalar rapidamente e que é mantido por mais de um dev.

## Estudantes
Joelmir & 
Jalmir