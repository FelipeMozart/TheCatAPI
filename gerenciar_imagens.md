# Gestão de imagens

Encontre aqui os passos necessários para gerenciar imagens dos felinos na TheCatAPI. 

## Visão Geral

Aprenda como manter seu repositório realizando a gestão das imagens dos felinos no repositório. Saiba como:

- Adicionar uma nova imagem ao repositório;
- Buscar uma imagem adicionada;
- Consultar a lista de imagens adicionadas ao repositório;
- Apagar um registro de uma imagem disponível no repositório.



### 1. Adicionar uma nova imagem ao repositório

Para adicionar uma nova imagem ao repositório você deve ter uma biblioteca de imagens disponíveis para upload. 


#### 1.1 Requisição 

Utilize o endpoint `POST images/upload` para criar um registro de uma nova imagem, com o corpo da requisição contendo a imagem, por exemplo:

**Request body**

| Nome | Descrição | Tipo | Obrigatório |
|------|-----------|------|-------------|
| `file` | Arquivo em .gif, .png, ou .jpg | `file` | Sim |
| `sub_id` | ID para identificação interna. | `string` | Não |

```c
curl 
--request POST 'https://api.thecatapi.com/v1/images/upload' \
--header 'x-api-key: live_2du7MqgVFkeexQfcCL0Vn738CK9AnmW1Ye20vPbZ35WFKv507Y3NAGQYnt7hIbOB' \
--form 'file=@"ulnqKIZpy/image0001.jpg"'
```


> O `form` será preenchido com valor = arquivo/nomeimagem.formato. No exemplo acima = 'file=@"ulnqKIZpy/image0001.jpg"'


#### 1.2 Resposta

Após adicionar a imagem escolhida da sua biblioteca em seu repositório.
A resposta de código  `200 OK` indica que a imagem já está disponível no repositório TheCatAPI.

```json
{
    "id": "AfysaoY_W",
    "url": "https://cdn2.thecatapi.com/images/AfysaoY_W.jpg",
    "width": 360,
    "height": 360,
    "original_filename": "image0001.jpg",
    "pending": 0,
    "approved": 1
}
```
Para buscar a imagem no repositório siga o passo abaixo.


### 2. Buscar imagem recém adicionada por ID

Siga os passos abaixo para encontrar uma imagem que adicionada ao repositório pelo `ID`.

#### 2.1 Requisição

Utilize o endpoint  `GET /images/{image_id}` para buscar uma imagem.

Obtém a imagem correspondente ao parâmetro `image_id` passado como parâmetro `path`.


Neste exemplo, o parâmetro `image_id` utilizado é o mesmo encontrado na resposta do passo anterior: `GET /images/AfysaoY_W`


#### 2.2 Resposta

Após adicionar o `ID` da imagem, a resposta de código  `200 OK` indica sucesso.

```json
{
    "id": "AfysaoY_W",
    "url": "https://cdn2.thecatapi.com/images/AfysaoY_W.jpg",
    "width": 360,
    "height": 360,
    "sub_id": null
}
```

## 3. Consultar a lista de imagens adicionadas ao repositório;

Saiba como consultar uma lista de imagens disponíveis no repositório.


#### 3.1 Requisição

Para buscar uma lista de imagens disponíveis no repositório utilize o endpoint `GET /image`. Os resultados podem ser filtrados através dos parâmteros `query` abaixo:

| Parâmetro |    Descrição      | Tipo | Obrigatório |
|------------|--------------------|------|------------|
| `limit`  | Número de resultados a serem retornados. O valor máximo é 25. O padrão é 1. | `integer` | Sim |
| `mime_types` | Os tipos de imagem a serem retornados: .gif, .jpg, ou .png. Retorna todos os tipos como padrão. | `string` delimitado por vírgulas. | Não |
| `order` | A ordem de retorno: RANDOM, ASC ou DESC. O padrão é RANDOM. | `string` | Não  |


#### 3.2 Resposta

A resposta de código  `200 OK` indica sucesso.

> No caso do exemplo abaixo foram utilizadas as `queries`: `limit 3` ; `mime_types .jpg` ; `order DESC` . 

```json
[
    {
        "breeds": [],
        "id": "AfysaoY_W",
        "url": "https://cdn2.thecatapi.com/images/AfysaoY_W.jpg",
        "width": 360,
        "height": 360,
        "sub_id": null,
        "created_at": "2022-12-01T15:44:59.000Z",
        "original_filename": "image0001.jpg",
        "breed_ids": null
    },
    {
        "breeds": [],
        "id": "m7GJR3Ubx",
        "url": "https://cdn2.thecatapi.com/images/m7GJR3Ubx.jpg",
        "width": 360,
        "height": 360,
        "sub_id": null,
        "created_at": "2022-12-01T15:18:06.000Z",
        "original_filename": "cat_01.jpg",
        "breed_ids": null
    },
    {
        "breeds": [],
        "id": "S1NMmWujv",
        "url": "https://cdn2.thecatapi.com/images/S1NMmWujv.jpg",
        "width": 360,
        "height": 360,
        "sub_id": null,
        "created_at": "2022-12-01T15:12:54.000Z",
        "original_filename": "cat_01.jpg",
        "breed_ids": null
    }
]
```


## 4 Apagar um registro de uma imagem disponível no repositório.

O passo abaixo lhe indica como deletar uma imagem que está no repositório.

#### 4.1 Requisição

Use o endpoint `DELETE /images/{image_id}` para excluir uma imagem.

Para este exemplo `image_id = AfysaoY_W`


#### 4.2 Resposta 

A resposta de código `204 No Content` indica sucesso na exclusão da imagem.


