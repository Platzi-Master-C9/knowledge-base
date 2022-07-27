- Start Date: (2022-02-23)
- Members: (Diego Sánchez, Efrén Ruíz)
- RFC PR: (leave this empty)

# Summary

Use of the nodemail module with the purpose of sending email notifications

# Basic example

```js
const nodemailer = require("nodemailer");

async function main() {
  let testAccount = await nodemailer.createTestAccount();

  let transporter = nodemailer.createTransport({
    host: "smtp.ethereal.email",
    port: 587,
    secure: false,
    auth: {
      user: testAccount.user,
      pass: testAccount.pass,
    },
  });

  let info = await transporter.sendMail({
    from: '"Fred Foo 👻" <foo@example.com>',
    to: "bar@example.com, baz@example.com",
    subject: "Hello ✔",
    text: "Hello world?",
    html: "<b>Hello world?</b>",
  });

  console.log("Message sent: %s", info.messageId);
  console.log("Preview URL: %s", nodemailer.getTestMessageUrl(info));
}
```

_Send an email notification when the host has written a new message to the guest._

![New host message, email notification](https://i.ibb.co/q5LZgNv/email-notification-new-message.png "New host message email notification")
​
_Send an email notification to an user who has not completed the necessary data to make reservations_

![Upload user data, email notification](https://i.ibb.co/BjqyPQP/email-notification-update-user-data.png "Upload user data, email notification")

# Motivation

Why we are doing this?

To facilitate the communication of different subjects of interest to the user using email notifications. These notifications could vary from booking updates, newsletter or even discounts of some places of interest for the user. It could be used in everything the user finds interesting.

What use cases does it support?

- Confirmation of bookings done by the customers.
- Informing the owner of a property if a customer has booked his/her property and the date that the user selected.
- Alerting the customer about info related to his/her account.
- Any information the customer could need using email communication

What is the expected outcome?

Offer a functional component / module and independent of other services that can be a part of the booking system.

We think that we can use a range of components that are useful to send emails, we should not stay only with one tool, because it limit us in different ways. But also, we need to see the best tools that solve our needs for our system, so if the implementation of the project needs a different tool, we should be able to add it.

# Detailed design

![C4 Model](https://camo.githubusercontent.com/d582f5dd2064804e56ac2bbd99dbc34f4611d01956424b0b51d094ede57a17e0/68747470733a2f2f692e6962622e636f2f596843736e57792f696d6167652e706e67)

# Drawbacks

Why should we _not_ do this?

- If the booking system needs to send a lot of emails daily, we should opt for a dedicated SMTP server.

# Alternatives

- **Mailgun:** It's a set of powerful APIs that allow us to send, receive, track and store email effortlessly.

- **Amazon SES:** Eliminates the complexity and expense of building an in-house email solution or licensing, installing and operating a third-party email service. The service integrates with other AWS services, making it easy to send emails from applications being hosted on services such as Amazon EC2.

- **EmailJS:** It allows sending emails directly from JavaScript without the need of a backend development. The developers creato one or more email templates and then trigger an email using the JavaScript SDK, specifying the template and the parameters for rendering the email.

We could opt for a pay service using the free tier option, but it depends on the amount of emails that we need to send. If the amount is relatively small, we can use one of these services on the free tier option.

# Adoption strategy

In order to use the component successfully, we need to implement templates, these templates can vary, depending on the purpose of the notification. For example, a template for a booking confirmation, a newsletter email, a promotion email, etc. It depends on the use cases. We need to assign these as tasks for the email notification team for the simple reason that we need to define exactly how these templates should be used.

To use styles on the emails, we could use [Styliner](http://styliner.slaks.net/), that is a node.js component that allows us to use CSS in the emails. We think that the email, besides being informative, it needs to be attractive to the user, because plain text emails are very vague and a lot of users could ignore them for this particular reason.

The template itself will have functionality, because it will be used with diverse data, and it can be used for different purposes; every squad is allowed to use this component.

We think that is not necessary to save any data of the email notifications, because it can be overflooded with meaningless information, that we don't really need for anything. The data, for example, of the booking confirmation, will be stored in another database, using the data generated by the booking function. We don't need to store any email information in the database, because we actually have the data.

**If we implement this proposal, how will existing C9 developers adopt it?**

Because it's a independent module, everyone can use it if they need to send an email notification to an user in a certain moment.

**Is this a breaking change?**

No, because it doesn't interfere with any module of the booking system.

**Can we write a codemod?**

Yes, we can write codemods to automatize certain emails, for example, newsletters or publicity emails.

**Should we coordinate with other projects or libraries?**

Not necessary, because the only module we need in order to send the emails would be nodemailer.

# How we teach this

**What names and terminology work best for these concepts and why?**

- SMTP: Simple Mail Transfer Protocol, it's the standar protocol used to send emails.

- nodemailer: A node.js module that allows us to send emails easily using SMTP.

**How is this idea best presented? As a continuation of existing C9 projects patterns?**

As a new component for the booking system, that allow us to send emails to the users (clients and owners of properties).

**Would the acceptance of this proposal mean the C9 documentation must be re-organized or altered?**

In certain extent, because we need to make sure that the squads of the booking system that could use this module know how to, for example, build a JSON string to transform it to a JS object with the structured data of the email to be sent.

**Does it change how C9 is taught to new developers at any level?**

No, because it's a module designed to send emails easily, it has a lot of documentation and explains each part that compose the module, to understand how it works

**How should this feature be taught to existing C9 developers?**

Basically with examples of use and the documentation, as mentioned before, we could implement a template of a JSON object that every squad can use to send specific emails.
