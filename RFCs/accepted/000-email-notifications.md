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

An method of our notifications system receives an object with the necessary data to send the email:

```js
{
    // Required
    to: ["bar@example.com", "baz@example.com"],
    subject: "Hello ✔",
    text: "Hello world?",
    // Opionals
    html: "<b>Hello world?</b>",
    cc: ["ccreceiver@example.com" "ccreceivertwo@example.com"],
    bcc: ["bccreceiver@example.com" "bccreceivertwo@example.com"],
    attachments: [
        {   // use URL as an attachment
            filename: "license.txt",
            path: "https://raw.github.com/nodemailer/nodemailer/master/LICENSE"
        },
        {   // encoded string as an attachment
            filename: "text1.txt",
            content: "aGVsbG8gd29ybGQh",
            encoding: "base64"
        }]
    ...
}
```

If everything was correct, the returned response will be a boolean with the "true" value, else "false".

There are yet more options in the email sending that we can use, but for now these are the basics, and we would also need to learn how to use the other options.

You can find a more detailed description about the meaning of each parameter in our dependencie [Nodemailer documentation](https://nodemailer.com/message/#common-fields).

## Complementary tools

- If you need to send an email with HTML but don't want to worry about the code, you can use an HTML email template generator like [mosaico.io](https://mosaico.io/editor-0.17.5-nr.html#templates/versafix-1/template-versafix-1.html), in this way the generation of an email with HTML code becomes much easier.

    Note that mosaico.io leaves a stamp that cannot be removed from the web editor, but can be removed from the generated HTML code.

---

# Motivation

## Why we are doing this?

Some teams of our Booking System need to communicate information to clients through emails, our intention is to optimize this task by simply making calling a method and giving as parameter the information that they want to communicate to one or more clients. These notifications could vary from booking updates, newsletter or even discounts of some places of interest for the user. It could be used in everything the user finds interesting.

Thus, we can also send emails from a specialized email address from which it will not be necessary to distribute credentials, since doing so could be unsafe.

## What use cases does it support?

- Confirmation of bookings done by the customers.
- Informing the owner of a property if a customer has booked his/her property and the date that the user selected.
- Alerting the customer about info related to his/her account.
- Any information the customer could need using email communication

## What is the expected outcome?

Offer a functional component/module and independent of other services that can be a part of the booking system.

We think that we can use a range of components that are useful to send emails, we should not stay only with one tool, because it limit us in different ways. But also, we need to see the best tools that solve our needs for our system, so if the implementation of the project needs a different tool, we should be able to add it.

---

# Detailed design

An email notification may be required at any time, so we need the service to be constantly available, we will give a method that receives the JS object with the necessary data to send the email.

The data will be processed by the module and then it will sent the email to the list of users especified in the JSON/JSobject. For now we think this could be an approximation of the process flow:

![Process flow of the email notification service](https://i.ibb.co/YjSWhYH/image.png "Process flow of the email notification")

Email notifications, or its metadata, will be stored in the notification system database, which according to what has been mentioned in some project workshops, will probably be MongoDB.

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

We could opt for a pay service using the free tier option, but it depends on the amount of emails that we need to send. If the amount is relatively small, we can use one of these services on the free tier option.

---

# Adoption strategy

In order to use the component successfully, we need to implement templates, these templates can vary, depending on the purpose of the notification. For example, a template for a booking confirmation, a newsletter email, a promotion email, etc. It depends on the use cases. We need to assign these as tasks for the email notification team for the simple reason that we need to define exactly how these templates should be used.

To use styles on the emails, we could use [Styliner](http://styliner.slaks.net/), that is a node.js component that allows us to use CSS in the emails. We think that the email, besides being informative, it needs to be attractive to the user, because plain text emails are very vague and a lot of users could ignore them for this particular reason.

The template itself will have functionality, because it will be used with diverse data, and it can be used for different purposes; every squad is allowed to use this component.

We think that is not necessary to save any data of the email notifications, because it can be overflooded with meaningless information, that we don't really need for anything. The data, for example, of the booking confirmation, will be stored in another database, using the data generated by the booking function. We don't need to store any email information in the database, because we actually have the data.

- To use this service, teams don't need to change anything, however they need to learn how to create a correct object for giving it to our send email method.

- This is not a breaking change, as said, teams don't have to change their code. What's more, this service will work as a help for the other teams and it won't need other systems than the notification system itself.

- We can write codemods to automatize certain emails, for example, newsletters or publicity emails.

---

# How we teach this

## Terminology

- **SMTP:** Simple Mail Transfer Protocol, it's the standar protocol used to send emails.

- **Nodemailer:** A node.js module that allows us to send emails easily using SMTP.

## Considerations and resources

- This is a new component for the Booking System, that allows us to send emails to the users (clients and owners of lodgings).

- There will be a README file with the explanation and documentation of the service, with some examples, because we need to make sure that the squads of the booking system that could use this module know how to, for example, build a JSON object with the structured data of the email to be sent.

- In any case, if someone has a question about the use of the service, those in charge will be available through the Slack channels. Currently, we are Diego Sánchez and Efrén Ruíz, from the C9, but have in mind that in the future we may not be responsible for this service.

- It does not change how C9 is taught to new developers at any level, because it's a module designed to send emails easily, it has documentation and explains each part that compose the module, to understand how it works

- You will be able to learn how to use this service with examples of use in our documentation. Take as template the JSON code that you find in the usage section of this document.

# Unsolved questions

- Should the service be built focusing only on sending emails?
