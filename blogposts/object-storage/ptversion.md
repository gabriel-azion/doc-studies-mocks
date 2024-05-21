Text: ---
schema: blog_post
title: Aprimorando a gestão de dados com o Edge Storage da Azion
authors:
    - src/content/authors/gabriel.franca.md
meta_tags: azion, edge storage, object storage, gestão de dados, serverless, s3 api
excerpt: >-
    Descubra como o Edge Storage da Azion simplifica a gestão de dados e aprimora o desempenho de aplicações. Aprenda sobre os benefícios do armazenamento de objetos no edge da rede e como aproveitá-lo usando a API REST da Azion, CLI e a API de Storage das Edge Functions.
description: >-
    Este blog mergulha no Azion Edge Storage, uma solução de armazenamento de objetos projetada para simplificar a gestão de dados e melhorar o desempenho da aplicação. O post abrange os principais benefícios, configuração, e a gestão de dados usando S3 API, REST API, Azion CLI e Edge Functions Storage API.
img_featured: >-
    /assets/blog/images/uploads/storage-image.png
categories:
    - desenvolvedores
related_content:
namespace: blogpost_azion_edge_storage
date: 2024-05-09T06:00:00Z
date_updated:
resourceHub:
    flags:
        contentType: Blog
permalink: /aprimorando-a-gestao-de-dados-com-azion-edge-storage/

---

Como desenvolvedores, navegar pelo complexo mundo do armazenamento de dados pode parecer intimidante. Há uma necessidade constante de gerenciar volumes crescentes de dados, garantir rápida acessibilidade e manter o desempenho do sistema.

E se você pudesse aproveitar o conceito de Object Storage, implantando seus dados no edge, beneficiando-se de acesso de baixa latência, escalabilidade, custo previsível e alta disponibilidade sem ter que lidar com as complexidades dos sistemas de armazenamento tradicionais?

Neste blog, mergulhamos no Azion Edge Storage, uma solução de armazenamento de objetos projetada com os desenvolvedores em mente, simplificando o processo de gestão de dados e potencializando o desempenho das aplicações.

---

## Object Storage no Edge

Através do Azion Edge Storage, a gestão de ativos como imagens e arquivos pode ser realizada sem se envolver nas complexidades do gerenciamento de infraestrutura. Isso permite que os usuários se concentrem em construir aplicações inovadoras, evitando quaisquer obstáculos de infraestrutura.

Os principais benefícios incluem:

- API compatível com S3: esta compatibilidade facilita a migração de outros sistemas de armazenamento em nuvem que usam a API S3, permitindo a transição sem a necessidade de alterar o código existente.
- Escalabilidade: a escalabilidade ilimitada fornecida pelas infraestruturas edge remove qualquer restrição de capacidade de armazenamento. Os usuários podem ajustar o armazenamento de acordo com suas demandas.
- Confiabilidade: o edge garante desempenho confiável e consistente.
- Previsibilidade de custo: custos inesperados podem ser evitados mantendo as despesas de transferência de dados dentro de orçamentos predeterminados.
- Arquitetura sem servidor (serverless): a arquitetura serverless traz um modelo prático de desenvolvimento de aplicações, enfatizando simplicidade e adaptabilidade.
- Evitar bloqueio do fornecedor: essa flexibilidade facilita a tomada de decisões estratégicas e promove preços competitivos.
- Sem mais cobrança de saída (egress charge): com o edge computing, o processamento de dados acontece mais próximo da fonte, minimizando os volumes de transferência de dados para e do servidor central. Como resultado, as empresas podem evitar a alta despesa de saída frequentemente associada aos serviços de nuvem, economizando nos custos operacionais.

---

## Configurando e Simplificando a Gestão de Dados

Edge Storage gerencia dados através de objetos. Cada objeto inclui:

- Dados que compõem o objeto.
- Metadados associados, como o tipo de mídia e o tamanho do objeto.
- Uma chave de objeto como o identificador único.

### API S3

Edge Storage é compatível com a API S3. Este recurso funciona da seguinte forma:

1.  As credenciais podem ser gerenciadas através do endpoint `/s3-credentials`. Os métodos relacionados às credenciais incluem:

1. GET: recuperar dados em todas as credenciais S3 registradas no Azion.
1. GET por ID: recuperar dados em uma credencial S3 registrada no Azion.
1. POST: criar uma credencial S3.
2. DELETE: remover as credenciais S3 da conta.

2.  Uma vez que as credenciais são criadas, você pode usá-las através:

1. S3cmd
2. S3 API através do endpoint regional `https://s3.use-east-005.azionstorage.net/`
3. Bibliotecas relacionadas ao tratamento do S3 para a linguagem de programação escolhida.

Criando credenciais S3 para serem usadas com o Edge Storage:

```
curl --location 'https://api.azion.com/v4/storage/s3-credentials \
--header 'Accept: application/json' \
--header 'Authorization: Token xxxxxxx \
--header 'Content-Type: application/json' \
--data '{
  "name": "My S3 Credential",
  "capabilities": ["listAllBucketNames", "listFiles"],
  "bucket": "my-bucket-name",
  // expiration based on the timezone defined in RTM settings
  "expiration_date": "2025-01-31T10:57:00"

}'
```

Configurando as suas credenciais no S3cmd:

```
user@user ~ % s3cmd --configure
Enter new values or accept defaults in brackets with Enter.
Refer to user manual for detailed description of all options.
Access key and Secret key are your identifiers for Amazon S3. Leave them empty for using the env variables.
Access Key: [your-recently-created-access-key]
Secret Key:  [your-recently-created-secret]
Default Region....
S3 Endpoint [s3.amazonaws.com]: https://s3.use-east-005.azionstorage.net/
```

Agora, você pode acessar e manipular objetos através do S3cmd dependendo das capacidades atribuídas à credencial S3.

Enviando um objeto usando a API S3

```
curl --location --request PUT 'https://s3.us-east-005.azionstorage.net/<bucket_name>/<object_key>' \
    --header 'Content-Type: text/plain' \
    --header 'X-Amz-Date: 20240304T125612Z' \
    --header 'Authorization: AWS4-HMAC-SHA256 Credential=<access_key>/<date>/us-east-1/execute-api/aws4_request, SignedHeaders=content-length;content-type;host;x-amz-date, Signature=<encrypted_signature>' \
    --data '<filepath>'
```

Um usuário, desde que esteja atribuído a uma equipe com a permissão Editar Credenciais de Armazenamento, pode criar credenciais que serão visíveis para outros usuários na mesma conta. Quando uma credencial é criada, ela não pode ser editada, e as chaves secretas só serão apresentadas no momento da criação. Dessa forma, ao visualizar uma credencial depois de ter sido criada, as chaves serão omitidas.

As credenciais podem ser atribuídas a um determinado bucket ou a todos os buckets criados pela conta, mas não a um grupo de buckets. Embora seja possível criar um conjunto de credenciais, elas não terão poderes de gestão sobre o bucket ou as próprias credenciais - a gestão de buckets e credenciais só pode ser realizada através da API REST.

No entanto, as credenciais proporcionam um conjunto específico de operações possíveis relacionadas aos objetos no bucket. Com credenciais apropriadas, é possível realizar operações como listar, ler, modificar e excluir objetos, dado que o bucket tenha as permissões necessárias. As credenciais S3 operam separadamente do nível de acesso definido para o bucket usando a API REST, definido pela propriedade `edge_access`. Por exemplo, se uma credencial com a capacidade `writeFiles` for criada para um bucket com permissões `read_only`, a credencial ainda poderá ser usada para adicionar ou modificar arquivos no bucket, enquanto a API Azion não pode ser usada para essa mesma operação.

Embora o gerenciamento do bucket e das credenciais esteja limitado à API REST, os próprios objetos podem ser manipulados pelas credenciais com permissão.

---

### API Rest

A Azion oferece métodos de API REST para armazenar objetos, desde a criação e modificação de buckets e de suas permissões até a gestão de objetos.

Digamos que você deseje usar o armazenamento de objetos como a origem para uma Edge Application estática. Para isso, você precisa:

1. Criar um bucket.
2. Fazer upload do arquivo que contém sua aplicação dentro de um diretório `src`. Por exemplo:

```
src/index.html
```

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="styles/style.css">
</head>
<body>
    <h1>Hello world!</h1>
    <p>I am an object from a bucket.</p>
</body>
</html>

```

Você pode acessar as instruções passo a passo neste [guia](https://www.azion.com/en/documentation/products/guides/upload-and-download-objects-from-bucket/) para fazer upload e download de objetos de um bucket do Azion Edge Storage.

---

### Azion CLI

Outra alternativa é iniciar e implantar uma [aplicação através da Azion CLI](https://www.azion.com/en/documentation/devtools/cli/init/). Quando você inicializa uma aplicação através do comando `azion init` e a implanta no edge:

1.  Um bucket é automaticamente criado com o nome que você escolheu para o projeto.
2.  Sua aplicação estática é armazenada nele.

Você pode ver mais informações sobre [como implantar um aplicação através do guia da Azion CLI](https://www.azion.com/en/documentation/products/cli/frameworks/react/), que apresenta os passos para implantar uma aplicação React na plataforma.

---

### Azion Edge Functions Storage API

O Azion Edge Storage pode ser acessado através da [API de Storage das Edge Functions](https://www.azion.com/en/documentation/devtools/runtime/api-reference/storage/). Essa interface permite que você leia e escreva dados no storage e nos seus buckets associados.

Para começar com a API de Storage, você precisa:

1. Importar as APIs dentro de sua edge function:

```
import Storage from "azion:storage";
```

2. Instanciar um novo objeto Storage:

```
const storage = new Storage(bucket);
```

3. Escolher e implementar os [métodos listados na documentação](https://www.azion.com/en/documentation/devtools/runtime/api-reference/storage/).

---

## Conclusão

O Azion Edge Storage se apresenta como uma solução para os desafios de armazenamento e gestão de dados, transformando como os desenvolvedores abordam o desempenho das aplicações. Ao alavancar tecnologias de armazenamento de objetos no edge da rede, ele não apenas oferece benefícios-chave como escalabilidade, alta confiabilidade e previsibilidade de custo, mas também simplifica o processo de desenvolvimento.

Com a gestão de dados simplificada usando a API REST amigável ao usuário da Azion, a CLI e a API de Storage das Edge Functions, os desenvolvedores podem se concentrar em inovação em vez de desafios organizacionais. À medida que avançamos para o futuro com o Azion Edge Storage, não estamos apenas superando problemas de dados, estamos desbloqueando o enorme potencial que existe em nossos dados, prontos para potencializar nossas Edge Applications.