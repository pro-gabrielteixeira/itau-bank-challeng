# Original challend (In portuguese): https://github.com/rafaellins-itau/desafio-itau-vaga-99-junior?tab=readme-ov-file

# Itaú Unibanco - Programming Challenge

This is a cool challenge involving both software development and software engineering. We want to test your ability to build a piece of software with several different parts working together!

## 1. Introduction

Your mission, should you choose to accept it, is to create a REST API that receives Transactions and returns Statistics based on those transactions. For this challenge, the API must be built using **Java or Kotlin with Spring Boot**.

A good starting point is the Spring Starter.

> 💡 Tip: There is no single "right" way to solve this challenge! We will evaluate things like code quality, readability, project organization, number and quality of tests, security concerns, and several other factors :)

---

## 2. Challenge Definition

In this challenge, you should create a REST API hosted on GitHub or GitLab. Please read all instructions carefully!

### 2.1 Technical Requirements

Your project:

- MUST be hosted on GitHub or GitLab  
- MUST NOT fork any other project  
- MUST have at least one commit per endpoint (minimum of 3 commits)  
  - We want to see the evolution of your project over time 😉  
- All commits MUST be made by the same user who created the project  
  - We understand that some people have personal and professional accounts or a separate one for studies — be mindful of this!  
- MUST follow the endpoints described below **exactly**  
  - For example, `/transaction` is **not** the same as `/transactions`  
- MUST accept and return objects **exactly** as described below  
  - For example, `timestamp` is **not** the same as `transactionDate` or `date-time`  
- MUST NOT use any database system (like H2, MySQL, PostgreSQL, ...) or cache (like Redis, Memcached, Infinispan, ...)  
- MUST store all data **in memory**  
- MUST accept and return **JSON** only  

> ⚠️ For security reasons, we cannot accept project files as attachments. Your project MUST be publicly available so we can access and review it. After receiving our feedback, feel free to make your project private :)

---

### 2.2 API Endpoints

Below are the required API endpoints and their expected behavior.

---

#### 2.2.1 Receive Transactions: `POST /transaction`

This endpoint receives Transactions. Each transaction consists of an amount and a timestamp:

```json
{
    "amount": 123.45,
    "timestamp": "2020-08-07T12:34:56.789-03:00"
}
```

| Field     | Description                             | Required? |
|-----------|-----------------------------------------|-----------|
| amount    | Decimal (floating point) value          | Yes       |
| timestamp| Date/Time in ISO 8601 format             | Yes       |

> 💡 Tip: Spring Boot supports ISO 8601 dates out of the box. Try using a field of type `OffsetDateTime`!

**Rules:**
- Both `amount` and `timestamp` must be provided
- The transaction **MUST NOT** be in the future
- The transaction **MUST** have occurred in the past
- The amount **MUST** be greater than or equal to zero

**Expected Responses:**
- `201 Created` with no body  
  - Transaction was accepted (valid and registered)
- `422 Unprocessable Entity` with no body  
  - Transaction was rejected (e.g., negative value)
- `400 Bad Request` with no body  
  - API could not understand the client request (e.g., invalid JSON)

---

#### 2.2.2 Delete Transactions: `DELETE /transaction`

This endpoint deletes all stored transaction data.

**Expected Response:**
- `200 OK` with no body  
  - All transaction data successfully deleted

---

#### 2.2.3 Get Statistics: `GET /statistics`

This endpoint returns the statistics of transactions that occurred in the **last 60 seconds**.

```json
{
    "count": 10,
    "sum": 1234.56,
    "avg": 123.456,
    "min": 12.34,
    "max": 123.56
}
```

| Field | Description | Required? |
|-------|-------------|-----------|
| count | Number of transactions in the last 60 seconds | Yes |
| sum   | Total sum of transaction values in the last 60 seconds | Yes |
| avg   | Average transaction value in the last 60 seconds | Yes |
| min   | Minimum transaction value in the last 60 seconds | Yes |
| max   | Maximum transaction value in the last 60 seconds | Yes |

> 💡 Tip: `DoubleSummaryStatistics` in Java 8+ may help or inspire your implementation.

**Expected Response:**
- `200 OK` with statistics data  
  - A JSON object containing the fields: `count`, `sum`, `avg`, `min`, and `max`  
  - If there are **no transactions** in the last 60 seconds, return all values as **zero**

---

## 4. Bonus Features

Here are some extra challenges if you want to go above and beyond! These are optional but desirable and may set your submission apart:

- **Automated Testing**: Unit and/or functional tests are crucial. Focus on test effectiveness (e.g., don’t test only the happy paths).
- **Containerization**: Can you containerize your application (e.g., Docker)? No need to publish it!
- **Logging**: Does your application inform what's happening during runtime? This is helpful for debugging.
- **Observability**: Does your API have a healthcheck endpoint?
- **Performance**: Can you estimate how long it takes to compute statistics?
- **Error Handling**: Can you customize default Spring Boot errors to return meaningful messages?
- **API Documentation**: Can you document your API (e.g., Swagger/OpenAPI)?
- **System Documentation**: Can someone unfamiliar with your project build and run it easily?
- **Configuration**: Can you make the 60-second window configurable (e.g., user wants 120 seconds)?

---

Good luck, and have fun coding! 🚀
