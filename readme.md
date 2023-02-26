# Loxley gRPC Web

Using the DB as the source of truth for grpc-web automatic resource binding in a TypeScript frontend

## Backend

* use sea-orm to write migrations
* use sea-orm-cli to generate serde rust structs
* write serde rust structs to protobuf schema /protos
  * for now, write custom services for those protobuf schema
  * could have CRUD endpoints autogenerated in future and then add custom ones for other data
* use tonic(-web) to serve data via grpc-web endpoints
  * can ignore unimplemented endpoints with a simple return `Err(Status::unimplemented(message: impl Into<String>));`
  * requests will require some protobuf <-> sea-orm serialisation

## Frontend

* use npx protoc to generate grpc+protobuf interfaces, class, messages and bindings, making for a strongly typed db-led way of performing server calls
  * npm run build:protos
* use protobuf-ts send data via gRPC-web
