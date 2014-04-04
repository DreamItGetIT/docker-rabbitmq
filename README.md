### Learning Docker http://docker.io/ by creating a RabbitMQ container.

http://docs.docker.io/en/latest/use/builder/#dockerfile-examples

http://www.rabbitmq.com/install-debian.html

Blog describing the breaking changes in RabbitMQ 3.3
http://www.rabbitmq.com/blog/2014/04/02/breaking-things-with-rabbitmq-3-3/

Enabling access for the default guest user to login from remote machine
http://www.rabbitmq.com/access-control.html


### To build:

    sudo docker build -t docker/rabbitmq .

### To run:

    sudo docker run -p :5672 -p :15672 docker/rabbitmq
    
### To persist your data:

Here we persistently save our data to the host machine's ``/tmp/rabbitmq/mnesia`` directory.

    mkdir -p /tmp/rabbitmq/mnesia
    chmod 777 /tmp/rabbitmq/mnesia
    sudo docker run -h rabbithost -p :5672 -p :15672 -v /tmp/rabbitmq/mnesia:/var/lib/rabbitmq/mnesia docker/rabbitmq

Since RabbitMQ uses the ``$HOSTNAME`` in its data path, we need to explicitly set it for the container.

    $ sudo docker run -h rabbithost -p :5672 -p :15672 -v /tmp/rabbitmq/mnesia:/var/lib/rabbitmq/mnesia docker/rabbitmq
    WARNING: Docker detected local DNS server on resolv.conf. Using default external servers: [8.8.8.8 8.8.4.4]
    
                  RabbitMQ 3.1.5. Copyright (C) 2007-2013 GoPivotal, Inc.
      ##  ##      Licensed under the MPL.  See http://www.rabbitmq.com/
      ##  ##
      ##########  Logs: /var/log/rabbitmq/rabbit@rabbithost.log
      ######  ##        /var/log/rabbitmq/rabbit@rabbithost-sasl.log
      ##########
                  Starting broker... completed with 6 plugins.


### To run as a daemon use -d
    sudo docker run -d -p :5672 -p :15672 docker/rabbitmq
    
### To explicitly bind machine port to the container use the following command
    sudo docker run -d -p 5672:5672 -p 15672:15672 docker/rabbitmq

### Use the following url to access RabbitMQ Admin
    localhost:15672
