# Real-time Kafka Azure Stocks Streaming Project with ML Prediction

This project demonstrates real-time stock data streaming and prediction using Apache Kafka, Azure services, and machine learning, containerized for easy deployment and scalability.

## Table of Contents
- [Overview](#overview)
- [Architecture](#architecture)
  - [Architecture Diagram](#architecture-diagram)
- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Usage](#usage)
- [Container Management](#container-management)
- [Machine Learning Model](#machine-learning-model)
- [Contributing](#contributing)
- [License](#license)

## Overview

This project utilizes Apache Kafka for real-time stock data streaming, integrated with various Azure services to process, store, and analyze the data. It incorporates machine learning for real-time stock price prediction. The project is containerized using Docker and orchestrated with Azure Kubernetes Service (AKS) for easy deployment and management.

## Architecture

The system architecture includes the following components:

1. **Real-time Stock Data Feed**: Continuous stream of real-time stock market data
2. **Apache Kafka**: Message broker for real-time data ingestion (containerized)
3. **Azure Event Hubs**: Fully managed, real-time data ingestion service
4. **Azure Stream Analytics**: Real-time data processing and analysis
5. **Azure Cosmos DB**: NoSQL database for storing processed data and predictions
6. **Azure Functions**: Serverless compute for additional data processing and ML model invocation (containerized)
7. **Azure Machine Learning**: Platform for training, deploying, and managing ML models
8. **ML Model Container**: Containerized machine learning model for real-time stock price prediction
9. **Azure Power BI**: Real-time data visualization and reporting
10. **Azure Kubernetes Service (AKS)**: Container orchestration for managing Kafka and other containerized components

### Architecture Diagram

Below is a high-level architecture diagram of the Real-time Kafka Azure Stocks Streaming Project with ML Prediction:

![Real-time Kafka Azure Stocks Streaming Architecture with ML Prediction](architecture-diagram.svg)

This diagram illustrates the flow of real-time data from the stock data source through various containerized components, Azure services, and the machine learning prediction pipeline.

## Prerequisites

- Azure subscription
- Docker
- Azure CLI
- kubectl
- Helm
- Python 3.8+
- TensorFlow  (for ML model development)

## Setup

1. Clone the repository:
   ```
   git clone https://github.com/yourusername/realtime-kafka-azure-stocks-ml.git
   cd realtime-kafka-azure-stocks-ml
   ```

2. Build Docker images:
   ```
   docker build -t kafka-producer:latest -f Dockerfile.producer .
   docker build -t kafka-consumer:latest -f Dockerfile.consumer .
   docker build -t azure-function:latest -f Dockerfile.function .
   docker build -t ml-model:latest -f Dockerfile.ml-model .
   ```

3. Set up Azure resources:
   - Create an Azure Kubernetes Service (AKS) cluster
   - Create an Azure Event Hubs namespace
   - Create an Azure Cosmos DB account
   - Set up Azure Stream Analytics job
   - Create an Azure Machine Learning workspace

4. Deploy Kafka to AKS:
   ```
   helm repo add bitnami https://charts.bitnami.com/bitnami
   helm install my-kafka bitnami/kafka
   ```

5. Apply Kubernetes configurations:
   ```
   kubectl apply -f k8s/producer-deployment.yaml
   kubectl apply -f k8s/consumer-deployment.yaml
   kubectl apply -f k8s/function-deployment.yaml
   kubectl apply -f k8s/ml-model-deployment.yaml
   ```

6. Train and deploy the ML model:
   - Use Azure Machine Learning to train your stock prediction model
   - Deploy the trained model to the ML Model Container in AKS

7. Update configuration files with your Azure credentials, Kafka connection details, and ML model endpoint.

## Usage

1. Start the Kafka producer to ingest real-time stock data:
   ```
   kubectl apply -f k8s/producer-job.yaml
   ```

2. Monitor Kafka consumer logs:
   ```
   kubectl logs -f deployment/kafka-consumer
   ```

3. Check Azure Function logs for data processing and ML model invocation:
   ```
   kubectl logs -f deployment/azure-function
   ```

4. Monitor ML model predictions:
   ```
   kubectl logs -f deployment/ml-model
   ```

5. Observe real-time data flow in Azure Stream Analytics.

6. Visualize real-time results and predictions in Azure Power BI.

## Container Management

- View all pods:
  ```
  kubectl get pods
  ```

- Scale the consumer or ML model deployment:
  ```
  kubectl scale deployment kafka-consumer --replicas=3
  kubectl scale deployment ml-model --replicas=2
  ```

- Update container images:
  ```
  kubectl set image deployment/kafka-producer kafka-producer=kafka-producer:v2
  kubectl set image deployment/ml-model ml-model=ml-model:v2
  ```

- View logs for a specific container:
  ```
  kubectl logs <pod-name> -c <container-name>
  ```

## Machine Learning Model

The ML model in this project is designed to predict stock prices in real-time based on incoming market data. Here are some key points about the model:

- Developed using TensorFlow 
- Trained on historical stock data and relevant features
- Containerized for easy deployment and scaling in AKS
- Invoked by Azure Functions for real-time predictions
- Continuously updated using Azure Machine Learning pipelines

For details on model architecture, training process, and performance metrics, please refer to the `ml-model/README.md` file.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
