# PROJETO DE AUTOMAÇÃO: API CORREIOS (CEP INTEGRATION)

## 1. OBJETIVO DO DOCUMENTO
Este documento detalha a estratégia de automação de testes para a API de consulta de CEPs (utilizando o endpoint de integração B2W/Americanas). O foco principal é validar a precisão dos dados geográficos retornados e a resiliência do back-end diante de entradas malformadas ou inexistentes, garantindo uma integração segura para serviços de logística e checkout.

## 2. TECNOLOGIAS UTILIZADAS
* **Framework:** [Cypress](https://www.cypress.io/) (Interface de API Testing)
* **Linguagem:** JavaScript / Node.js
* **Protocolo:** HTTP/REST
* **CI/CD:** GitHub Actions

## 3. ARQUITETURA E ESTRUTURA
A suíte de testes foi projetada para cobrir dois pilares fundamentais da integridade de APIs:

* **Geographic Coverage (Caminho Feliz):** Validação de CEPs reais abrangendo todas as regiões do Brasil (Sul, Sudeste, Centro-Oeste, Nordeste e Norte). O teste garante que campos como `address`, `city` e `state` correspondam exatamente à base oficial.
* **Robustness & Error Handling:** Testes de cenários negativos para validar como a API lida com:
    * **Entradas Inválidas:** Formatos alfanuméricos, caracteres especiais e espaços.
    * **Boundary Testing:** CEPs com excesso ou ausência de caracteres (acima/abaixo de 8 dígitos).
    * **Status Code Mapping:** Verificação da diferenciação correta entre erros de negócio (`404 Not Found`) e falhas de processamento interno (`500 Internal Server Error`).
* **Non-Breakable Requests:** Uso da flag `failOnStatusCode: false` para permitir a inspeção detalhada de payloads de erro sem interromper o fluxo de execução do Cypress.

## 4. COMO EXECUTAR O PROJETO

### **Pré-requisitos**
* Node.js instalado
* Clone do repositório: `git clone https://github.com/FabioGVL/CorreiosAPI.git`

### **Instalação**
```bash
npm install
npx cypress run
