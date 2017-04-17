# Atomic Design

Some summarised notes and thoughts from [Brad Frost's Atomic Design](http://atomicdesign.bradfrost.com/).

## Style Guides

Cornerstones of good design systems are style guides. They organise design materials whilst documenting their design, usage and intentions. Several kinds of style guides have emerged serving different purposes.

- Brand identity style guides define the assets and materials that make a company unique. They provide logos, typography, colour palettes and message guidelines that allow a company to be cohesive about itself across a variety of media channels.
- Writing style guides provide author guidelines for contributing text. The rise of the web has made it much easier for people to contribute written content. These guides can be extremely granular going as far as defining the particulars around punctuation and grammar.
- Pattern libraries, also known as front-end style guides or user interface libraries, provide components and guidelines for constructing user interfaces. They promote consistency and cohesion not just for your own organisation but for third parties who may be trying to integrate with you. They provide a shared vocabulary for the components that comprise your design and inform developers and designers of the tools that they have at their disposal for constructing user interfaces.

A great resource for digging into other companies style guides is [styleguides.io](http://styleguides.io/).

## Atoms

Atoms serve as the foundational building blocks that comprise our user interfaces. They could include basic HTML elements like form labels, inputs, buttons and other components that aren't able to be broken down any further. Each interface atom has its own properties such as dimensions, colour and font. Exisiting in isolation they don't really do much.

[The Periodic Table of HTML Elements](https://madebymike.com.au/html5-periodic-table/) originally created by [Josh Duck](http://joshduck.com/) provides a great example of the HTML elements that we can use to build user interfaces.

## Molecules

Molecules are relatively simple groups of user interface elements which function together as a unit. Taking the form label, input and button atoms, they can be joined together to form a search molecule. Combining the atoms together gives them purpose. When thinking about molecules, it helps to adhere to the single responsibility principle. Create molecules that do one thing and one thing well.

## Organisms

Organisms are complex user interface components which are composed of groups of molecules, and/or atoms and/or other organisms. Taking the search form molecule, it could be combined with a logo and navigation bar as part of a header organism.

## Templates

Moving away from the chemistry analogy, templates bring together atoms, molecules and organisms to articulate the designs underlying content structure. A homepage template may include the header organism and all the other necessary components to construct the page. A template provides context for the relatively abstract organisms, molecules and atoms. The template defines the content structure but does not define the content itself.

## Pages

Pages provide specific instances of templates and show what a user interface looks like with real, representative content in place.
