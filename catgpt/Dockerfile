FROM golang:1.21-alpine AS build-stage

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY *.go ./
COPY *.png ./
COPY tpl/ ./tpl/

RUN CGO_ENABLED=0 GOOS=linux go build -o /catgpt

FROM gcr.io/distroless/static-debian12 AS build-release-stage

WORKDIR /

COPY --from=build-stage /catgpt /catgpt

EXPOSE 8080

CMD [ "/catgpt" ]