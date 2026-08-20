[![Cypress Tests](https://github.com/FabioGVL/CorreiosAPI/actions/workflows/CorreiosAPIAutomation.yml/badge.svg)](https://github.com/FabioGVL/CorreiosAPI/actions/workflows/CorreiosAPIAutomation.yml)

# Automação de Testes de API - Consulta de CEP (B2W / Integração)

## Escopo do Produto

Este documento detalha a estratégia de automação de testes para a API de consulta de CEPs (utilizando o endpoint de integração B2W/Americanas). O foco principal é validar a precisão dos dados geográficos retornados e a resiliência do back-end diante de entradas malformadas ou inexistentes, garantindo uma integração segura para serviços de logística e checkout.

## Escopo do Teste

A estratégia foca em validar a integridade geográfica dos dados de endereçamento e o comportamento do sistema perante cenários de erro e resiliência de parâmetros.

* **Mapeamento de Features:** Consulta de Logradouro (busca de endereços através de códigos postais - CEP) e Base de Dados Geográfica (integração com os registros oficiais de endereçamento brasileiro).
* **Features Testadas:** Consulta de CEPs Válidos (validação de retorno 200 OK para endereços de diferentes regiões do Brasil) e Tratamento de CEPs Inexistentes (verificação de status code e mensagem de erro para requisições inválidas).
* **Massa de Dados:** Conjunto de parâmetros com CEPs reais diversificados e strings alfanuméricas para testes de erro e resiliência.
* **Tipos de Testes:**
  * **Testes de Funcionalidade:** Garantir que os endpoints da API estão operando e retornando os dados conforme o esperado.
  * **Testes de Integração:** Garantir que a comunicação entre o cliente e o servidor ocorra sem falhas de protocolo ou conexão.
  * **Testes de Contrato:** Verificar se a estrutura dos dados retornados (JSON) segue o padrão técnico esperado.

## Arquitetura e Estrutura

O projeto foi organizado para garantir a separação entre a lógica de teste e a configuração das requisições, facilitando a manutenção e a escalabilidade.

- **Padrão de Projeto:** Estrutura de testes baseada no Cypress para automação de requisições à API, utilizando `cy.request()` e `failOnStatusCode: false` para permitir a inspeção detalhada de payloads de erro. A estratégia contempla validação regional por meio de CEPs reais de todas as regiões do Brasil, verificando campos como `address`, `city` e `state`, além de cenários negativos e de resiliência envolvendo dados alfanuméricos, caracteres especiais, espaços e CEPs com quantidade de caracteres acima ou abaixo de 8. Também são realizadas validações de Status Codes, diferenciando erros de rota (`404 Not Found`) de falhas de processamento interno (`500 Internal Server Error`).
- **Tecnologias e Ambiente:** `Cypress` | `JavaScript (ES6+)` | `Node.js` | `Git Actions` | `Git` | `Windows 11` | `Chrome` | `Postman`
---

# Passos para Configurar e Reproduzir o Projeto

Siga o guia abaixo para clonar, configurar o ambiente e executar a suíte de testes automatizados em sua máquina local.

---

## Pré-requisitos

Certifique-se de possuir as seguintes ferramentas instaladas em seu ambiente:

- [Node.js](https://nodejs.org/) — versão 20.15.0 ou superior recomendada
- [Git](https://git-scm.com/)
- Editor de código de sua preferência, como o [VS Code](https://code.visualstudio.com/)

---

## Obtendo o Código do Projeto

Você pode obter os arquivos do projeto de duas formas.

### Opção A: Clonando via Git (Recomendado)

Abra o terminal e execute o comando abaixo para clonar o repositório:

```bash
git clone https://github.com/FabioGVL/CorreiosAPI.git
```

Em seguida, navegue para dentro da pasta do projeto:

```bash
cd CorreiosAPI
```

### Opção B: Baixando via ZIP

1. Acesse a página do repositório no GitHub.
2. Clique no botão verde **Code**.
3. Selecione **Download ZIP**.
4. Extraia o conteúdo do arquivo compactado em uma pasta no seu computador.
5. Abra o VS Code, vá em **Arquivo > Abrir Pasta** e selecione a pasta descompactada (`CorreiosAPI-master`).

---

## Instalando as Dependências

Com o terminal aberto na raiz do projeto, execute o comando abaixo para instalar o Cypress e as dependências necessárias:

```bash
npm install
```

---

## Executando os Testes

O projeto suporta diferentes modos de execução do Cypress.

### Modo Interativo (Cypress App)

Abre a interface gráfica do Cypress para acompanhar a execução visualmente:

```bash
npx cypress open
```

Na interface, selecione **E2E Testing**, escolha o navegador desejado e clique no arquivo de teste correspondente para iniciar.

### Modo Headless (Linha de Comando)

Executa os testes diretamente pelo terminal de forma rápida:

```bash
npx cypress run
```

---

## Resumo dos Comandos

| **Objetivo** | **Comando** |
| -------------------------------------- | ------------------ |
| **Instalar dependências / Cypress** | `npm install` |
| **Abrir interface gráfica do Cypress** | `npx cypress open` |
| **Executar testes em modo Headless** | `npx cypress run` |
