# Use the official RabbitMQ image from Docker Hub
FROM rabbitmq

# Set environment variables for default user and password
ENV RABBITMQ_DEFAULT_USER=guest
ENV RABBITMQ_DEFAULT_PASS=guest

# Expose port 15672 for the RabbitMQ management plugin (web UI)
EXPOSE 15672

# Expose RabbitMQ default port 5672 (for client connections)
EXPOSE 5672

# Start RabbitMQ with the default command
CMD ["rabbitmq-server"]

