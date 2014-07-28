# see-threepio

see-threepio is a powerful, platform-agnostic solution to language localisation that leverages the ubiquity of JSON.

## Terminology
* term - base expression, as simple as a string

## Term
All 'terms' are essentially functions with 0 - N named parameters.


## Example format

    {
        "anErrorOccurred": "An error occurred",
        "itemsInCart(count)": "You have {count} ~pluralise(item|{count}) in your cart",
        "pluralise(word|number)": "{word}|~if(~=({number}|1)|s))"
    }

## Node JS
One of the most powerful features of see-threepio is the is the ability to leverage
exiting package tools and create an inheritance model in any method you choose.

This works extremely well if you're running your own private npm repository.

###seethreepio-myapp-en (npm module)
####en.json
    {
        "colorSelect": "Select a ~color from ~color wheel"
    }

####index.js
    var merge = require('merge');

    module.exports = merge(
        true,
        require('seethreepio-myapp-en-au'),
        require('./en-au')
    );

###seethreepio-myapp-en-au (npm module)
####en-au.json
    {
        "color": "colour"
    }

####index.js
    var merge = require('merge');

    module.exports = merge(
        true,
        require('seethreepio-myapp-en-au'),
        require('./en-au')
    );

###Using it..
You can now use it in your module (server side).

    var lang = require('seethreepio-myapp-en-au'),
        SeeThreepio = require('see-threepio-js'),
        seeThreepio = new SeeThreepio(lang);

    console.log(seeThreepio.get('colorSelect'));
    // outputs:
    // Select a colour from the colour wheel
