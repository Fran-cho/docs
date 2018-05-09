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

Authentication is achieved through a pre-shared key that's specific to each client we onboard. Ada will generate and send you your authentication key. Don't share it with anybody else!

Each of the endpoints described below requre an `Authorization` HTTP header that's set to the key that Ada provides for your client.

### Endpoints

#### `POST` : `/train/`

| Field | Type | Required |
|-------|------|----------|
|`client_id` | String | Yes |

This endpoint simply kicks off a training event for a client. This will pick up all the new questions that have been added to the Client and build them into the machine learning model.

---

#### `GET` : `/prediction/`

| Field | Type |Required |
|-------|------|----------|
|`client_id` | String | Yes |
|`question_to_predict` | String | Yes |
|`num_predictions`| Number | No|

This endpoint takes a `question_to_predict` and a `num_predictions` and returns a list of (one or more) Labels.

---

#### `POST` : `/question/`

| Field | Type |Required |
|-------|------|----------|
|`client_id` | String | Yes |
|`question`|String|Yes|
|`label`|String|Yes|
|`active`|Boolean|Yes|

This endpoint allows you to create new Questions for a Client. The `question` field is a string representation of the question. The `label` field is an identifier to an object in your application's domain that should be "predicted" from this question. The `active` field simply turns on/off the question in the model.

---

#### `PATCH` : `/question/`

| Field | Type |Required |
|-------|------|----------|
|`client_id` | String | Yes |
|`question`|String|Yes|
|`label`|String|Yes|
|`active`|Boolean|Yes|

This endpoint allows you to edit Questions for a Client.

---

#### `DELETE` : `/question/`

| Field | Type |Required |
|-------|------|----------|
|`client_id` | String | Yes |
|`question`|String|Yes|

This endpoint allows you to delete a Question.

---

#### `POST` : `/questions/`
| Field | Type |Required |
|-------|------|----------|
|`client_id` | String | Yes |
|`questions` | Array | Yes |
|`label` | String | Yes |

This endpoint lets you train several questions at once to a Client.

---

#### `DELETE` : `/questions/`
| Field | Type |Required |
|-------|------|----------|
|`client_id` | String | Yes |
|`questions` | Array | Yes |
|`label` | String | Yes |

This endpoint lets you train several questions at once to a Client.

---

#### `DELETE` : `/labels/`
| Field | Type |Required |
|-------|------|----------|
|`client_id` | String | Yes |
|`label`|String|Yes|

This endpoint allows you to delete all questions associated with a Label. Use this endpoint when you're application is deleting the object associated with this AM label.

---
