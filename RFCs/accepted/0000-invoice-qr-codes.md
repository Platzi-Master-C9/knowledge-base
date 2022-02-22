- Start Date: 2022-02-19
- Members: 
1. Paulina Ignacio @Lina2Bot
2. Edwin Páez      @Zawng
- RFC PR: 

# Summary

Generate QR code to visualize the digital ticket from booking.

# Basic example

# Motivation

Sharing information about the client's booking for they or their guests. 
In case, the client or the person who booked decide to go with others. 
Therefore, when the person who scan the QR code would obtain the booking information (date, hour, location, phone, e-mail, etc.)

# Detailed design

[WIP]
Cuál, cómo, y por qué implementamos

# Drawbacks

[WIP]
¿Qué podría salir mal?

# Alternatives

Share booking information by email.

We can do this more easily with libraries like
1. [qrcode](https://www.npmjs.com/package/qrcode)
2. [qrcode-with-logos](https://www.npmjs.com/package/qrcode-with-logos)
3. [easyqrcodejs](https://www.npmjs.com/package/easyqrcodejs)
4. [react-qr-code](https://www.npmjs.com/package/react-qr-code)

# Adoption strategy
[WIP]

<!-- If we implement this proposal, how will existing C9 developers adopt it? Is
this a breaking change? Can we write a codemod? Should we coordinate with
other projects or libraries? -->

# How we teach this
 
"The quick response, or QR, Code is a two-dimensional version of the Barcode able to convey a wide variety of information almost instantly with the scan of a mobile device. 

Able to store up to 7089 digits or 4296 characters, including punctuation marks and special characters, the Code can equally encode words and phrases such as internet addresses. One thing to always keep in mind, especially when it comes to designing the Static QR Codes aesthetic is that the more data is added, the more the size increases and its structure becomes more complex. 

Even when damaged, the QR Code’s structure data keys include duplications. It is thanks to these redundancies that allow up to 30% of the Code structure to take damage without affecting its readability on scanners, ."

"The anatomy of a QR Code: Positioning detection markers, Alignment markings, Timing pattern, Version information, Format information, Data and error correction keys and Quiet zone."

# Unresolved questions
[WIP]

1. ¿Qué información se debería mostrar en la factura?
2. ¿En qué formato se daría esta factura?
