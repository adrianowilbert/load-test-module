# load-test-module #
Modulo de teste de carga na linguagem Scala para estudos.
Este modulo pode ser incluído em qualquer projeto de API's dentro do pacote `src`.

| **WILBERT** | [Adriano Wilbert](https://github.com/adrianowilbert) _(adrianowilbert@gmail.com.br)_

### Modulo

Este módulo utiliza as seguintes tecnologias:

  IDE - [IntelliJ](https://www.jetbrains.com/idea/).

  Framework - [gatling](http://gatling.io/). 
  
  Linguagem - [Scala](https://www.scala-lang.org/).

### API

Projeto utliza a API de código aberto: http://fakerestapi.azurewebsites.net/swagger/ui/index

#### Linha de comando

Para executar os testes por linha de comando:

```shell - impedidos
mvn package -Dgatling.simulationClass=br.com.lojasrenner.api.impedidos.simulation.ConsultaListaWorldCheck -f src/load-test/pom.xml
```

#### Estrutura do Modulo

    |- load-test-module
        |- docker
        |- src
            |- test
                |- resources
                    |- bodies
                    |- data
                |- scala
                    |- br.com.cliente
                         |- api.loadTest
                             |- operation
                             |- simulation
                         |- header
                         |- http
                         |- utils      
    |- target 
    
#### Arquivo GIT Ignore

O arquivo .gitignore do projeto de API deve ser substituído pelo .gitignore encontrado no módulo.

#### Transformando o Modulo em um projeto MAVEN

O modulo precisa ser transformado em um projeto maven após inserido no projeto.
     
         1. Clica em `Maven Projects` no canto superior a esquerda do projeto
         2. Clica no botão +
         3. Procura a pasta do módulo
         4. Clica no `pom` do módulo
         5. Modulo se transformará em um projeto Maven

#### Estrutura do Pacote Detalhamento

- docker:
    Responsável pela execução dos testes baseados em containers de execução

- src/test/resources:
    - `bodies` contém modelos para corpos de solicitação (exemplo: elementos que contêm no `contem type`)
    - `data` contém arquivos alimentadores (exemplo: csv com dados a serem utilizados)
    
- src/test/scala/br.com.cliente/api.nomeApi:
    - `operation` contém métodos dos processos de testes (exemplo: geração de build)
    - `simulation` contém fluxos de testes a serem executados (especificamente os testes)
    
- src/test/scala/br.com.cliente:
    - `header` contém os elementos do cabeçalho (exemplo: inserção do token)
    - `http` contém as bases das url (exemplo: constrói os url dos endpoints)
    - `utils` contém os utils (exemplo: classes randômicas)
    
- target
    Elementos substituídos a cada execução de testes.
   
#### Comandos Docker

- Comandos para usar no terminal:
    - `docker-compose up` executa o arquivo de composição para rodar os testes
    - `Ctrl+c` pausa os teste
    - `docker-compose dow` limpa o recipiente e finaliza os testes
    
    #### docker-compose
    
    Para executar os testes em uma estrutura de containes para acompanhar os testes em tempo real no Grafana.
    ```shell
    cd src\load-test\docker
    docker-compose up -d
    ```
    
    Para interromper os testes
    ```shell
    Ctrl+C
    ```
    
    Para limpar os recepientes e finalizar os testes
    ```shell
    docker-compose down
    ```
    
    Acompanhar a execução do gatling.
    ```shell
    cd src\load-test\docker
    docker-compose logs -f gatling
    ```
    
    Para e reconfigurar o gatling.
    ```shell
    docker-compose stop gatling
    docker-compose start gatling
    ```
    
    Gerar os reports após a execução (quando não for habilitado reports ao fim de cada simulação)
    ```shell
    docker-compose.exe -f docker-compose-reports.yml run --rm reports
    ```
    
    Remover todos os containers
    ```shell
    docker-compose.exe down --remove-orphans
    ```
    
- Endereço para acompanhar os testes:
    - [Grafana LocalHost](http://localhost:8081).