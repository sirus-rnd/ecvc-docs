# Dokumentasi Penggunaan API Linimasa

Linimasa API menggunakan schema [graphql](https://graphql.org/) yang dapat diakses melalui `http` webservice pada alamat [https://ecvc.linimasa.app/graphql](https://ecvc.linimasa.app/graphql)

## Prosedur pengunaan

1. mintalah `access token` kepada kami. satu `access token` hanya dapat digunakan untuk 1 provider saja. Apabila ada penambahan provider, anda harus meminta access token baru.
1. request API dilakukan dengan menggunakan format request sebagai berikut [serving over http](https://graphql.org/learn/serving-over-http/)
1. tambahkan `access token` pada `Authorization` request header

## Contoh penggunaan

contoh request menggunakan http post

```http
POST /graphql HTTP/1.1
Accept: application/json
Authorization: Bearer $ACCESS_TOKEN
Host: ecvc.linimasa.app

{
  "query": "query { profile { me { name } } }",
  "operationName": "getProfile",
  "variables": {}
}
```

contoh response

```http
HTTP/1.1 200 OK                                               
Access-Control-Allow-Origin: *                                
Connection: keep-alive                                        
Content-Length: 65                                            
Content-Type: application/json; charset=utf-8                 
Date: Thu, 26 Mar 2020 05:57:14 GMT                           
ETag: W/"41-r4m70BkMnYV2gtHfQcuZlXCC8q4"                      
Server: openresty/1.15.8.2                                    
Strict-Transport-Security: max-age=15724800; includeSubDomains
X-Powered-By: Express                                         
                                                              
{                                                             
    "data": {                                                 
        "profile": {                                          
            "me": {                                           
                "name": "klinik sehat root account"           
            }                                                 
        }                                                     
    }                                                         
}                                                             
```

contoh request menggunakan parameter

```http
POST /graphql HTTP/1.1
Accept: application/json
Authorization: Bearer $ACCESS_TOKEN
Host: ecvc.linimasa.app

{
  "query": "query getFacility($id: String!){ facility { byID(id: $id) { name } } }",
  "operationName": "getFacility",
  "variables": { "id": "x-9191" }
}
```

## Playground

anda dapat mencoba query dengan menggunakan `query playground` yang tersedia di [https://ecvc.linimasa.app/graphql](https://ecvc.linimasa.app/graphql)

1. masukkan `access token` pada tab `header` di pojok kiri bawah
    
    ```json
    {
      "Authorization": "Bearer $ACCESS_TOKEN"
    }
    ```

1. tulis `query` yang anda inginkan dengan menggunakan graphql syntax

    ```gql
    query {
      profile {
        me {
          name
        }
      }
    }
    ```

1. ketik `ctrl+enter` atau anda dapat memencet tombol "play" ditengah playground
1. dokumentasi schema terdapat di tab di sebelah kanan yang bertuliskan `docs`
1. penggunaan lebih lajut dapat dibaca di [https://github.com/prisma-labs/graphql-playground](https://github.com/prisma-labs/graphql-playground)
