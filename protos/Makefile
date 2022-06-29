BIN := "./bin/calendar"
DOCKER_IMG="calendar:develop"

GIT_HASH := $(shell git log --format="%h" -n 1)
LDFLAGS := -X main.release="develop" -X main.buildDate=$(shell date -u +%Y-%m-%dT%H:%M:%S) -X main.gitHash=$(GIT_HASH)

PATH_GEN_GOLANG_GRPC := ../gen/go/grpc/calendar/v1
PATH_GEN_GOLANG_GRPC_GATEWAY := ../gen/go/grpc-gateway/calendar/v1

gen-grpc:
	protoc -I . --go_out $(PATH_GEN_GOLANG_GRPC) --go_opt paths=source_relative \
	--go-grpc_out $(PATH_GEN_GOLANG_GRPC) --go-grpc_opt paths=source_relative \
	server.proto

gen-grpc-gateway:
	protoc -I . --grpc-gateway_out $(PATH_GEN_GOLANG_GRPC_GATEWAY) \
    --grpc-gateway_opt logtostderr=true \
    --grpc-gateway_opt paths=source_relative \
    --grpc-gateway_opt generate_unbound_methods=true \
    server.proto

gen-server:
	gen-grpc:
	gen-grpc-gateway:
