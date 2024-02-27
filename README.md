#  gRPC Connect
 gRPC 互換の HTTP API を実装するためのフレームワーク。 一般的な gRPC Server と同じように Protocol Buffers を用いて API を定義し、
 Server と Client のコードを生成することができる


1. install
```sh
$ mkdir connect-go-example
$ cd connect-go-example
$ go mod init example
$ go install github.com/bufbuild/buf/cmd/buf@latest
$ go install github.com/fullstorydev/grpcurl/cmd/grpcurl@latest
$ go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
$ go install connectrpc.com/connect/cmd/protoc-gen-connect-go@latest
```

2. protoの定義ファイルの作成
```sh
$ mkdir -p greet/v1
$ touch greet/v1/greet.proto
```

3. greet/v1/greet.proto ファイルの編集
```sh
syntax = "proto3";

package greet.v1;

option go_package = "example/gen/greet/v1;greetv1";

message GreetRequest {
  string name = 1;
}

message GreetResponse {
  string greeting = 1;
}

service GreetService {
  rpc Greet(GreetRequest) returns (GreetResponse) {}
}
```

4. buf.yamlファイルの作成
```sh
$ buf mod init
```

5. buf.gen.yaml ファイルの作成
``` sh
$ touch  buf.gen.yaml
``` 

6. lintとコード自動コード生成
```sh
$ buf lint
$ buf generate
```

7. cmd/server/main.goを作成
```sh
$ mkdir ...
```

8. main.goにサーバーの実装
```sh
$ go get golang.org/x/net/http2
$ go get connectrpc.com/connect
$ go run ./cmd/server/main.go
```


9. 別コマンドからリクエスト
```sh
$ curl \
    --header "Content-Type: application/json" \
    --data '{"name": "Jane"}' \
    http://localhost:8080/greet.v1.GreetService/Greet
```















