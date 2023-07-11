# Data Streaming
**Data Streaming** é um produto de **Observe** que permite que você alimente suas plataformas de stream, SIEM e big data com os logs de eventos de suas aplicações na Azion em tempo real. Para manter uma performance avançada, usa a codificação ASCII para evitar problemas de parser e problemas na interpretação dos dados.

Você pode escolher de quais produtos e domínios disponíveis na Azion deseja coletar seus dados de logs e conectá-los ao endpoint de sua plataforma de análise de dados. Você também pode escolher quais variáveis quer usar em sua análise.

Ao criar um data streaming, você consegue:

- Ter um conjunto de logs organizado.
- Conectar o seu data streaming a endpoints.
- Entender o comportamento de seus usuários.
- Identificar dados de ameaças à segurança.
- Tomar decisões informadas.
- Aperfeiçoar suas aplicações e seu negócio através de práticas confiáveis de observabilidade.

Após configurar seu data streaming, você pode conferir os seus logs de dados sendo enviados com sucesso através do [Real-Time Events](https://www.azion.com/pt-br/documentacao/produtos/real-time-events/).

## Implementação
| Tarefa | Guia |
| ----- | ----- |
| Utilização | [Como utilizar o Data Streaming](https://www.azion.com/pt-br/documentacao/produtos/guias/como-usar-data-streaming/) |
| Associar domínios | [Como associar domínios no Data Streaming](https://www.azion.com/pt-br/documentacao/produtos/guias/data-streaming-associar-dominios/) |
| Criar template personalizado | [Como criar um template personalizado no Data Streaming](https://www.azion.com/pt-br/documentacao/produtos/guias/data-streaming-template-personalizado/) |

---

## Logs

Por padrão, o Data Streaming envia seus logs de eventos quando o bloco com as variáveis atinge 2.000 registros, a cada 60 segundos, ou quando o tamanho do pacote atinge o valor determinado no campo Max Size do payload, o que ocorrer primeiro. No entanto, se você estiver usando o endpoint AWS Kinesis Data Firehose, o Data Streaming enviará seus logs de eventos quando o bloco atingir 500 registros ou a cada 60 segundos.

---

## Data source ingestion
Um Data Source representa a aplicação na Azion que gera os registros de eventos que você quer usar. Ao selecionar um data source, você decide de onde seus dados vão ser coletados e as demais configurações são feitas de acordo com sua escolha.

---

## Personalização de Payload
Ao usar o endpoint Standard HTTP/HTTPS POST, o payload para o seu endpoint não é pré-definido. Você tem a opção de personalizar as informações essenciais que serão enviadas em seus dados da forma que achar melhor.

---

## Data sources

Selecionar um data source na lista suspensa é obrigatório. Você pode escolher entre:

- [Activity History](#activity-history)
- [Edge Applications](#edge-applications)
- [Edge Functions](#edge-functions)
- [WAF Events](#waf-events)

Cada data source tem *variáveis* pré-configuradas, combinadas em um template, que representam a informação específica que você pode receber dos seus registros de eventos. Veja os pré-requisitos e as variáveis de cada data source e que dados fornecem a seguir.

### Activity History {#activity-history}

> Não é possível associar domínios ao usar o data source **Activity History**.

O data source **Activity History** exibe os dados referentes aos [registros de atividade](https://www.azion.com/pt-br/documentacao/produtos/gestao-de-contas/activity-history/) de sua conta no RTM. As seguintes variáveis estão disponíveis para essa opção:

| Variável | Descrição |
| --- | --- |
| $author_email | Email do usuário do Real-Time Manager que executou a atividade. |
| $author_name | Nome do usuário do Real-Time Manager que executou a atividade. |
| $client | Identificador único de cliente Azion. Exemplo: 4529r |
| $comment | Campo em branco disponível para que usuários possam adicionar comentários ao realizarem mudanças. |
| $time | Data e hora da requisição. Exemplo: Oct. 31st, 2022 - 19:30:41 |
| $title | Título da atividade, composto por: nome do modelo, nome e tipo de atividade. Exemplo: Pathorigin Default Origin was changed |
| $type | Tipo de ação executada no Real-Time Manager: CREATED, CHANGED, DELETED ou SIGNED UP. |

---

### Edge Applications {#edge-applications}

O data source **Edge Applications** exibe os dados das requisições feitas para suas [edge applications](https://www.azion.com/pt-br/documentacao/produtos/edge-application/) na Azion. As seguintes variáveis estão disponíveis para essa opção:

| Variável | Descrição |
| --- | --- |
| $asn | Autonomous System Number Allocation (ASN), que são redes de endereços IP gerenciadas por uma ou mais operadoras de rede que têm uma política de roteamento clara e única. Exemplo: AS52580 |
| $bytes_sent | Número de bytes enviados para o cliente. Exemplo: 191 |
| $client | Identificador único de cliente Azion. Exemplo: 4529r |
| $configuration | Identificador único de configuração Azion definido no arquivo de configuração do virtual host. Exemplo: 1595368520 |
| $country | País do cliente detectado pela geolocalização de endereço IP. Exemplo: United States |
| $host | Informação de host enviada na linha da requisição. Armazena: nome do host da linha da requisição, *ou* o nome do host do campo *Host* do campo host do cabeçalho, *ou* o nome do servidor correspondente à requisição. |
| $http_referrer | Endereço da página na qual o usuário fez a requisição. Valor do cabeçalho Referer. Exemplo: https://example.com |
| $http_user_agent | Identificação da aplicação, do sistema operacional, do fornecedor, e/ou da versão do usuário final. Valor do cabeçalho User-Agent. Exemplo: Mozilla/5.0 (Windows NT 10.0; Win64; x64) |
| $proxy_status | Código de status de erro HTTP ou da origem quando nenhuma resposta é obtida da origem. Exemplo: 520. **Em caso de cache, a resposta é `-`**. |
| $remote_addr | Endereço IP da origem que gerou a requisição. |
| $remote_port | Porta remota da origem que gerou a requisição. |
| $request_id | Identificador único da requisição. Exemplo: 5f222ae5938482c32a822dbf15e19f0f |
| $request_length | Tamanho da requisição, incluindo a linha da requisição, cabeçalhos e corpo. |
| $request_method | Método da requisição. Exemplo: GET ou POST |
| $request_time | Tempo de processamento da requisição decorrido desde que os primeiros bytes foram lidos a partir do cliente com resolução de milisegundos. Exemplo: 1.19 |
| $request_uri | URI da requisição realizada pelo usuário, sem a informação do host e de protocolo e com argumentos. Exemplo: /v1?v=bo%20dim |
| $requestPath | URI da requisição sem a informação de Query String, Host e Protocol. Exemplo:  se `request_uri`: /jira/plans/48/scenarios/27?vop=320#plan/backlog, então `requestPath`: /jira/plans/48/scenarios/27 |
| $requestQuery | Parâmetros da URI da requisição. Exemplo: requestQuery: vid=320#plan/backlog |
| $scheme | Esquema da requisição. Exemplo: HTTP ou HTTPS |
| $sent_http_content_type | Cabeçalho “Content-Type” enviado na resposta da origem. Exemplo: text/html; charset=UTF-8. |
| $sent_http_x_original_image_size | Cabeçalho "X-Original-Image-Size" enviado na resposta da origem. Informa o tamanho da imagem original. Exemplo: 987390 |
| $server_addr | Endereço IP do servidor que recebeu a requisição. |
| $server_port | Porta remota do servidor que recebeu a requisição. |
| $server_protocol | Protocolo da requisição. Exemplo: HTTP/1.1. |
| $session_id | Identificação da sessão. |
| $ssl_cipher | String de cifra utilizada para estabelecimento de conexão TLS. Exemplo: TLS_AES_256_GCM_SHA384 |
| $ssl_protocol | Protocolo de uma conexão TLS estabelecida. Exemplo: TLS v1.2 |
| $ssl_server_name | Nome do servidor, informado pelo cliente, que o cliente está tentando conectar. Exemplo: www.example.com |
| $ssl_session_reused | Retorna `r` se a sessão TLS for reutilizada; nos demais casos, retorna `.`. |
| $state | Estado do cliente detectado pela geolocalização de endereço IP. Exemplo: CA |
| $status | Código de status HTTP da requisição. Exemplo: 200 |
| $stream | ID definida através de configuração de host virtual com base na diretiva de localização. Definido no arquivo de configuração do host virtual. |
| $tcpinfo_rtt | Tempo de Round-Trip Time (RTT) medido pelo edge para o usuário. Disponível em sistemas que suportam a opção TCP_INFO socket. |
| $time | Data e hora da requisição. Exemplo: Oct. 31st, 2022 - 19:30:41 |
| $traceback | Informa os nomes dos Rules Engine do Edge Application e do Edge Firewall executadas pela requisição. |
| $upstream_addr | Endereço IP e porta do cliente. Também pode armazenar múltiplos servidores ou grupos de servidores. Exemplo: 192.168.1.1:80. |
| $upstream_bytes_received | Número de bytes recebidos pelo edge da origem, se o conteúdo não estiver em cache. Exemplo: 8304 |
| $upstream_bytes_sent | Número de bytes enviados para a origem. Exemplo: 2733 |
| $upstream_cache_status | Status do cache local do edge. Exemplo: MISS, BYPASS, EXPIRED, STALE, UPDATING, REVALIDATED ou HIT. |
| $upstream_connect_time | Tempo, em milisegundos, para o edge estabelecer uma conexão com a origem. No caso de TLS, inclui tempo gasto em handshake. **`0` no caso de KeepAlive e `-` no caso de cache.** |
| $upstream_header_time | Tempo, em milissegundos, para que o edge receba os cabeçalhos de resposta da origem. Exemplo: 0.345. **No caso de cache, a resposta é `-`.** |
| $upstream_response_time | Tempo, em milisegundos, para o edge receber uma resposta padrão da origem, incluindo cabeçalhos e corpo. Exemplo: 0.876. **No caso de cache, a resposta é `-`.** |
| $upstream_status | Código de status HTTP da origem. Se um servidor não pode ser selecionado, a variável mantém o código de status 502 (Bad Gateway). **No caso de cache, a resposta é `-`.** |
| $waf_attack_action | Informa a ação do WAF em relação à ação. Pode ser: $BLOCK, $PASS, $LEARNING_BLOCK ou $LEARNING_PASS. |
| $waf_attack_family | Informa a classificação da infração de WAF detectada na requisição. Exemplo: SQL, XSS, TRAVERSAL, entre outras. |
| $waf_block | Informa se o WAF bloqueou ou não a ação. `0` quando não bloqueado e `1` quando bloqueado. Quando em `Learning Mode`, ele não será bloqueado, independentemente do retorno. |
| $waf_headers | Quando os cabeçalhos de solicitação enviados pelo usuário são analisados pelo módulo WAF e marcados como **blocked**, `$waf_block = 1`. Tem uma string codificada em base64. Caso contrário, ele terá um traço `-`. Aplica-se aos modos `WAF Learning` ou `Blocking`. |
| $waf_learning | Informa se o WAF está em Learning Mode. Pode ser `0` ou `1`. |
| $waf_match | Lista de infrações encontradas na requisição do usuário final. É formada por elementos chave-valor: a *chave* é referente ao tipo de infração detectada; o *valor* apresenta a string que gerou a infração. |
| $waf_score | Informa a pontuação que será incrementada em caso de match com as regras criadas para o WAF. |
| $waf_total_blocked | Informa o número total de requisições bloqueadas. |
| $waf_total_processed | Informa o número total de requisições processadas. |

> Você pode adicionar a variável **$traceback** em um custom template com o data source Edge Applications se você tem ativada a opção de *Debug rules* em sua aplicação. Veja mais em [Debugging rules em Edge Application](https://www.azion.com/pt-br/documentacao/produtos/edge-application/rules-engine/#debug-de-regras).

As variáveis: `$upstream_bytes_received`; `$upstream_cache_status`; `$upstream_connect_time`; `$upstream_header_time`; `$upstream_response_time` e `$upstream_status` podem apresentar *mais de um elemento separado por vírgula*. Quando uma conexão é disparada, seja por redirecionamento interno ou escolha de origem com [Load Balancer](https://www.azion.com/pt-br/documentacao/produtos/edge-application/load-balancer/), por exemplo, cada valor contido no campo representa a respectiva conexão iniciada. O campo pode ser separado por:

- Uma vírgula, representando múltiplos IPs.
- Dois-pontos, representando redirecionamento interno.

Se vários servidores foram contatados durante o processamento da solicitação, seus endereços são separados por vírgulas, por exemplo: `192.168.1.1:80, 192.168.1.2:80`.

Se ocorre um redirecionamento interno de um grupo de servidores para outro, iniciado por *X-Accel-Redirect* ou *Error Responses*, os endereços de servidores de diferentes grupos são separados por *dois-pontos*. Exemplo: `192.168.1.1:80, 192.168.1.2:80, unix:/tmp/sock : 192.168.10.1:80, 192.168.10.2:80`.

Se um servidor não puder ser selecionado, a variável mantém o nome do grupo de servidores.

Considerando vários valores como transições na conexão, o último valor tende a ser o mais importante. Se você usa o recurso *Error Responses* nas suas edge applications, você verá dois valores nos campos *upstream* que representam o status da origem e o resultado da solicitação feita para que o conteúdo seja entregue. Em casos normais, você terá `502: 200`.

*502* é o código de erro HTTP para a resposta da primeira tentativa de obter conteúdo do servidor de origem. Como ele retornou um erro *502*, considerando que você configurou uma *Error Responses* para o status *502*, outra solicitação será feita para que o URI seja definido. Em seguida, a página será entregue e o status HTTP será adicionado aos campos *upstream*, respeitando sua posição para todos eles. Neste exemplo, o resultado é a composição `502 : 200`.

---

### Edge Functions {#edge-functions}

O data source **Edge Functions** exibe os dados referentes às solicitações feitas para suas [edge functions](https://www.azion.com/pt-br/documentacao/produtos/edge-application/edge-functions/) na Azion. Você deve ter contratado esse módulo para poder usá-lo no Data Streaming.

As seguintes variáveis estão disponíveis para essa opção:

| Variável | Descrição |
| --- | --- |
| $client | Identificador único de cliente Azion. Exemplo: 4529r |
| $edge_function_id | Identificador da Edge Function. Exemplo: 1321 |
| $global_id | Identificador da configuração. |
| $log_level | Nível do log gerado: ERROR, WARN, INFO, DEBUG ou TRACE. |
| $log_message | Mensagem editável usada para o log na chamada da função. Disponível para usuários identificarem e reportarem acontecimentos. |
| $message_source | Fonte da mensagem. Quando as mensagens são geradas pela API do Console: `CONSOLE`; quando são relacionadas a uma mensagem de erro: `RUNTIME`.  |
| $request_id | Identificador único da requisição. Exemplo: 5f222ae5938482c32a822dbf15e19f0f |
| $time | Data e hora da requisição. Exemplo: Oct. 31st, 2022 - 19:30:41 |

---

### WAF Events {#waf-events}

O data source **WAF Events** exibe os dados referentes às requisições analisadas pelo [Web Application Firewall (WAF)](https://www.azion.com/pt-br/documentacao/produtos/edge-firewall/web-application-firewall/) para que você possa mapear a pontuação atribuída à requisição, às regras de WAF que deram match e aos motivos do bloqueio. Você deve ter contratado esse módulo para poder usá-lo no Data Streaming.

As seguintes variáveis estão disponíveis para essa opção:

| Variável | Descrição |
| --- | --- |
| $blocked | Informa se o WAF bloqueou ou não a ação. `0` quando não bloqueado e `1` quando bloqueado. Quando em `Learning Mode`, ele não será bloqueado, independentemente do retorno. |
| $client | Identificador único de cliente Azion. Exemplo: 4529r |
| $configuration | Identificador único de configuração Azion definido no arquivo de configuração do virtual host. Exemplo: 1595368520 |
| $country | País do cliente detectado pela geolocalização de endereço IP. Exemplo: United States |
| $headers | Quando os cabeçalhos de solicitação enviados pelo usuário são analisados pelo módulo WAF e marcados como **blocked**, `$waf_block = 1`. Tem uma string codificada em base64. Caso contrário, ele terá um traço `-`. Aplica-se aos modos `WAF Learning` ou `Blocking`. |
| $host | Informação de host enviada na linha da requisição. Armazena: nome do host da linha da requisição, *ou* o nome do host do campo *Host* do campo host do cabeçalho, *ou* o nome do servidor correspondente à requisição. |
| $remote_addr | Endereço IP da origem que gerou a requisição. |
| $requestPath | URI da requisição sem a informação de Query String, Host e Protocol. Exemplo: se `request_uri`: /jira/plans/48/scenarios/27?vop=320#plan/backlog, então `requestPath`: /jira/plans/48/scenarios/27 |
| $requestQuery | Parâmetros da URI da requisição. Exemplo: requestQuery: vid=320#plan/backlog |
| $server_protocol | Protocolo da requisição. Exemplo: HTTP/1.1. |
| $time | Data e hora da requisição. Exemplo: Oct. 31st, 2022 - 19:30:41 |
| $truncated_body | Essa variável foi descontinuada. Portanto, não terá um valor atribuído à ela, apenas `-` no lugar de um valor. |
| $version | A versão de Azion Log usada. Exemplo: v5 |
| $waf_args | Argumentos da requisição. |
| $waf_attack_action | Informa a ação do WAF em relação à ação. Pode ser: $BLOCK, $PASS, $LEARNING_BLOCK ou $LEARNING_PASS. |
| $waf_attack_family | Informa a classificação da infração de WAF detectada na requisição. Exemplo: SQL, XSS, TRAVERSAL, entre outras. |
| $waf_learning | Informa se o WAF está em modo Learning. Pode ser `0` ou `1`.  |
| $waf_match | Lista de infrações encontradas na requisição do usuário final. É formada por elementos chave-valor: a *chave* é referente ao tipo de infração detectada; o *valor* apresenta a string que gerou a infração. |
| $waf_score | Informa a pontuação que será incrementada em caso de match com as regras criadas para o WAF. |
| $waf_server | Hostname usado na requisição de WAF. Exemplo: api-login.azion.com.br |
| $waf_uri | URI usada na requisição do WAF. Exemplo: /access/v2/after-login |

–-

## Templates

Um template no **Data Streaming** fornece o conjunto de variáveis pré-configuradas disponíveis para cada data source em um formato adequado para a transferência dos seus registros de eventos. Após selecionar o seu data source, você pode:

- Selecionar o template correspondente, fornecido pela Azion.
- Personalizar seu próprio template, escolhendo quais variáveis quer usar.

Você encontra quatro templates fornecidos pela Azion e um **Custom Template**, que permite que você decida quais variáveis serão usadas. Os templates estão disponíveis na lista suspensa **Template** e as variáveis para os templates são exibidas no campo de código **Data Set** em formato JSON.

Veja qual template corresponde a qual data source:

| Data Source | Template |
| --- | --- |
| Activity History | Activity History Collector |
| Edge Applications | Edge Applications + WAF Event Collector |
| Edge Functions | Edge Functions Event Collector |
| WAF Events | WAF Event Collector |
| todos | Custom Template |

Ao selecionar um dos templates fornecidos pela Azion, você não consegue modificar as variáveis exibidas no campo de código **Data Set**. Ao selecionar **Custom Template**, você consegue personalizar quais variáveis quer usar de acordo com suas necessidades.

> Veja o guia [Como criar um template personalizado no Data Streaming](https://www.azion.com/pt-br/documentacao/produtos/guias/data-streaming-template-personalizado/) para mais informações sobre como personalizar o seu **Data Set**.

–-

## Domínios

Você pode associar os seus [domains existentes]({https://www.azion.com/pt-br/documentacao/produtos/edge-application/domains/) registrados na Azion ao seu data streaming. Se você ainda não tem um domínio registrado na sua conta, veja a documentação sobre [Criar um novo domínio associado a sua edge application](https://www.azion.com/pt-br/documentacao/produtos/ponto-de-partida/#crie-dominio).

Ao associar um domínio, os eventos relacionados a esse ou a esses domínios específicos são coletados e enviados para seu endpoint. Você pode associar um ou mais domínios e você tem a opção de filtrar domínios com **Filter Domains** ou selecionar todos os domínios com **All Domains**.

Ao selecionar **All Domains**, a plataforma seleciona automaticamente todos os domínios atuais e *futuros* de sua conta no RTM.

> Veja o guia [Como associar domínios no Data Streaming](https://www.azion.com/pt-br/documentacao/produtos/guias/data-streaming-associar-dominios/) para mais informações sobre como usar esse campo.

Se você selecionar a opção **All Domains**, você também pode configurar a porcentagem de dados que quer receber, de forma aleatória, do seu data streaming através da opção de *Sampling*. Além de filtrar por amostra, a opção também reduz custos de coleta e análise de dados.

> No momento, a opção *Sampling* não está disponíveis para todas as contas do RTM. Se você deseja usá-la em sua conta, [contate nosso time de vendas](https://www.azion.com/pt-br/contate-vendas/).

Para habilitar o sampling no RTM, no campo **Sampling (%)**, insira o número para a *porcentagem* de dados que quer receber. Essa porcentagem retornará dados relacionados a todos os seus domínios.

Quando a opção de Sampling está habilitada, você só pode adicionar *um* data streaming em sua conta. Após esse data streaming ser desabilitado, a opção **Add Streaming** é habilitada novamente na tela do Data Streaming no RTM.

–-

## Payload

> Esta funcionalidade só está disponível para o endpoint **Standard HTTP/HTTPS POST**.

Ao usar o endpoint Standard HTTP/HTTPS POST, o payload para o seu endpoint não é pré-definido. Você tem a opção de personalizar as informações essenciais que serão enviadas em seus dados da forma que achar melhor.

Para personalizar o payload enviado pelo conector no **Data Streaming**, você tem os seguintes campos:

- **Max Size** (*opcional*): define, em bytes, o tamanho de pacotes de dados que serão enviados. Aceita valores a partir de *1000000*.
- **Log Line Separator** (*opcional*): define que informação será usada no fim de cada linha de registro (log). Usado para quebrar informações em linhas diferentes.
- **Payload Format** (*opcional*): define qual informação será enviada em seus dados para cada requisição de data streaming.

Por padrão, o Data Streaming recomenda o formato NDJSON com o uso de `\n` como um log line separator e $dataset como payload format, que usa as informações fornecidas no campo de código **Data Set**, descrevendo as variáveis escolhidas como template.

Você pode escolher outras opções para ambos os campos. Dependendo dos tipos de seus registros, você pode usar `,` como log line separator, por exemplo.

O formato NDJSON não usa os arrays típicos de JSON `[]`, e cada dado é apresentado em uma linha diferente, sem vírgula separando-as. Ele pode ser útil para dados estruturados com processamentos de um registro por vez. Já o formato JSON é o mais conhecido e possui tabulação de dados, usando arrays `[]` e sendo separado por vírgulas. Com ele, o payload pode ser tratado como um registro individual.

Por exemplo, se o **Log Line Separator** receber `,` e o **Payload Format** receber `[$dataset]`, e o template tem as seguintes variáveis no campo de código **Data Set**:

$request_method\
$host\
$status

Você receberá uma resposta em JSON semelhante a isso:

```JSON
    [
        {
            "request_method": "GET",
            "host": "www.onedomain.com",
          "status": "200"
        },
        {
            "request_method": "POST",
            "host": "www.anotherdomain.com.br",
            "status": "200"
        }
    ]
```

Mas se o **Log Line Separator** receber `\n` e o **Payload Format** receber `$dataset`, você receberá uma resposta em NDJSON semelhante a isso:

```JSON
{"request_method": "GET", "host": "www.onedomain.com", "status": "200"}
{"request_method": "POST", "host": "www.anotherdomain.com.br", "status": "200"}
```

### Personalizando o payload com Activity History

Você pode personalizar o payload com informações específicas se você está usando o data source [Activity History](#activity-history) e o endpoint [Standard HTTP/HTTPS POST](#standard-http-https-post).

As seguintes informações devem ser usadas nos campos de payload para configurá-lo:

- **Log Line Separator**: \n
- **Payload Format**: 'v1\t$time_iso8601\t$clientid\t$title\t$comment\t$type\t$author_name\t$author_email'

–-

## Status code {#status-code}


Os servidores do **Data Streaming** funcionam em duas etapas: monitoram os endpoints uma vez por minuto (1x/min) e declaram o endpoint como *available*, disponível, ou *unavailable*, indisponível.


O Data Streaming tenta enviar mensagens para endpoints que estão *available*. Se o endpoint estiver *unavailable*, as mensagens não são enviadas, pois as informações são descartadas. No minuto seguinte, o Data Streaming faz o envio dos dados novamente se o endpoint ficar *available*.


Para ser considerado como *available*, o endpoint deve ser aprovado por todos os servidores da Azion. Se um dos servidores indicar que o endpoint está *unavailable*, as mensagens não são enviadas.


### Comportamento do status HTTP 504


Ocorre quando o endpoint responde ao teste com sucesso, mas não recebe as mensagens dentro do tempo de timeout: *20 segundos* para endpoints do tipo HTTP POST.


### Comportamento do status HTTP 503


Ocorre quando o endpoint é declarado como *unavailable*, indisponível, pela monitoração do endpoint. Portanto, o Data Streaming não tenta enviar as mensagens.


Como o sistema é distribuído, não é possível saber qual o servidor específico que envia as mensagens para cada endpoint.
