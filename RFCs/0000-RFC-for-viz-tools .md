- Start Date: 2022-02-21
- Members: Yael Ramírez @YaelRmz, Juan Alberto Solís @JuanSolisCTJ13
- RFC PR: (leave this empty)

# Summary

Provide a mechanism for the metrics vizualitation of the _host_ role

# Definitions
_host_: Person who offers his property in the booking system.

# Basic example
## Integration of D3 dashboards in the Website

A section will be added where the host will be able to see a panel with metrics such as:

- Number of active reservations.
- Reservation history
- History of cancelled reservations
- Revenue per property 
- Reviews and rating per property

It would look like this

![](https://i.imgur.com/9uGFFqF.png)


# Motivation

As part of data monitoring, we need to give practical information about the stadistic of his booking for the _host_

# Detailed design

## Usage

### Installation

We have a variety of ways to download and use D3. We will show two forms, this is the link to the [documentation](https://riptutorial.com/d3-js/example/2955/installation):

#### NPM
- Initialize NPM in your project if you have not done so already: 
`
npm init
`
- NPM install D3: 
`
npm install --save d3
`
- Reference d3.js (for development) or d3.min.js (for production) in your HTML: 
    - `<script type="text/javascript" src="node_modules/d3/build/d3.js"></script>`

#### Directly
- To link directly to the latest release, copy this snippet:
    - `<script src="https://d3js.org/d3.v7.min.js"></script>`


### Examples

We have a lot of possibilities to visualizations. In this [link](https://observablehq.com/@d3/gallery) you can see examples like this:
![](https://cdn.substack.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F4ff45cab-8501-487d-9a2c-42035bdbbb41_942x480.gif)

![](https://www.abeamer.com/files/by-date/2018/10/d3-datamap/story-frames/story.gif)

# Drawbacks

- The knowledge base for this squad apparently is more suited to use Python tecnologies and could be a time to master:
    - The library itself.
    - React.
    - JS.


# Alternatives

- streamlit.io: Python library.

# Adoption strategy

The frontend teams will have to work with this d3 and react components in their views for the respective user. For a correct adoption of this feature we will have to give them not only the general purpose graph but the customized viz for the view, including the respective group of tests. 
The backend team will have to give us recommendations for embedding the viz without affecting the app performance.

# How we teach this

We will create an MD file to explain how to use this feature

# Unresolved questions

Almost everything in this feature is TBD.
