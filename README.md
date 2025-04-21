# Banking API

## Overview
The Banking API is a RESTful API for RAYBANK that provides endpoints for 
managing banking operations. It serves as the specification for the 
[BankingUI](https://github.com/raywo-trainings/BankingUI) and [BankingService](https://github.com/raywo-trainings/BankingService) projects.

This API allows you to:
- Manage clients (create, read, update, delete)
- Manage different types of accounts (current accounts, savings accounts)
- Process financial transactions (deposits, withdrawals)
- Track account entries and balances

## API Specification

### Version
Current version: 2.0.0

### Base URL
Development server: `http://localhost:8080/api/v2`

## Endpoints

The API is organized around the following resources:

### Clients
- `GET /clients` - Retrieve all clients
- `POST /clients` - Create a new client
- `GET /clients/{id}` - Retrieve a specific client
- `PUT /clients/{id}` - Update a client
- `DELETE /clients/{id}` - Delete a client

### Accounts (General)
- `GET /accounts` - Retrieve all accounts (can be filtered by owner ID)
- `GET /accounts/{iban}` - Retrieve a specific account
- `DELETE /accounts/{iban}` - Delete an account (only if balance is zero)

### Current Accounts
- `GET /current-accounts` - Retrieve all current accounts
- `POST /current-accounts` - Create a new current account
- `GET /current-accounts/{iban}` - Retrieve a specific current account
- `PUT /current-accounts/{iban}` - Update a current account
- `DELETE /current-accounts/{iban}` - Delete a current account

### Savings Accounts
- `GET /savings-accounts` - Retrieve all savings accounts
- `POST /savings-accounts` - Create a new savings account
- `GET /savings-accounts/{iban}` - Retrieve a specific savings account
- `PUT /savings-accounts/{iban}` - Update a savings account
- `DELETE /savings-accounts/{iban}` - Delete a savings account

### Entries (Transactions)
- `GET /accounts/{iban}/entries` - Retrieve all entries for an account
- `POST /accounts/{iban}/deposits` - Create a deposit entry
- `POST /accounts/{iban}/withdrawals` - Create a withdrawal entry

## Data Models

### Client
```json
{
  "id": 4711,
  "firstname": "Max",
  "lastname": "Mustermann"
}
```

### Account
The API supports two types of accounts:

#### Current Account
```json
{
  "iban": "DE12123456789012345678",
  "balance": 205.78,
  "owner": {
    "id": 4711,
    "firstname": "Max",
    "lastname": "Mustermann"
  },
  "accountType": "current",
  "overDraftLimit": 1000.00,
  "overdraftInterestRate": 12.5
}
```

#### Savings Account
```json
{
  "iban": "DE12123456789012345678",
  "balance": 205.78,
  "owner": {
    "id": 4711,
    "firstname": "Max",
    "lastname": "Mustermann"
  },
  "accountType": "savings",
  "interestRate": 1.25
}
```

### Entry (Transaction)
```json
{
  "id": "123e4567-e89b-12d3-a456-426614174000",
  "iban": "DE12123456789012345678",
  "amount": 345.12,
  "entryDate": "2025-04-01T10:00+02:00",
  "description": "Einzahlung",
  "entryType": "deposit"
}
```

## Error Handling

The API uses standard HTTP status codes to indicate the success or failure of requests:

- `200 OK` - The request was successful
- `201 Created` - A new resource was successfully created
- `204 No Content` - The request was successful but there is no content to return
- `400 Bad Request` - The request was syntactically invalid
- `404 Not Found` - The requested resource was not found
- `422 Unprocessable Entity` - The request was semantically invalid

Error responses follow the RFC-9457 Problem Details format:

```json
{
  "instance": "/client/4711",
  "type": "about:blank",
  "title": "The given entity could not be validated.",
  "details": "The firstname field needs to be at least 1 character long.",
  "status": 422,
  "violations": [
    {
      "field": "firstname",
      "constraint": "NotNull",
      "message": "must not be empty"
    }
  ]
}
```

## Related Projects

This API specification serves as the foundation for:

1. [BankingUI](https://github.com/raywo-trainings/BankingUI) - A user interface for interacting with the Banking API
2. [BankingService](https://github.com/raywo-trainings/BankingService) - A service implementation of the Banking API

## Development

### Prerequisites
- OpenAPI 3.1.0 compatible tools for viewing and editing the specification

### Usage
1. Clone this repository
2. Open the `openapi.yml` file in your preferred OpenAPI editor or viewer
3. Use the specification to generate client code, server stubs, or documentation

## License

This project is licensed under the GNU General Public License - see the [LICENSE](LICENSE) file for details.
