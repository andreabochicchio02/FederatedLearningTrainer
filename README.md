# Federated Learning Trainer
This project implements a **Horizontal Federated Learning (HFL)** platform for distributed training of TensorFlow models without centralizing data. The system is designed to be privacy-preserving, fault-tolerant, and scalable, and allows real-time monitoring and control of the training process.

A representative use case is a network of hospitals collaboratively training a machine learning model on sensitive medical data. Each hospital trains locally and only shares model updates, ensuring data privacy while achieving performance comparable to centralized training.

The system was evaluated using a federated setup on the MNIST dataset. The federated model achieved accuracy comparable to centralized training, confirming the effectiveness of the approach.

## Technologies Used
- **Erlang** – Distributed coordination and fault tolerance _(Project Requirement)_
- **Python** – TensorFlow training and model aggregation
- **TensorFlow / Keras** – Neural network implementation
- **Java (Spring Boot)** – Backend and system orchestration
- **WebSockets (SockJS)** – Real-time communication
- **Maven & Rebar3** – Build automation

## Documentation Links
[PROJECT DOCUMENTATION](https://github.com/andreabochicchio02/FederatedLearning/blob/main/Federated_Learning_DOC.pdf)

## System Architecture
<img width="640" height="480" alt="image" src="https://github.com/user-attachments/assets/bc794d00-9215-4061-854b-7c997a3ff6db" />


## Stand Alone Use (without Java server)
### Hide Warnings (Linux)
```export TF_CPP_MIN_LOG_LEVEL=3```

### Starting Erlang Shells
To start the master node:
```rebar3 shell --sname master@localhost```

To start slave nodes:

```rebar3 shell --sname slave1@localhost``` 

```rebar3 shell --sname slave2@localhost```

### Basic Commands
To start the environment, passing models and weights and loading the db in each node the command is:
```master_supervisor:start_link_shell(self()).``` 

To train the model for 1 epoch, the command is:
```master_api:train().```

While, if you want to train the model for `N` epoch, the command is:
```master_api:train(N).```

If you want to train the model for at most `N` epoch, until a `T` accuracy threshold is reached the command is:
```master_api:train(N, T).```


### Emulating disconnection and sleep
To emulate a node disconnection, from the master terminal you can execute:

```erlang:disconnect_node('slave1@localhost').```

This will disconnect the slave1@localhost node and the connection lost handling will be executed from the node and the master.

The sleep in the python node: 
```time.sleep(70000)```



