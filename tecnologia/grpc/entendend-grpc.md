# Entendendo GRPC

o **gRPC** é um framework open source baseado na tecnologia **RPC (Remote Procedure Call)**, criado pelo Google em 2015. Ele foi projetado para conectar serviços de maneira altamente eficiente, o que o tornou uma escolha natural para arquiteturas de microserviços.
=======
o **gRPC** é um framework open source baseado na tecnologia **RPC (Remote Procedure Call)** criado pelo Google em 2015. Ele foi projetado para conectar serviços de maneira altamente eficiente, o que o tornou uma escolha natural para arquiteturas de microsserviços.
>>>>>>> 9c6e8f2 (fix text)
Diferentemente do modelo **REST** que utiliza o formato JSON sobre o protocolo **HTTP/1.1**, o gRPC é notoriamente mais performático pois adota o **HTTP/2** como transporte e os **Protocol Buffers (Protobuff)** como sua linguagem de definição de interface (IDL) e formato de serialização binária.

## A Evolução do Protocolo de Transporte: Do HTTP/1.1 ao HTTP/2
Antes de tentarmos entender o motivo pelo qual gRPC é dito como superior ao REST, é necessário compreender os protocolos de transporte, que definem as regras de empacotamento e entrega de dados na rede. O **HTTP/1.1**, embora tenha sido o padrão da web por décadas, possui limitações de desempenho que o **HTTP/2** resolveu.

A principal diferença entre os dois se dá pela maneira como os dados são processados: 
- O **HTTP/1.1** transmite informações como texto puro, o que exige um processamento mais pesado e consequentemente mais lento.
- O **HTTP/2** utiliza o formato binário para transmitir informações, permitindo que os computadores leiam as sequências de bits diretamente sem a necessidade de converter o texto em binário, resultando em uma comunicação muito mais rápida.
Além disso, o **HTTP/2** introduz o conceito de **Multiplexação** que permite enviar e receber múltiplas requisições simultaneamente através de uma única conexão **TCP**, reduzindo drasticamente a latência. Diferentemente do **HTTP/1.1** que não possui multiplexação e para cada arquivo ou recurso solicitado o navegador precisa abrir várias conexões **TCP** sequenciais ou paralelas; Ademais, o protocolo é **bidirecional**, ao contrário do **HTTP/1.1**, onde apenas o cliente inicia a comunicação, o **HTTP/2** permite que o servidor envie dados de forma proativa enquanto a conexão estiver aberta, funcionando de forma semelhante ao websockets 

## Contratos e Tipagem com Protocol Buffers
Como dito anteriormente, o gRPC utiliza uma **IDL (Interface Definiton Language)** chamada **Protocol Buffers (Protobuf)** para realizar a comunicação de maneira eficiente. Uma **IDL** funciona com uma linguagem neutra para descrever o contrato entre serviços, permitindo que definamos a interface uma única vez e gere o código para linguagens de programação automaticamente. Os arquivos de **protobuf** possuem a extensão `.proto`onde os desenvolvedores descrevem detalhadamente quais métodos o serviço oferece, quais paramêtros são esperados e qual o formato exato da resposta. Essa estrutura não apenas garante a consistência dos dados, mas também aumenta a manutenabilidade e a evolucionabilidade dos sistemas.

Abaixo, temos um exemplo prático de como um serviço de usuário é definido utilizando a sintaxe do **proto3**:

```protobuff
syntax = "proto3";

package user;

// A opção go_package define onde o código gerado ficará (exemplo em Go)
option go_package = "./pb";

// O serviço define quais operações estão disponíveis
service UserService {
  rpc CreateUser (CreateUserRequest) returns (UserResponse);
  rpc GetUser (GetUserRequest) returns (UserResponse);
  rpc UpdateUser (UpdateUserRequest) returns (UserResponse);
  rpc DeleteUser (DeleteUserRequest) returns (DeleteUserResponse);
}

// Representação da entidade Usuário
message User {
  string id = 1;
  string name = 2;
  string email = 3;
  int32 age = 4;
}

// Mensagens de Requisição (Request)
message CreateUserRequest {
  string name = 1;
  string email = 2;
  int32 age = 3;
}

message GetUserRequest {
  string id = 1;
}

message UpdateUserRequest {
  string id = 1;
  string name = 2;
  string email = 3;
}

message DeleteUserRequest {
  string id = 1;
}

// Mensagens de Resposta (Response)
message UserResponse {
  User user = 1;
}

message DeleteUserResponse {
  string message = 1;
  bool success = 2;
}
```

Referências: 
[Introdução ao gRPC - Golang](https://dev.to/thenicolau/introducao-ao-grpc-golang-210f)
[gRPC: onde vive? o que come?](https://dev.to/mfbmina/grpc-onde-vive-o-que-come-5049)
