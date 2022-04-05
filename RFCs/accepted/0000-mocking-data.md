Title: [WIP] Mocking data

- Start Date: 2022-02-23
- Members: Saúl Regalado and Adrián Fernández
- RFC PR: (leave this empty)


# Summary

Use the faker.js library to mock data, since it has several properties that generate data similar to what is expected in everyday use of the system.


# Basic example

- faker.name.firstName() ---->  Cameron

- faker.phone.phoneNumber() —-->  +1 291-299-0192

- console.log(
    faker.fake('{{name.lastName}}, {{name.firstName}} {{name.suffix}}')
  );


# Motivation

In order to guarantee the correct develope of all data processing, the need arises to test the implementations, with data as close as reality we can generate:

- Check if it is the expected data type.
- The correct process is applied to each of the data.
- Measure the performance of the application, if the process is applied effectively.


# Detailed design

To generate a lot of data, very similar to common use, that allows us to test the behavior of these mocks within the development, both the validation and the process of valid data. The properties that may interest us would be:

- faker.name: to generate user base information 
  - findName: generates a first and last name
  - gender: useful for gender analysis/segregation


- faker.finance: for everything related to costs and payments
  - amount: simulate hosting costs


- faker.address: everything related to sites and location
  - country
  - state
  - latitude and longitude

- faker.datatype: useful if you want to test data type validation
  - number
  - float
  - json

- faker.date: fake reservations
  - between: generate dates between chosen periods

- faker.internet:
  - email: essential for creating an account within the platform
  - avatar: check everything related to profile pictures

- faker.image: check support for messages and comments containing images



# Drawbacks

Its implementation is limited solely to testing the development's ability to process the required information, however, with this proposal we cannot measure software performance


# Alternatives

Implement an in-house method that is capable of measuring the performance of the system, thus providing the necessary metrics to know if it meets the expected parameters or the parts where there is a possibility of improvement.



# Adoption strategy

It is a library written in TypeScript, the project is designed to be developed in the same language, so the process of adopting the solution will be simple


# How we teach this

With the documentation plus some concrete examples should be enough to show the operation of the library and its use.



# Unresolved questions

How to measure application performance, this library does not give solutions for that need, so it is not a comprehensive solution. Something else must be sought to integrate that requirement

