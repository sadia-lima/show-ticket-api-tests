# Show Ticket API Test Design

This repository contains a **Postman collection** for testing the Show Ticket Web Application API. The tests cover system behavior, validation, authentication, and business rules. The purpose of these tests is to verify correct API behavior and provide a foundation for automated API testing.

---

## Test Descriptions

| Test Name | Endpoint | Request | Expected Result |
|-----------|----------|--------|----------------|
| Get All Shows | GET `/api/shows` | No body | Status 200, list of shows returned |
| Get Show By ID | GET `/api/shows/1` | No body | Status 200, single show returned |
| Create Booking Valid | POST `/api/bookings` | Valid booking JSON | Status 201, booking created |
| Create Booking Missing Field | POST `/api/bookings` | Missing `customerName` | Status 400, validation error |
| Invalid Ticket Quantity | POST `/api/bookings` | `tickets = -5` | Status 400, validation error |
| Invalid Show ID | GET `/api/shows/9999` | No body | Status 404, show not found |
| Access Without Authentication | POST `/api/bookings` | No token | Status 401 or 403 |
| Booking Too Many Tickets | POST `/api/bookings` | `tickets = 500` | Status 400 or business rule rejection |

---

## Interesting Behavior

Some endpoints demonstrate unexpected behavior with invalid input. For example:  

- Sending a very large ticket quantity does not always trigger a validation error.  
- This suggests that **business rule validation may be incomplete** in the generated API.  

These observations highlight areas where the system could handle edge cases more robustly.

---

## Git Repository Structure

```text
project-repo/
│
├─ api_tests/
│   └─ show-ticket-postman-collection.json
│
└─ README.md
