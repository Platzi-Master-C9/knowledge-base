- Start Date: (2022-02-25)
- Members: (Cristhian Jimenez)
- RFC PR: 

# Summary

Data visualization is the presentation of data in a graphical format. This presentation format is important for decisions' makers because enable them to see analytics presented visually in order to make better decisions. 

A picture is worth 1000 words.

Deciding which tool is the best is a challenge because there are a lot of different options which select. All of them with a lot of features and benefits, and with integration options with a lot programming languages.

# Motivation

We need to choose an option that meets the following expectations:

- Preferably open source
- Large adoption in IT industry
- Wide community that support its use
- Integration with many programming languages

Those expectations allow us: low or zero cost, availability to customize code if needed, use a proven and high-performing library because it is used by many companies around the world, supported by a large community that allows to solve implementation problems quicly and flatten the knowledge curve, and finally the posibility of using a language which we could be confortable.

# Detailed design
### Why D3.js?
D3.js it is an open-source JavaScript library for manipulating documents based on data. D3 helps you bring data to life using HTML, SVG and CSS. D3’s emphasis on web standards gives you the full capabilities of modern browsers without tying yourself to a proprietary framework, combining powerful visualization components and a data-driven approach to DOM manipulation.
D3 has 100.4K GitHub stars and 23K GitHub forks. These are some companies that use D3: Accenture, Coinbase, Coursera, Graphy, Square, Zalando, Odoo, Strava among others. 
D3 can be integrated into JavaScript, React, Angular, React Native, and a bunch of others.
### How much it cost?
Zero cost.
### Where is D3.js used?
D3.js is a javascript library added to the front-end in the web application.
Back-end (the server) will generate the necessary data.
The part of the application the users interact with (the front-end) will use D3.js.

# Implementation example
This is a implementation example on internet: https://www.w3schools.com/ai/ai_d3js.asp

# Drawbacks
The Speed: it stands to reason that a framework as complex and customizable as D3.js will have some sort of performance bottleneck somewhere down the line. When dealing with really large datasets, D3.js can reduce down to a snail’s pace and can act like a bit of a speed bump while waiting for it to do its thing.
Base Documentation: the community is great and all, but the base documentation of D3.js leaves much to be desired.
It Takes Time: The double-edged sword to having full customization and being able to make something from scratch is that it just takes time.

# Alternatives
Chart.js
Plotly
CanvasJS
Paths.js
Google Charts

# Unresolved questions
Is D3 the best data visualization tool to choose? 
Maybe should we pay for a licenced library in order to get a better support?