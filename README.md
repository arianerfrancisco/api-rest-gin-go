![1 YcFmahlLvOPyjfNtw1GkbQ](https://user-images.githubusercontent.com/72419533/183143696-b7af4347-a970-42f9-bcda-32ba3db58eb9.png)

<h1 align="center"> Integração contínua e entrega contínua (CI/CD) </h1>

## As rotinas de integração contínua foram divididas em dois jobs: test e build.

No job test, tem-se o seguinte log:

    Set up job
    Run actions/checkout@v3
    Set up Go
    Build-DB
    Create-DB
    Test
    Post Set up Go
    Post Run actions/checkout@v3
    Complete job

O GitHub Actions primeiro preparou o job, rodou o actions/checkout@v3 e preparou o Go. 
Em seguida, o banco de dados foi preparado. Nos detalhes, nota-se que tanto o Postgres quanto o pgAdmin são imagens, portanto não há nada para ser feito nessa etapa.
Depois, o GitHub Actions criou o banco de dados, rodando docker-compose up -d, trazendo as imagens e subindo o Postgres e o pgAdmin (ambos constam como "done).
Na sequência, os testes foram executados com o comando go test -v main_test.go.
Ele trouxe todas as bibliotecas necessárias e, por fim, executou os testes automatizados. Podemos ver, por exemplo, que RUN TesteVerificaStatusCodeDaSaudacaoComParametro no /gui passou.


No job build:

    Set up job
    Run actions/checkout@v3
    Build
    Post Run actions/checkout@v3
    Complete job

Preparou-se o job e rodou o actions/checkout@v3.
Executou o build com o comando go build -v main.go. 

Créditos: Curso Alura
