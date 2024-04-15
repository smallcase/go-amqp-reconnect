# streadway/amqp Conneciton/Channel auto reconnect wrap
rabbitmq/amqp091-go Connection/Channel does not reconnect if rabbitmq server restart/down and no cluster supported.

To simply developers, here is auto reconnect wrap with detail comments.

## How to change existing code
1. add import `import "github.com/smallcase/go-amqp-reconnect/rabbitmq"`
2. Replace `amqp.Connection`/`amqp.Channel` with `rabbitmq.Connection`/`rabbitmq.Channel`

## Example
### Close by developer
> go run example/close/demo.go

### Auto reconnect
> go run example/reconnect/demo.go

### RabbitMQ Cluster with Reconnect
```go
import "github.com/smallcase/go-amqp-reconnect/rabbitmq"

rabbitmq.DialCluster([]string{"amqp://usr:pwd@127.0.0.1:5672/vhost","amqp://usr:pwd@127.0.0.1:5673/vhost","amqp://usr:pwd@127.0.0.1:5674/vhost"})
```

### Set reconnect delay seconds

You can set reconnect delay seconds with environment variable "**AMQP_RECONN_DELAY_SECONDS**"
e.g. 
```sh
# Default to 3s.
export AMQP_RECONN_DELAY_SECONDS=10 
```