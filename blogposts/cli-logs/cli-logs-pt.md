---
schema: blog_post
title: Melhorando a Depuração de Edge Functions com Azion CLI Logs
authors:
    - src/content/authors/gabriel.franca.md
meta_tags: azion, cli, logs, debugging, edge functions, serverless
excerpt: >-
    Aprenda como melhorar o processo de depuração de suas edge functions usando os logs da Azion CLI. Obtenha insights imediatos sobre o comportamento de sua aplicação e monitore logs diretamente do seu terminal.
description: >-
    Este post do blog fornece um guia abrangente sobre como usar os logs da Azion CLI para depurar edge functions. Ele abrange o processo de acesso a logs em tempo real, os pré-requisitos para usar o Azion CLI e os benefícios dos logs de console localizados.
img_featured: >-
    /assets/blog/images/uploads/azion-cells-technical-approach-and-the-future-of-serverless-computing.png
categories:
    - developers
related_content:
namespace: blogpost_azion_cli_logs
date: 2024-02-26T06:00:00Z
date_updated:
resourceHub:
    flags:
        contentType: Blog
permalink: /melhorando-a-depuracao-de-edge-functions-com-azion-cli-logs/
---

# Melhorando a Depuração de Edge Functions com o comando Azion Logs

Os logs em tempo real, ou tail logs, são um recurso inestimável para obter insights imediatos sobre o comportamento da sua aplicação. No entanto, acessar esses logs pode muitas vezes ser uma tarefa desafiadora.

O Azion CLI simplifica esse processo permitindo que você monitore logs diretamente do seu terminal. Isso é particularmente útil para logs de suas edge functions.

O comando `azion logs cells` permite que você visualize `console.logs()` de suas edge functions em sua máquina local, melhorando significativamente a maneira como você testa e depura funções serverless. Para monitoramento mais contínuo, o comando `azion logs cells --tail` pode ser usado para continuar exibindo novos logs à medida que eles chegam.

Embora o Azion CLI também suporte o comando `azion logs http` para acessar logs HTTP relacionados às suas edge applications, nos concentraremos nos comandos `azion logs cells` e `azion logs cells --tail` nesta discussão. O comando `azion logs http` será abordado em uma postagem dedicada em breve.

[Aprenda mais sobre Edge Functions]()
[Aprenda mais sobre Edge Applications]()

---

## Por Trás das Cenas: Como Funcionam os Tail Logs da Azion CLI

![Logs da Azion](./logs.png "Logs da Azion")

### Logs da Azion

#### Fluxo de Dados

1. O usuário inicia o processo executando o comando `azion logs cells`.
2. O Azion CLI interage com a API GraphQL.
3. A API GraphQL responde retornando logs dos últimos cinco minutos.
4. O CLI processa e interpreta esses dados.
5. Os logs são apresentados ao usuário, com a opção de exibir os dados em um formato mais legível e aprimorado.

### Tail Logs

#### Fluxo de Dados

1. O usuário inicia o processo executando o comando `azion logs cells --tail`.
2. O Azion CLI continua chamando a API GraphQL, iniciando a cada vez a partir do carimbo de data/hora do último log que foi exibido na tela.
3. A API GraphQL responde retornando os dados solicitados.
4. O CLI então processa e interpreta esses dados.
5. Finalmente, os logs são retornados ao usuário. O usuário pode receber esses dados em um formato mais legível e aprimorado.

### Responsabilidades

- **Azion CLI**: atua como a interface para a interação do usuário e é responsável por formatar e retornar os dados ao usuário.
- **API GraphQL**: lida com as solicitações de entrada (comunica-se com o beholder) e recupera os dados solicitados.

---

## Pré-requisitos para Usar o Azion CLI

- [Azion CLI instalado](https://www.azion.com/pt-br/documentacao/produtos/azion-cli/#instalacao-do-azion-cli).
- Node.js ≥ 18.
- Acesso à linha de comando.

---

## Colocando em Prática: Verificando logs de edge functions

### Verificando logs localmente

1. Abra o terminal.
2. Execute `azion init`.
3. Escolha o template JavaScript.
4. Decida executá-lo localmente.
5. Instale as dependências.
6. Edite o arquivo `main.js`, criado pelo comando init.
   - Adicione declarações `console.log()` conforme necessário.

Declarações de log de exemplo para inspecionar os dados da requisição:

```js
export default function myWorker(event) {
  // Registra a URL da Requisição
  console.log("URL da Requisição: ", event.request.url);
  // Registra o Método da Requisição
  console.log("Método da Requisição: ", event.request.method);
  // Registra os Cabeçalhos da Requisição
  console.log("Cabeçalhos da Requisição: ", event.request.headers);
  // Se event.request.method for 'POST' ou 'PUT', registre também o corpo da requisição.
  // Fique ciente: ler o corpo irá consumi-lo, então ele não estará mais disponível para fetch
  if (["POST", "PUT"].includes(event.request.method)) {
    event.request
      .clone()
      .text()
      .then((bodyText) => {
        console.log("Corpo da Requisição: ", bodyText);
      });
  }
  return new Response("Olá, Mundo");
}
```

7. Execute `azion dev`.
8. Acesse a porta fornecida ao final da execução do comando `azion dev`:
    - Execute: curl http://localhost:{{porta}}.
    - Visite: http://localhost:{{porta}} em seu navegador.
9. Verifique os logs gerados no terminal quando a função é executada.

### Implementando sua aplicação e verificando tail logs ao vivo na Azion

Siga estes passos:

1. Execute `azion deploy` para implantar sua aplicação no edge.
2. Acesse o domínio da sua aplicação, fornecido no final do processo de implantação.
3. Execute `azion logs cells --tail` para recuperar tail logs ao vivo de suas edge functions.

> Nota: o comando `azion logs cells` busca logs dos últimos *5 minutos*. Mais detalhes estão disponíveis na [documentação do comando azion logs](https://www.azion.com/pt-br/documentacao/produtos/azion-cli/#usando-o-comando-azion-logs-cells).

---

## Aproveitando os Logs da Azion

O comando `azion logs cells` fornece acesso direto a informações essenciais para depuração. Com registros de suas funções serverless estruturados de forma consciente, você pode obter insights sobre a sequência de operações, o que simplifica a identificação de problemas. Status de logs, mensagens de erro, dados específicos da função, entradas, saídas, e o estado da aplicação podem acelerar o processo de depuração.

## Benefícios dos Logs de Console Localizados

Os logs de console localizados têm vários benefícios:

- **Depuração aprimorada**: trazer condições semelhantes ao edge para o seu setup local permite uma depuração eficiente, reduzindo significativamente o tempo de desenvolvimento.
- **Melhor compreensão do comportamento da função**: você pode monitorar a funcionalidade e a lógica de sua função em tempo real.
- **Desenvolvimento iterativo**: logs de console localizados simplificam os testes para ciclos de desenvolvimento iterativo, garantindo que cada mudança funcione conforme o esperado.
- **Redução de custos com servidores**: reduzir implantações em servidores para pequenas alterações pode diminuir o uso e os custos do servidor.

---

## Conclusão

Em conclusão, o [Azion CLI](https://www.azion.com/pt-br/documentacao/produtos/azion-cli/) oferece uma maneira poderosa e eficiente de depurar e monitorar suas edge functions. Com a capacidade de observar logs em tempo real através do seu terminal, você pode obter insights valiosos sobre o comportamento de sua aplicação, reduzindo significativamente o tempo de desenvolvimento e os custos de uso do servidor. O comando `azion logs cells --tail`, em particular, oferece uma visão em tempo real do comportamento da sua função, tornando-se uma ferramenta inestimável para qualquer desenvolvedor que trabalhe com edge functions da Azion. Seja você testando localmente ou implementando sua aplicação na Azion, essas ferramentas proporcionam uma abordagem eficiente para depuração e monitoramento.