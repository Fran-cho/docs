# Answering Machine

Answering Machine (AM) is Ada's NLP service, used for training and querying text classification machine learning models.

## Concepts

- Clients
- Questions
- Labels
- Predictions
- Training

### Clients

AM services many clients, so we need a way to keep track of "who's who" on the platform. Before you get started, you'll need a `client_id`, which Ada generates on your behalf.

Each client gets its own machine learning model, so it's important to make sure that you group all the "application specific" content and training under one client.

### Questions

Questions are AM's bread and butter. To take advantage of AM's machine learning, you'll `POST` new questions to the `/questions/` endpoint. AM then trains that question to the label provided in order to assemble a machine learning model. Predictions requested from this client will return labels that are determined to likely be associated with the questions that have been trained previously.

### Labels

Labels are the thing you want AM to return after a successful prediction. The "classes" of the classifier. You'll train Questions to Labels to assemble your machine learning model, then request Predictions to retrive a Label associated with the query string.

### Predictions

A prediction is an operation to return an appropriate Label for a query string. The prediction endpoint receives a query string, generates class probabilities, and returns any Labels that are above a certain confidence threshold.

### Training

You "train" your machine learning model by teaching it questions that it should associate with a Label.

## Usage

### Authentication

### Endpoints

#### `/train/`

| Field | Required |
|-------|----------|
|`client_id` | Yes |

This endpoint simply kicks off a training event for a client. This will pick up all the new questions that have been added to the Client and build them into the machine learning model.

#### `/prediction/`

| Field | Required |
|-------|----------|
|`client_id` | Yes |



#### `/question/`

| Field | Required |
|-------|----------|
|`client_id` | Yes |


#### `/questions/`

| Field | Required |
|-------|----------|
|`client_id` | Yes |


#### `/labels/`

| Field | Required |
|-------|----------|
|`client_id` | Yes |


#### `/parameters/`

| Field | Required |
|-------|----------|
|`client_id` | Yes |
