- Start Date: (2022-04-03)
- Members: Diego Sánchez
- RFC PR:

# Summary

Define the HTTP operations and endpoints for the REST API of the notifications services in the API Gateway.

---

# Basic example

Users are obtained through their autentication information

**Requests need the user's token to return its corresponding notifications. For the example, imagine that the token belongs to the user 'oneMoreUser'.**

- `[GET] /notifications/` - Get all notifications

```json
{
  "user": "oneMoreUser",
  "data": [
    {
      "id": "123abcd",
      "textContent": "Invita a un amigo y consigue $50.000 COP",
      "date": "2022-04-02T15:00:00.000Z",
      "read": false,
      "action": {}
    },
    {
      "id": "124abce",
      "textContent": "Reservaste una habitación en Cartagena",
      "date": "2022-04-01T20:15:00.000Z",
      "read": true,
      "action": {}
    },
    {
      "id": "125abcf",
      "textContent": "¡Rápido que te lo quitan! Termina de reservar tu habitación en Cartagena",
      "date": "2022-04-01T17:50:00.000Z",
      "read": false,
      "action": {}
    }
    ...
  ]
}
```

---

# Motivation

We need to expose some specific behaviors of notifications to process information on the frontend and satisfy the requirements of each user, such as seeing all their notifications or marking them as read. REST is useful for what we need, and that is why we have considered using it to expose the logic of the notification system.

---

# Detailed design

## Get all notifications

- **Endpoint:** `[GET] /notifications/`
- **Requires authentication:** YES
- **Description:** Get all notifications from an authenticated user.

### Success response

- **Code:** 200 OK
- **Content example:**

  #### Request body

    ```json
    {
      "token": "theuserauthtoken"
    }
    ```
  #### Response body

    ```json
    {
      "data": [
        {
          "id": "123abcd",
          "textContent": "Invita a un amigo y consigue $50.000 COP",
          "date": "2022-04-02T15:00:00.000Z",
          "read": false,
          "action": {}
        },
        {
          "id": "124abce",
          "textContent": "Reservaste una habitación en Cartagena",
          "date": "2022-04-01T20:15:00.000Z",
          "read": true,
          "action": {}
        },
        {
          "id": "125abcf",
          "textContent": "¡Rápido que te lo quitan! Termina de reservar tu habitación en Cartagena",
          "date": "2022-04-01T17:50:00.000Z",
          "read": false,
          "action": {}
        }
        // All the remaining notifications...
        ...
      ]
    }
    ```

## Get the lasts notifications, with pagination

- **Endpoint:** `[GET] /notifications&page=:num`
- **Requires authentication:** YES
- **Description:** A page refers to a limited number of notifications, for example, page 1 gets the latest notifications, up to number 10, that is, each page will be made up of 10 notifications, and consulting a higher page number will retrieve older notifications. if no page number is received, the response will be the page 1.

### Success response

- **Code:** 200 OK
- **Content example:**

  #### Request body

    ```json
    {
      "token:": "theusertauthtoken"
    }
    ```

  #### Response body

    ```json
    {
      "data": [
        {
          "id": "123abcd",
          "textContent": "Invita a un amigo y consigue $50.000 COP",
          "date": "2022-04-02T15:00:00.000Z",
          "read": false,
          "action": {}
        },
        {
          "id": "124abce",
          "textContent": "Reservaste una habitación en Cartagena",
          "date": "2022-04-01T20:15:00.000Z",
          "read": true,
          "action": {}
        },
        {
          "id": "125abcf",
          "textContent": "¡Rápido que te lo quitan! Termina de reservar tu habitación en Cartagena",
          "date": "2022-04-01T17:50:00.000Z",
          "read": false,
          "action": {}
        }
        // Until completing the amount of notifications that we consider a page, it could be 10 or 20
      ]
      ...
    }
    ```

## Get only one notification by its ID

- **Endpoint:** `[GET] /notifications/:notification`
- **Requires authentication:** YES
- **Description:** Get the information about only one notification by its ID.

### Success response

- **Code:** 200 OK

- **Content example:** If we pass "124abce" as notification id:

  #### Request body

    ```json
    {
      "token:": "theusertauthtoken"
    }
    ```

  #### Response body

    ```json
    {
      "data":
        {
          "id": "124abce",
          "textContent": "Reservaste una habitación en Cartagena",
          "date": "2022-04-02T15:00:00.000Z",
          "read": true,
          "action": {}
        }
    }
    ```

## Mark a notification as read

- **Endpoint:** `[PATCH] /notifications/mark-read`
- **Requires authentication:** YES
- **Description:** Set the "read" property of a notification to true.

### Success response

- **Code:** 200 OK
- **Content example:** If we pass "123abcd" as notification id:

  #### Request body

    ```json
    {
      "token:": "theusertauthtoken",
      "id": "123abcd"
    }
    ```

  #### Response body

    ```json
    {
      "data":
        {
          "id": "123abcd",
          ...
          "read": true,
          ...
        }
    }
    ```

## Set all notifications as read

- **Endpoint:** `[PATCH] /notifications/all-read`
- **Requires authentication:** YES
- **Description:** Set the "read" property of all notifications to true.

### Success response

- **Code:** 200 OK
- **Content example:**

  #### Request body

    ```json
    {
      "token:": "theusertauthtoken"
    }
    ```

  #### Response body

    ```json
    {
      "data": [
        {
          "id": "123abcd",
          ...
          "read": true,
          ...
        },
        {
          "id": "124abce",
          ...
          "read": true,
          ...
        }
        {
          "id": "125abcf",
          ...
          "read": true,
          ...
        }
        ...
      ]
    }
    ```

---

# Drawbacks

Why should we not do this? Please consider:

- If we change the name/estructure of any endpoint, the other teams could need to make changes to their code.
- The presented structure extracts the users from their authentication, however, another way would be to include the user in the url.

---

# Alternatives

- **GraphQL:** This allow expose methods without endpoint and front-end can consume the data that they require.
