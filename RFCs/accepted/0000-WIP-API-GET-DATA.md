- Start Date: 2022-03-02
- Members: Yael Ramírez @yaelrmz, Saúl Regalado @Saulrega 
- RFC PR: (leave this empty)

# Summary

We need implement and API REST endpoint in order to get data from the different domains to the _Data Monitoring_ team. So the idea is to build a web server using Fastify

# Basic example

In events like: _new usser created_, _new place created_, _new booking created_, etc. We need get the infomation associate to this events.

#### Example with _Places_ domain

![](https://i.imgur.com/VLQ8NXu.png)


Basically, this is the acction that we need for each domain

# Motivation

The team _Data Monitoring_ need information from the other domains in order to measure our metrics. We propse an interface to the other teams can use to bring the necessary data

# Detailed design

We will build a web server using Fastify. 

## Usage

### Installation
Get fastify with NPM:

`npm install fastify`

### Code
Create server.js and add the following content:
```js
// Require the framework and instantiate it
const fastify = require('fastify')({ logger: true })

// Declare a route
fastify.get('/', async (request, reply) => {
  return { hello: 'world' }
})

// Run the server!
const start = async () => {
  try {
    await fastify.listen(3000)
  } catch (err) {
    fastify.log.error(err)
    process.exit(1)
  }
}
start()
```

### Launch
Launch the server with:

`node server`

### Test
We can test it with:

`curl http://localhost:3000`

# Detailed design for _Places_

### Trigger: _New place added_

- URL: `/places/new_place`
- Method: `POST`
- Auth required: NO
- Use: send data about the new place

#### Data constraints

```json
{
    "host_id":   {int},
    "place_id":  {int},
    "timestamp": {int}(seconds)(fecha_creacion),
    "price":     {double},
    "latitude":  {double},
    "longitude": {double},
    "name":      {string},
    "is_active": {bool}
}
```

#### Data example

```json
{
    "host_id":   23567,
    "place_id":  345,
    "timestamp": 1646237243,
    "price":     64.8,
    "latitude":  15.945484,
    "longitude": -97.695531,
    "name":      "Oaxaca house",
    "is_active": true
}
```

### Trigger: _New review added_

- URL: `/places/new_review`
- Method: `POST`
- Auth required: NO
- Use: send data about the new review

#### Data constraints

```json
{
    "host_id":   {int},
    "place_id":  {int},
    "user_id":   {int},
    "timestamp": {int}(seconds)(fecha_creacion),
    "review":    {string},
    "rating":    {int}, //*
}
```

#### Data example

```json
{
    "host_id":   2343,
    "place_id":  342,
    "user_id":   23454,
    "timestamp": 1646237243,
    "review":    "Good place....",
    "rating":    4,
}
```

### Trigger: _Deactivation/Activation of place_

- URL: `/places/status_place`
- Method: `POST`
- Auth required: NO
- Use: send data about Activation/Deactivation of a place

#### Data constraints

```json
{
    "place_id":  {int},
    "is_active": {bool},
    "timestamp": {int}(seconds)(fecha_creacion), //**
}
```

#### Data example

```json
{
    "place_id":  476,
    "is_active": false,
    "timestamp": 1646237243,
}
```

# Detailed design for _Users_

### Trigger: _New user registred_

- URL: `/users/new_user`
- Method: `POST`
- Auth required: NO
- Use: send data about the new user

#### Data constraints

```json
{
    "user_id":    {string},
    "email":      {string},
    "timestamp":  {int}(segundos)(fecha_creacion),
    "is_verifed": {bool},
    "gener":      {string},
    "state":      {string},
    "zip":        {string},
    "country":    {string},
    "is_active":  {bool},
    "is_host":    {bool} // trigger
}
```

#### Data example

```json
{
   "user_id":     657687,
    "email":      "user@example.com",
    "timestamp":  1646237243,
    "gener":      "Male",
    "state":      "Guerrero",
    "zip":        "39810",
    "country":    "Acapulco",
    "city":       "Costera",
    "is_active":  true
}
```

### Trigger: _User verified_

- URL: `/users/verified_user`
- Method: `POST`
- Auth required: NO
- Use: send data about verification of an user

#### Data constraints

```json
{
    "user_id":    {string},
    "timestamp":  {int}(segundos)(fecha_creacion),
    "is_verifed": {bool},
}
```

#### Data example

```json
{
    "user_id":    128,
    "timestamp":  1646237243,
    "is_verifed": true
}
```

### Trigger: _User Actived/Deactived_

- URL: `/users/status_user`
- Method: `POST`
- Auth required: NO
- Use: send data about Activation/Deactivation of an user

#### Data constraints

```json
{
    "user_id":    {string},
    "timestamp":  {int}(segundos)(fecha_creacion),
    "is_active":  {bool},
}
```

#### Data example

```json
{
    "user_id":    1977,
    "timestamp":  1646237243,
    "is_active":  false,
}
```

### Trigger: _User Accountless_ *

- URL: `/users/accountless_user`
- Method: `POST`
- Auth required: NO
- Use: send data about accountless user

#### Data constraints

```json
{
    "uid":             {string},
    "start_timestamp": {int},
    "end_timestamp":   {int}
}
```

#### Data example

```json
{
    "uid":             876567687,
    "start_timestamp": 1646237243,
    "end_timestamp":   1646237643
}
```

# Detailed design for Booking

### Trigger: _New booking registred_

- URL: `/booking/new_booking`
- Method: `POST`
- Auth required: NO
- Use: send data about the new booking

#### Data constraints

```json
{
    "booking_id":         {int},
    "host_id":            {int},
    "place_id":           {int},
    "user_id":            {int},
    "timestamp":          {int}(segundos)(fecha_creacion),
    "cost":               {double},
    "number_guests":      {int},
    "check_out_date":     {int},
    "check_in_date":      {int},
    "commission_charged": {double},
    "is_canceled":        {bool}
}
```

#### Data example

```json
{
    "booking_id":         8656,
    "host_id":            6546,
    "place_id":           6754,
    "user_id":            8665,
    "timestamp":          1646237243,
    "cost":               56.9,
    "number_guests":      2,
    "check_out_date":     1646287243,
    "check_in_date":      1646482454,
    "commission_charged": 14.9,
    "is_canceled":        false
}
```

# Drawbacks

- We need a server to implement this API
- _Users_, _Places_ and _Bookings_ teams need add this API call and this would add CPU usage 
- We don’t know how many experience in Javascript our team members has. So we need to have in mind maybe the possibility of more carry overs.

# Alternatives

We have other API libraries like:
- [Express](https://expressjs.com/es/): another web framework based on JS
- [FastAPI](https://fastapi.tiangolo.com/): web framework for building APIs with Python 3.6+

# Adoption strategy

- We can divide each _domain_ to work in sub-teams 
- Our team needs to coordinate with the _Users_, _Places_ and _Booking_ team because they have the data

# How we teach this

- We have the necessity of learn Javascript
- We have the necessity of learn about API REST

# Unresolved questions
- In this RFC we don't talk about **how this data will be saved** to _Data Monitoring_ team
- Who has the responsability of _Accountless Users_?
- _Place_ and _Booking_ has data of _Review_, whic one we should be use?

