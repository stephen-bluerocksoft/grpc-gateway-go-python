# README

## Setup Python Server

```shell
python3 -m pip install grpcio
python3 -m pip install grpcio-tools
python3 -m grpc_tools.protoc -I./proto/helloworld -I./proto --python_out=. --pyi_out=. --grpc_python_out=. helloworld.proto
python3 greeter_server.py
```

## Setup Go Client

```shell
go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.28
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.2
export PATH="$PATH:$(go env GOPATH)/bin"
protoc -I ./proto --go_out ./proto --go_opt paths=source_relative --go-grpc_out ./proto --go-grpc_opt paths=source_relative --grpc-gateway_out ./proto --grpc-gateway_opt paths=source_relative ./proto/helloworld/helloworld.proto
go mod init helloworld
go get google.golang.org/grpc
go get google.golang.org/grpc/credentials/insecure
go get github.com/grpc-ecosystem/grpc-gateway/v2/runtime
go get github.com/grpc-ecosystem/grpc-gateway/v2/utilities
go mod download github.com/golang/glog
go mod tidy
go run main.go
```

## Hit REST endpoint

`curl -H "Content-Type: application/json" -d '{"name":"WORLD"}' http://localhost:8081/v1/example/echo`