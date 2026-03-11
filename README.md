# Escopo do Projeto
Este documento detalha a estratégia de automação de testes para a API de consulta de CEPs (utilizando o endpoint de integração B2W/Americanas). O foco principal é validar a precisão dos dados geográficos retornados e a resiliência do back-end diante de entradas malformadas ou inexistentes, garantindo uma integração segura para serviços de logística e checkout.

## 1. Arquitetura e estrutura
A suíte de testes foi projetada para cobrir dois pilares fundamentais da integridade de APIs:

* Validação de CEPs reais abrangendo todas as regiões do Brasil (Sul, Sudeste, Centro-Oeste, Nordeste e Norte). O teste garante que campos como `address`, `city` e `state` correspondam exatamente à base oficial.
* Testes de cenários negativos para validar como a API lida com:
    * Formatos alfanuméricos, caracteres especiais e espaços.
    * CEPs com excesso ou ausência de caracteres (acima/abaixo de 8 dígitos).
    * Verificação da diferenciação correta entre erros (`404 Not Found`) e falhas de processamento interno (`500 Internal Server Error`).
* Uso da flag `failOnStatusCode: false` para permitir a inspeção detalhada de payloads de erro sem interromper o fluxo de execução do Cypress.

## 2. Passos para reproduzir o teste

### 2.1 Efetuando o download e descompactando o projeto
- No GitHub, clique em "code".
- Clique em "Download Zip" para fazer o download do arquivo deste teste.
- No seu computador, localize o download efetuado.
- Descompacte o arquivo.

### 2.2 Configurando o projeto no VSCode e executando o teste
- Abra o VSCode.
- Clique em `Arquivo/File`.
- Clique em `Abrir pasta/Open folder`.
- Escolha a pasta do arquivo descompactado (`CorreiosAPI-master`).
- Após o projeto ser aberto no VSCode, navegue até `Cypress > E2E`.
- Os testes estarão dentro das pastas `UI`.
- No terminal do Cypress digite `npx cypress open`. Caso necessário, instale o Cypress através do comando `npm install cypress`.
- Aguarde o Cypress abrir.
- Selecione a opção `E2E Testing`.
- Na próxima página selecione o navegador desejado.
- Na próxima página selecione o teste que deseja executar e a automação será executada.
- Também é possível executar o teste através do comando `npx cypress run`. O teste rodará dentro do próprio VSCode e serão gerados vídeos dos resultados dos testes. Os vídeos ficarão armazenados no destino `Cypress > Vídeos`.

## 3. Ferramentas e ambientes utilizados para execução do projeto:
- Cypress v10.11.0
- Node JS v20.15.0
- Google Chrome v126.0.6478.126
- Windows 11 v23H2
- Postman
- GIT

