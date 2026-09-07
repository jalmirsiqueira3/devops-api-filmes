# 🎬 DevOps API Filmes

[![CI Docker](https://github.com/jalmirsiqueira3/devops-api-filmes/actions/workflows/ci-docker.yaml/badge.svg)](https://github.com/jalmirsiqueira3/devops-api-filmes/actions/workflows/ci-docker.yaml)
[![CI ESLint](https://github.com/jalmirsiqueira3/devops-api-filmes/actions/workflows/ci-eslint.yaml/badge.svg)](https://github.com/jalmirsiqueira3/devops-api-filmes/actions/workflows/ci-eslint.yaml)

[![Node.js](https://img.shields.io/badge/Node.js-24%2B-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0%2B-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Express](https://img.shields.io/badge/Express-5.0%2B-000000?logo=express&logoColor=white)](https://expressjs.com/)
[![Vitest](https://img.shields.io/badge/Vitest-Testing-6E9F18?logo=vitest&logoColor=white)](https://vitest.dev/)
[![ESLint](https://img.shields.io/badge/ESLint-Code%20Quality-4B32C3?logo=eslint&logoColor=white)](https://eslint.org/)
[![Prettier](https://img.shields.io/badge/Prettier-Code%20Formatter-F7B93E?logo=prettier&logoColor=black)](https://prettier.io/)

[![Docker](https://img.shields.io/badge/Docker-Containerization-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![Ansible](https://img.shields.io/badge/Ansible-Automation-EE0000?logo=ansible&logoColor=white)](https://www.ansible.com/)
[![Vagrant](https://img.shields.io/badge/Vagrant-Infrastructure-1868F2?logo=vagrant&logoColor=white)](https://www.vagrantup.com/)
[![VirtualBox](https://img.shields.io/badge/VirtualBox-7.0%2B-183A61?logo=virtualbox&logoColor=white)](https://www.virtualbox.org/)
[![Netdata](https://img.shields.io/badge/Netdata-Monitoring-00AB44?logo=netdata&logoColor=white)](https://www.netdata.cloud/)

Projeto desenvolvido para a disciplina de **Gestão de Configuração de Software 2**, com foco na aplicação prática de conceitos e ferramentas de **DevOps, automação de infraestrutura, conteinerização e monitoramento**.

A aplicação consiste em uma API REST simples para gerenciamento de filmes, utilizada como base para a implementação de uma infraestrutura automatizada utilizando **Docker, Vagrant e Ansible**, além de monitoramento e alertas com **Netdata**.

---

## 🎯 Sobre o Projeto

O objetivo principal do projeto foi aplicar, de forma prática, conceitos relacionados ao processo de desenvolvimento e operação de aplicações.

Ao longo do desenvolvimento, diferentes tecnologias foram incorporadas ao projeto, permitindo construir um fluxo que vai desde a execução local da API até o provisionamento automatizado da infraestrutura e o monitoramento da aplicação.

O projeto contempla:

* Desenvolvimento de uma API REST com Node.js.
* Conteinerização da aplicação utilizando Docker.
* Criação e gerenciamento de máquinas virtuais utilizando Vagrant.
* Provisionamento e configuração automatizada utilizando Ansible.
* Monitoramento da infraestrutura utilizando Netdata.
* Configuração de alertas para utilização de CPU.
* Testes de carga utilizando `stress-ng`.
* Organização do desenvolvimento utilizando GitLab Flow.

---

## 🛠️ Tecnologias Utilizadas

### Desenvolvimento

* **Node.js**
* **JavaScript/TypeScript**
* **npm**

### DevOps e Infraestrutura

* **Docker**
* **Vagrant**
* **Ansible**
* **VirtualBox**

### Monitoramento

* **Netdata**
* **stress-ng**
* **mailutils**

### Versionamento

* **Git**
* **GitLab Flow**

---

## ✨ Destaques

* API REST desenvolvida com Node.js, TypeScript e Express.
* Testes automatizados com Vitest e cobertura de código.
* Imagem Docker para execução reproduzível.
* Provisionamento automatizado com Vagrant e Ansible.
* Monitoramento de infraestrutura com Netdata.
* Pipeline de integração contínua com GitHub Actions.

---

## 🏗️ Arquitetura

A infraestrutura foi organizada utilizando duas máquinas virtuais provisionadas pelo Vagrant.

```text
                         ┌─────────────────────┐
                         │    Máquina Host     │
                         │                     │
                         │      Vagrant        │
                         └──────────┬──────────┘
                                    │
                     ┌──────────────┴──────────────┐
                     │                             │
              ┌──────▼──────┐               ┌──────▼──────┐
              │     VM1     │               │     VM2     │
              │             │               │             │
              │   Ansible   │               │   Netdata   │
              │   Docker    │               │  stress-ng  │
              │     API     │               │             │
              └──────┬──────┘               └──────┬──────┘
                     │                             │
                     └────────── Monitoramento ────┘
```

### Responsabilidade das ferramentas

| Tecnologia      | Responsabilidade                            |
| --------------- | ------------------------------------------- |
| **Node.js**     | Desenvolvimento da API                      |
| **Docker**      | Conteinerização da aplicação                |
| **Vagrant**     | Criação e gerenciamento das VMs             |
| **Ansible**     | Provisionamento e configuração automatizada |
| **Netdata**     | Monitoramento da infraestrutura             |
| **stress-ng**   | Simulação de carga para testes              |
| **GitLab Flow** | Organização do fluxo de desenvolvimento     |

---

## 📂 Estrutura do Projeto

```text
devops-api-filmes/
│
├── 📁 vagrant/
│   ├── Vagrantfile
│   ├── inventory.ini
│   ├── configura-node.yaml
│   └── 📁 data/
│       └── configurar-monitoramento.yml
│
├── 📁 src/
│
├── 📁 tests/
│
├── 📄 Dockerfile
├── 📄 package.json
├── 📄 package-lock.json
└── 📄 README.md
```

### Principais componentes

* **`vagrant/`** — arquivos relacionados à criação e configuração das máquinas virtuais.
* **`vagrant/data/`** — playbook utilizado para configuração do monitoramento.
* **`src/`** — código-fonte da aplicação.
* **`tests/`** — testes automatizados do projeto.
* **`Dockerfile`** — definição da imagem utilizada para executar a API.
* **`package.json`** — dependências e scripts da aplicação.
* **`README.md`** — documentação do projeto.

---

## 🐳 Conteinerização com Docker

A API foi configurada para ser executada utilizando **Docker**, permitindo que a aplicação seja executada em um ambiente isolado e reproduzível.

A imagem da aplicação é construída a partir do `Dockerfile` e posteriormente utilizada pela infraestrutura provisionada pelo Ansible.

Essa abordagem permite separar a aplicação do ambiente de execução e facilita sua implantação em diferentes máquinas.

---

## 🖥️ Infraestrutura com Vagrant e Ansible

Para simular um ambiente de infraestrutura real, foram utilizadas duas máquinas virtuais gerenciadas pelo **Vagrant**.

O **Ansible** é utilizado para automatizar a configuração dessas máquinas, evitando a necessidade de realizar manualmente cada etapa de instalação e configuração.

O playbook responsável pela configuração da aplicação realiza tarefas como:

* Configuração do ambiente.
* Instalação das dependências necessárias.
* Clone do repositório da aplicação.
* Construção da imagem Docker.
* Execução da API em container.

### Requisitos

Para executar a infraestrutura localmente, é necessário possuir:

* [VirtualBox](https://www.virtualbox.org/)
* [Vagrant](https://www.vagrantup.com/)
* [Git](https://git-scm.com/)

O Ansible será utilizado dentro da infraestrutura provisionada.

### Inicializando as máquinas virtuais

Na máquina hospedeira, execute o comando a partir do diretório `vagrant`:

```bash
vagrant up
```

O Vagrant irá criar as máquinas virtuais, configurar as redes privadas, sincronizar os diretórios e preparar o ambiente.

Para verificar o estado das máquinas:

```bash
vagrant status
```

---

## ⚙️ Configuração da Aplicação com Ansible

Após iniciar as máquinas, acesse a VM1:

```bash
vagrant ssh vm1
```

Navegue até o diretório compartilhado:

```bash
cd /vagrant
```

Execute o playbook:

```bash
ansible-playbook -i inventory.ini configura-node.yaml
```

Caso seja solicitada confirmação para estabelecer a conexão SSH, confirme digitando:

```text
yes
```

O playbook realiza automaticamente a configuração do ambiente, incluindo o clone da aplicação, construção da imagem Docker e execução da API.

### Testando a API

Após a configuração, a aplicação pode ser testada através da VM1:

```bash
curl http://192.168.56.11:3000/filmes
```

ou:

```bash
wget -qO- http://192.168.56.11:3000/filmes
```

Se a configuração foi realizada corretamente, a API deverá retornar a lista de filmes em formato JSON.

---

## 📊 Monitoramento com Netdata

O projeto utiliza **Netdata** para monitorar os recursos da infraestrutura.

Foram configurados:

* Monitoramento de utilização da CPU.
* Limite de utilização de CPU.
* Alertas automáticos.
* Envio de notificações por e-mail.

### Ferramentas utilizadas

* Netdata
* mailutils
* stress-ng

### Configuração do monitoramento

A partir da VM1, no diretório `/vagrant`, execute:

```bash
ansible-playbook -i inventory.ini data/configurar-monitoramento.yml
```

O playbook realiza a instalação e configuração das ferramentas necessárias para o monitoramento.

---

## 🔥 Teste de carga

Para validar o funcionamento do monitoramento e dos alertas, foi utilizado o `stress-ng` para gerar carga artificial de CPU.

Primeiro, saia da VM1:

```bash
exit
```

Acesse a VM2:

```bash
vagrant ssh vm2
```

Execute:

```bash
stress-ng --cpu 4 --cpu-load 85 --timeout 15s
```

O comando gera uma carga de CPU superior ao limite configurado para o alerta.

O monitoramento pode ser acompanhado através da interface web do Netdata:

```text
http://192.168.56.11:19999
```

O endereço pode ser acessado pelo navegador da máquina hospedeira.

### 🚨 Alertas

Foi configurado um alerta para:

* **CPU acima de 80%**

Quando o limite é atingido, o Netdata realiza o envio de um e-mail para o destinatário configurado no arquivo:

```text
/etc/netdata/health_alarm_notify.conf
```

---

## 🧪 Testes

O projeto também possui testes automatizados para validar o comportamento da aplicação.

Os testes fazem parte do processo de desenvolvimento e ajudam a garantir que alterações realizadas na API não introduzam regressões.

Para executar os testes:

```bash
npm test
```

Para gerar o relatório de cobertura:

```bash
npm run coverage
```

---

## 📖 API

A aplicação disponibiliza endpoints para gerenciamento de filmes.

### GET `/filmes`

Retorna a lista de filmes cadastrados.

Exemplo:

```http
GET /filmes
```

Resposta `200 OK`:

```json
[
  {
    "id": 1,
    "titulo": "O Poderoso Chefão",
    "ano": 1972
  }
]
```

### POST `/filmes`

Adiciona um novo filme.

Exemplo:

```http
POST /filmes
Content-Type: application/json
```

Corpo da requisição:

```json
{
  "titulo": "O Poderoso Chefão",
  "ano": 1972
}
```

Resposta `201 Created`:

```json
{
  "id": 1,
  "titulo": "O Poderoso Chefão",
  "ano": 1972
}
```

### DELETE `/filmes/:id`

Remove um filme pelo identificador.

Exemplo:

```http
DELETE /filmes/1
```

Resposta `204 No Content` quando o filme é removido. Caso o identificador não exista, a API retorna `404 Not Found`.

---

## 🔄 Fluxo de Trabalho

O projeto utiliza o **GitLab Flow** como estratégia de organização do desenvolvimento.

O fluxo foi utilizado para separar o desenvolvimento de novas funcionalidades do código principal, permitindo maior organização durante a implementação das diferentes etapas do projeto.

A adoção do fluxo também possibilitou trabalhar com branches e integração das alterações ao longo do desenvolvimento.

---

## 🚀 Execução Local

Além da infraestrutura virtualizada, a API pode ser executada diretamente na máquina local para desenvolvimento e testes.

### Pré-requisitos

* [Node.js](https://nodejs.org/)
* [npm](https://www.npmjs.com/)

### 1. Clone o repositório

```bash
git clone https://github.com/jalmirsiqueira3/devops-api-filmes.git
```

### 2. Acesse o projeto

```bash
cd devops-api-filmes
```

### 3. Instale as dependências

```bash
npm install
```

### 4. Faça o build

```bash
npm run build
```

### 5. Inicie o servidor

```bash
npm start
```

A API estará disponível em:

```text
http://localhost:3000
```

---

## 🎓 Contexto Acadêmico

Projeto desenvolvido para a disciplina de **Gestão de Configuração de Software 2**, com o objetivo de aplicar conceitos de automação, gerenciamento de configuração, infraestrutura e práticas de DevOps.

O projeto foi desenvolvido em dupla e evoluiu incrementalmente conforme novas tecnologias e requisitos eram introduzidos na disciplina.

---

## 👨‍💻 Autores

### Jalmir Siqueira

* [GitHub](https://github.com/jalmirsiqueira3)
* [LinkedIn](https://www.linkedin.com/in/jalmir-siqueira-a3221828a)

### Joelmir Siqueira

* [GitHub](https://github.com/joelmirsiqueira)
* [LinkedIn](https://www.linkedin.com/in/joelmirsilva-de-siqueira-815a81332)