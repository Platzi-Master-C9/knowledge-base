- Start Date: (2022-02-23)
- Members: Diego Sánchez, Efrén Ruíz
- RFC PR:

# Summary

Use the nodemailer module for the purpose of sending email notifications.

---

# Basic example

*Send an email notification when the host has written a new message to the guest.*
![New host message, email notification](https://i.ibb.co/q5LZgNv/email-notification-new-message.png "New host message email notification")

*Send an email notification to an user who has not completed the necessary data to make reservations*
![Upload user data, email notification](https://i.ibb.co/BjqyPQP/email-notification-update-user-data.png "Upload user data, email notification")

## Usage

Trought a POST request the service receives a JSON with the necessary data to send the email:

```json
{
    // Required
    "to": ["bar@example.com", "baz@example.com"],
    "subject": "Hello ✔",
    "text": "Hello world?",
    // Opionals
    "html": "<b>Hello world?</b>",
    "cc": ["ccreceiver@example.com" "ccreceivertwo@example.com"],
    "bcc": ["bccreceiver@example.com" "bccreceivertwo@example.com"],
    "attachments": [
        {   // use URL as an attachment
            "filename": "license.txt",
            "path": "https://raw.github.com/nodemailer/nodemailer/master/LICENSE"
        },
        {   // encoded string as an attachment
            "filename": "text1.txt",
            "content": "aGVsbG8gd29ybGQh",
            "encoding": "base64"
        }]
    ...
}
```

If everything was correct, the API will respond with a "200 OK" code and the received JSON data.

There are yet more options in the email sending that we can use, but for now these are the basics, and we would also need to learn how to use the other options.

You can find a more detailed description about the meaning of each parameter in our dependencie [Nodemailer documentation](https://nodemailer.com/message/#common-fields).

## Complementary tools

- If you need to send an email with HTML but don't want to worry about the code, you can use an HTML email template generator like [mosaico.io](https://mosaico.io/editor-0.17.5-nr.html#templates/versafix-1/template-versafix-1.html), in this way the generation of an email with HTML code becomes much easier.

    Note that mosaico.io leaves a stamp that cannot be removed from the web editor, but can be removed from the generated HTML code.

---

# Motivation

## Why we are doing this?

Some teams of our Booking System need to communicate information to clients through emails, our intention is to optimize this task by simply making a request to our REST API with the information that they want to communicate to one or more clients. These notifications could vary from booking updates, newsletter or even discounts of some places of interest for the user. It could be used in everything the user finds interesting.

Thus, we can also send emails from a specialized email address from which it will not be necessary to distribute credentials, since doing so could be unsafe.

## What use cases does it support?

- Confirmation of bookings done by the customers.
- Informing the owner of a property if a customer has booked his/her property and the date that the user selected.
- Alerting the customer about info related to his/her account.
- Any information the customer could need using email communication

## What is the expected outcome?

Offer a functional component/module and independent of other services that can be a part of the booking system.

---

# Detailed design

An email notification may be required at any time, so we need the service to be constantly available, a solution to this may be to create a REST API with the endpoint "/notifications/send-email" that listens for POST requests (only from the booking system teams), receiving in the body of the request a JSON with the necessary data to send the email.

The data will be processed by the service and then it will sent the email to the list of users especified in the JSON. We're not sure about if we need to use the message broker of our notification system, if so, we are not clear how this will be integrated. For now we think this could be an approximation of the process flow:

![Process flow of the email notification service](https://i.ibb.co/YhCsnWy/image.png "Process flow of the email notification")

Email notifications will be stored in the notification system database, which according to what has been mentioned in some project workshops, will probably be MongoDB.

---

# Drawbacks

## Why should we *not* do this?

- What about sending emails since an email provider? Maybe initially we could send emails from an email provider like gmail or outlook, after all our module doesn't do anything that can't be done from a mail manager.

- We have no experience using nodemailer, so what if it turns out to be insufficient and we haven't realized it. For now it's the best free option we've found, but...

- If the booking system needs to send a lot of emails daily, we should opt for a dedicated SMTP server.

---

# Alternatives

- **Mailgun:** It's a set of powerful APIs that allow us to send, receive, track and store email effortlessly.

- **Amazon SES:** Eliminates the complexity and expense of building an in-house email solution or licensing, installing and operating a third-party email service. The service integrates with other AWS services, making it easy to send emails from applications being hosted on services such as Amazon EC2.

- **EmailJS:** It allows sending emails directly from JavaScript without the need of a backend development. The developers creato one or more email templates and then trigger an email using the JavaScript SDK, specifying the template and the parameters for rendering the email.

---

# Adoption strategy

- To use this service, teams don't need to change anything, however they need to learn how to communicate with the REST API

- This is not a breaking change, as said, teams don't have to change their code. What's more, this service will work as a help for the other teams and it won't need other systems than the notification system itself.

- We can write codemods to automatize certain emails, for example, newsletters or publicity emails.

---

# How we teach this

## Terminology

- **SMTP:** Simple Mail Transfer Protocol, it's the standar protocol used to send emails.

- **Nodemailer:** A node.js module that allows us to send emails easily using SMTP.

## Considerations and resources

- This is a new component for the Booking System, that allows us to send emails to the users (clients and owners of properties).

- We will include a README file with the explanation and documentation of the service, with some examples, because we need to make sure that the squads of the booking system that could use this module know how to, for example, build a JSON object with the structured data of the email to be sent.

- In any case, if someone has a question about the use of the service, those in charge will be available through the Slack channels. Currently, we are Diego Sánchez and Efrén Ruíz, from the C9, but have in mind that in the future we may not be responsible for this service.

- It does not change how C9 is taught to new developers at any level, because it's a module designed to send emails easily, it has documentation and explains each part that compose the module, to understand how it works

- You will be able to learn how to use this service with examples of use in our documentation. Take as template the JSON code that you find in the usage section of this document.

# Unsolved questions

- How about using a paid service on its free tier?
- Should the service be built focusing only on sending emails?
