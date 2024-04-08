# TITLE TBD

Impulsione a Qualidade do Software: Desenvolvimento Local com Azion CLI

"Ambientes de Teste Local: Benefícios principais e Guia da Azion CLI"

"Melhore a Qualidade do Software: Teste local com Azion CLI"

"Maximize a Eficiência: Teste Local para Edge Functions"

"Desenvolvimento Seguro: Azion CLI para teste local"

"Melhore o Desempenho: Azion CLI e Teste Local Explicado"

Usando Azion CLI para Desenvolvimento e Testes Locais

Azion CLI é uma ferramenta eficiente para configurar ambientes de teste local para Edge Functions. Você pode facilmente usá-lo executando o comando \`azion dev\`, iniciando o processo de desenvolvimento local.

Para cenários com edge functions para Edge Firewall, você só precisa passar a flag \`--firewall\` junto com o comando. Este recurso enriquece suas capacidades de teste e análise de funções de firewall antes de integrá-las ao produto.

Benefícios:

- *Prevenção de erros*: teste novos recursos ou modificações antes de serem lançadas, reduzindo o risco de introduzir erros no sistema de produção.

- *Depuração melhorada*: depure o código de forma mais eficiente e rápida em um ambiente controlado.

- *Otimização de desempenho*: teste o comportamento do aplicativo sob diferentes cargas ou cenários de usuário únicos.

- *Melhorias de segurança*: identifique e corrija vulnerabilidades de segurança antes que o aplicativo seja lançado.

- *Eficiência no desenvolvimento*: trabalhe sem uma conexão com a internet, promovendo produtividade e autonomia.

- *Custo-eficaz*: evite correções pós-produção que consomem muitos recursos, economizando tempo e dinheiro ao resolver problemas potenciais antes do lançamento.

## Requisitos


- A Azion CLI instalada.
- Node.js >= 18.

## Testando edge functions para Edge Applications

Para iniciar um ambiente de teste local:

1.  Abra o terminal, crie um novo diretório e acesse-o.
2.  Inicie um aplicativo através do azion init
3.  Dê um nome a sua aplicação ou aceite a sugestão.
4.  Selecione JavaScript como o template.

\> Você pode iniciar a aplicação com base no modelo que desejar. Neste exemplo, usamos JavaScript.

5.  Inicie o desenvolvimento local respondendo sim à interação.
6.  Instale as dependências.
7.  Após um processo de compilação, Azion retornará a porta para acessar a aplicação.
8.  Envie requisições para o servidor e verifique o comportamento.

\>nota: você sempre pode encerrar o processo no terminal e rodar \`azion dev\` para executar a aplicação localmente. As alterações aplicadas na função são atualizadas através de hot reload.

O comando \`azion dev\` inicia um ambiente local onde você pode testar e monitorar a funcionalidade e eficiência de suas Edge Functions.

As edge functions da Azion são executadas no Azion Edge Runtime e possuem compatibilidade com Web APIs e Azion APIs.

*   [Primeiros passos com Edge Functions](https://www.google.com/url?q=https://www.azion.com/pt-br/documentacao/produtos/guias/edge-functions/primeiros-passos/&sa=D&source=editors&ust=1712588650570674&usg=AOvVaw1U-FRQBrsHjpUDdljIdoMt).
*   [Web APIs](https://www.google.com/url?q=https://www.azion.com/pt-br/documentacao/devtools/runtime-apis/javascript/&sa=D&source=editors&ust=1712588650570857&usg=AOvVaw0OHUK06bDQ7SmSIgLu7GUS).
*   [Lista completa de suporte a Web APIs do Azion Edge Runtime](https://www.google.com/url?q=https://www.azion.com/pt-br/documentacao/produtos/edge-application/edge-functions/runtime-apis/javascript/tipos-suportados/&sa=D&source=editors&ust=1712588650571052&usg=AOvVaw18dhDP8kNctApwLY-lf01O).

---

## Testando edge functions para Edge Firewall

Se você implementou funções para Edge Firewall, você precisa considerar condições especiais de teste.

Para isso, é preciso executar o comando \`azion dev\` com a flag \`--firewall\`, que informa ao sistema de que você está testando uma função de firewall.

*   [Edge functions para o Edge Firewall](https://www.google.com/url?q=https://www.azion.com/pt-br/documentacao/produtos/secure/edge-firewall/edge-functions-instances/&sa=D&source=editors&ust=1712588650571829&usg=AOvVaw3jWFpd7lfLDpzHnfhfCooY).
*   [API Network List.](https://www.google.com/url?q=https://www.azion.com/pt-br/documentacao/produtos/edge-application/edge-functions/runtime/api-reference/network-list/&sa=D&source=editors&ust=1712588650572004&usg=AOvVaw1tSA39Bzegnz5uJLcfmxwR)
*   [API de Metadados](https://www.google.com/url?q=https://www.azion.com/pt-br/documentacao/produtos/edge-application/edge-functions/runtime/api-reference/metadata/&sa=D&source=editors&ust=1712588650572235&usg=AOvVaw1PB8IlumCY5hMoepuhIZK4).

---

## Como o Azion CLI Local Dev Funciona

### Fluxo de Dados

Através da Azion CLI, o usuário executa o comando \`azion dev \[flags\]\`.

A Azion CLI chama o Vulcan, que gerencia a construção e o desenvolvimento local.

O Vulcan inicia um servidor e este servidor instancia o Runtime. Este runtime suporta uma lista de Web APIs e emula o verdadeiro Azion Edge Runtime.

### Responsabilidades

*Azion CLI*: atua como o ponto principal de interação entre o usuário e o sistema. Tem a responsabilidade de gerenciar todo o processo de implantação do aplicativo, garantindo um fluxo de trabalho suave e eficiente.

*Vulcan*: o motor que impulsiona a inicialização do projeto, construção e adaptação. Ele configura de maneira inteligente o projeto com base no modelo selecionado, garantindo que o aplicativo esteja otimamente configurado para seu uso pretendido. Para o desenvolvimento local, o Vulcan:

-  Inicia um servidor.
-  Instancia o Edge Runtime.
-  Lida com mudanças no código-fonte, implementando hot reload.

---

## Sobre Edge Functions

As Edge Functions da Azion são usadas para aprimorar Edge Applications ou para impulsionar a segurança em um Edge Firewall. Ambas são executadas na Azion Edge Runtime, reduzem a latência e ajudam a implementar uma abordagem distribuída. OK, mas qual é a diferença entre elas?

A diferença está na maneira como as funções são estruturadas, vamos nos aprofundar nisso.

edge functions Applications

Primeiro, as edge functions para Edge Applications funcionam com base em um evento fetch. Elas são inicializadas com uma função \`addEventListener\`, passando fetch como o tipo de evento, e um evento. Por exemplo:

```js

  addEventListener('fetch', event \=> {

      event.respondWith(handleRequest(event.request));

    });
```

Segundo, é necessário definir o comportamento da função handleRequest. Esta função tem \`event.request\` como a assinatura. Esses dados podem ser usados para implementar a lógica necessária, como:

Manipular cookies.

Implementar um comportamento com base no método de solicitação HTTP (POST, GET, PUT, DELETE).

Acessar os metadados da solicitação.

A função \`handleRequest\` pode ser definida como:

```js
  const html \= \`<!DOCTYPE html>

  <body>

    <h1>Hello World</h1>

    <p>This markup was generated by Azion - Edge Functions.</p>

  </body>\`

  async function handleRequest(request) {

    return new Response(html, {

      headers: {

        "content-type": "text/html;charset=UTF-8",

      },

    })

  }
```

Neste exemplo, a resposta será o conteúdo HTML, declarado anteriormente pela const html. O cabeçalho pode ser manipulado e, no exemplo, o tipo de conteúdo é definido.

Exemplo completo:

```js
const html \= \`<!DOCTYPE html>

  <body>

    <h1>Hello World</h1>

    <p>This markup was generated by Azion - Edge Functions.</p>

  </body>\`

  async function handleRequest(request) {

    return new Response(html, {

      headers: {

        "content-type": "text/html;charset=UTF-8",

      },

    })

  }

  addEventListener('fetch', event \=> {

      event.respondWith(handleRequest(event.request));

    });
```

[Saiba mais sobre edge functions para Edge Applications](https://www.google.com/url?q=https://www.azion.com/pt-br/documentacao/produtos/build/edge-application/edge-functions/&sa=D&source=editors&ust=1712588650580606&usg=AOvVaw02WTxFWw44ieRadRqA9kFA).

### Edge functions para Edge Firewall

As edge functions para o Edge Firewall operam com base em um evento de firewall. Eles são inicializados usando a function \`addEventListener\`, passando \`'firewall'\` como o tipo de evento, e um evento. For example:

```js
  addEventListener('firewall', event \=> {

      event.deny();

  });

```

Nesse caso, a system envia uma negação em resposta ao evento de firewall que foi acionado. Pode haver outras reações a eventos como \`event.continue()\`, e \`event.drop()\` dependendo das circunstâncias específicas ou da lógica desejada.

É necessário definir os comportamentos potenciais para diferentes reações a eventos dentro do listener do evento de firewall. A resposta exata depende da condição atendida. Por exemplo:

Detectar níveis de ameaça.

Bloquear ou listar direitos dos endereços IP.

Implementar comportamentos baseados em padrões de tráfego.

Um exemplo onde a função \`event.deny\` é definida e usada:

```js
 // Definir uma lista de endereços IP bloqueados

  const blockedIPs \= \["192.0.2.0", "203.0.113.0", "198.51.100.0"\]

  addEventListener('firewall', event \=> {

      let ip \= event.request.clientIP;

      if (blockedIPs.includes(ip)) {

          event.deny();

      } else {

          event.continue();

      }

  });
```

Neste exemplo, o listener do evento de firewall verifica o endereço IP que acionou o evento na lista de IPs bloqueados. Se o IP estiver na lista, a evento é negado. If the IP is not on the list, processing of the event will continue. Ele mostra como você pode usar \`event.deny()\`, \`event.continue()\`, and \`event.drop()\` em cenários de aplicação reais.

[Saiba mais sobre as edge functions para o edge firewall](https://www.google.com/url?q=https://www.azion.com/pt-br/documentacao/produtos/secure/edge-firewall/edge-functions-instances/&sa=D&source=editors&ust=1712588650584523&usg=AOvVaw0yg15wcLOykG_UU4-d1IGI).

---

## Conclusão


Usar ambientes de teste locais melhora o processo de desenvolvimento do produto. Uma ferramenta como a Azion CLI facilita a construção de soluções de software confiáveis, eficientes, seguras e de alto desempenho. Ao testar edge functions com o comando \`azion dev\`, e opcionalmente adicionando uma flag \`--firewall\` quando necessário, os desenvolvedores podem navegar por possíveis armadilhas antes de levar seu código para produção.
