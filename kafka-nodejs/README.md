# Kafka Node.js Client - README

Welcome to the Kafka Node.js Client project! This client library allows you to interact with Apache Kafka using Node.js. It provides a convenient way to produce and consume messages from Kafka topics using asynchronous programming paradigms. Below, you'll find all the necessary information to get started with using this library.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
  - [Producer](#producer)
  - [Consumer](#consumer)
- [Configuration](#configuration)
- [Error Handling](#error-handling)
- [Contributing](#contributing)
- [License](#license)

## Installation

You can install the Kafka Node.js Client library using npm:

```bash
npm install kafka-nodejs-client
```

## Usage

### Producer

To send messages to a Kafka topic, you can use the `Producer` class provided by the library. Here's a simple example:

```javascript
const { Producer } = require('kafka-nodejs-client');

const producer = new Producer({
  kafkaBrokers: ['kafka-broker1:9092', 'kafka-broker2:9092'],
});

async function produceMessage(topic, message) {
  try {
    await producer.connect();
    await producer.send(topic, message);
  } catch (error) {
    console.error('Error producing message:', error);
  } finally {
    producer.disconnect();
  }
}

produceMessage('my-topic', 'Hello, Kafka!');
```

### Consumer

Consuming messages from Kafka topics can be achieved using the `Consumer` class. Here's a basic example:

```javascript
const { Consumer } = require('kafka-nodejs-client');

const consumer = new Consumer({
  kafkaBrokers: ['kafka-broker1:9092', 'kafka-broker2:9092'],
  groupId: 'my-group',
  topics: ['my-topic'],
});

consumer.on('message', (message) => {
  console.log('Received message:', message.value);
});

consumer.connect();
```

## Configuration

You can customize the behavior of the Kafka Node.js Client by providing various configuration options when creating the producer or consumer instance. Some common configuration options include:

- `kafkaBrokers`: An array of Kafka broker addresses.
- `groupId`: The consumer group ID.
- `topics`: An array of topics to subscribe to.
- `clientId`: A unique identifier for the client.
- `autoCommit`: Whether to enable automatic offset commits for consumers.

Refer to the library documentation for a complete list of configuration options.

## Error Handling

Both the `Producer` and `Consumer` classes handle errors internally. However, it's important to implement your own error handling to gracefully handle scenarios like connection failures, serialization errors, or invalid configurations. Always wrap your Kafka operations in try-catch blocks and handle errors appropriately.

## Contributing

We welcome contributions to the Kafka Node.js Client project! If you find any issues or have ideas for improvements, feel free to open issues and pull requests on our GitHub repository.

## License

This project is licensed under the [MIT License](LICENSE). Feel free to use, modify, and distribute the code according to the terms of the license.

---

Thank you for using the Kafka Node.js Client library. If you have any questions or need further assistance, please don't hesitate to contact us or refer to the documentation for more details. Happy Kafka-ing!