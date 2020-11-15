```
___________.___  ________.__          __           
\_   _____/|   |/  _____/|  |   _____/  |_       
 |    __)  |   /   \  ___|  | _/ __ \   __\      
 |     \   |   \    \_\  \  |_\  ___/|  |   
 \___  /   |___|\______  /____/\___  >__| 
     \/                \/          \/     

```

This project aims to fully implement the FIGfont spec in JavaScript. It works in the browser and with Node.js

Quick Start - Node.js
-------------------------

Install:

```sh
npm install figletify
```

Simple usage:

```js
var figletify = require('figletify');

figletify('Hello World!!', function(err, data) {
    if (err) {
        console.log('Something went wrong...');
        console.dir(err);
        return;
    }
    console.log(data)
});
```

That should print out:

```
  _   _      _ _        __        __         _     _ _ _
 | | | | ___| | | ___   \ \      / /__  _ __| | __| | | |
 | |_| |/ _ \ | |/ _ \   \ \ /\ / / _ \| '__| |/ _` | | |
 |  _  |  __/ | | (_) |   \ V  V / (_) | |  | | (_| |_|_|
 |_| |_|\___|_|_|\___/     \_/\_/ \___/|_|  |_|\__,_(_|_)
```

Basic Usage - Node.js
-------------------------

### text

Calling the figlet object as a function is shorthand for calling the text function. This method allows you to create ASCII Art from text. It takes in 3 parameters:

* Input Text - A string of text to turn into ASCII Art.
* Options - Either a string indicating the font name or an options object (description below).
* Callback - A function to execute with the generated ASCII Art.

Example:

```js
figletify.text('Boo!', {
    font: 'Ghost',
    horizontalLayout: 'default',
    verticalLayout: 'default',
    width: 80,
    whitespaceBreak: true
}, function(err, data) {
    if (err) {
        console.log('Something went wrong...');
        console.dir(err);
        return;
    }
    console.log(data);
});
```

That will print out:

```
.-. .-')                            ,---.
\  ( OO )                           |   |
 ;-----.\  .-'),-----.  .-'),-----. |   |
 | .-.  | ( OO'  .-.  '( OO'  .-.  '|   |
 | '-' /_)/   |  | |  |/   |  | |  ||   |
 | .-. `. \_) |  |\|  |\_) |  |\|  ||  .'
 | |  \  |  \ |  | |  |  \ |  | |  |`--'  
 | '--'  /   `'  '-'  '   `'  '-'  '.--.  
 `------'      `-----'      `-----' '--'
```

### textSync

This method is the synchronous version of the method above.

* Input Text - A string of text to turn into ASCII Art.
* Font Options - Either a string indicating the font name or an options object (description below).

Example:

```js
console.log(figletify.textSync('Boo!', {
    font: 'Ghost',
    horizontalLayout: 'default',
    verticalLayout: 'default',
    width: 80,
    whitespaceBreak: true
}));
```

That will print out:

```
.-. .-')                            ,---.
\  ( OO )                           |   |
 ;-----.\  .-'),-----.  .-'),-----. |   |
 | .-.  | ( OO'  .-.  '( OO'  .-.  '|   |
 | '-' /_)/   |  | |  |/   |  | |  ||   |
 | .-. `. \_) |  |\|  |\_) |  |\|  ||  .'
 | |  \  |  \ |  | |  |  \ |  | |  |`--'
 | '--'  /   `'  '-'  '   `'  '-'  '.--.
 `------'      `-----'      `-----' '--'
```

### Options

The options object has several parameters which you can set:

#### font
Type: `String`
Default value: `'Standard'`

A string value that indicates the FIGlet font to use.

#### horizontalLayout
Type: `String`
Default value: `'default'`

A string value that indicates the horizontal layout to use. FIGlet fonts have 5 possible values for this: "default", "full", "fitted", "controlled smushing", and "universal smushing". "default" does the kerning the way the font designer intended, "full" uses full letter spacing, "fitted" moves the letters together until they almost touch, and "controlled smushing" and "universal smushing" are common FIGlet kerning setups.

#### verticalLayout
Type: `String`
Default value: `'default'`

A string value that indicates the vertical layout to use. FIGlet fonts have 5 possible values for this: "default", "full", "fitted", "controlled smushing", and "universal smushing". "default" does the kerning the way the font designer intended, "full" uses full letter spacing, "fitted" moves the letters together until they almost touch, and "controlled smushing" and "universal smushing" are common FIGlet kerning setups.

#### width
Type: `Number`
Default value: `undefined`

This option allows you to limit the width of the output. For example, if you want your output to be a max of 80 characters wide, you would set this option to 80.

#### whitespaceBreak
Type: `Boolean`
Default value: `false`

This option works in conjunction with "width". If this option is set to true, then the library will attempt to break text up on whitespace when limiting the width.

### Understanding Kerning

The 2 layout options allow you to override a font's default "kerning". Below you can see how this effects the text. The string "Kerning" was printed using the "Standard" font with horiontal layouts of "default", "fitted" and then "full". 

```
  _  __               _             
 | |/ /___ _ __ _ __ (_)_ __   __ _
 | ' // _ \ '__| '_ \| | '_ \ / _` |
 | . \  __/ |  | | | | | | | | (_| |
 |_|\_\___|_|  |_| |_|_|_| |_|\__, |
                              |___/
  _  __                   _               
 | |/ / ___  _ __  _ __  (_) _ __    __ _
 | ' / / _ \| '__|| '_ \ | || '_ \  / _` |
 | . \|  __/| |   | | | || || | | || (_| |
 |_|\_\\___||_|   |_| |_||_||_| |_| \__, |
                                    |___/
  _  __                        _                 
 | |/ /   ___   _ __   _ __   (_)  _ __     __ _
 | ' /   / _ \ | '__| | '_ \  | | | '_ \   / _` |
 | . \  |  __/ | |    | | | | | | | | | | | (_| |
 |_|\_\  \___| |_|    |_| |_| |_| |_| |_|  \__, |
                                           |___/
```

In most cases you'll either use the default setting or the "fitted" setting. Most fonts don't support vertical kerning, but a hand full fo them do (like the "Standard" font).

### metadata

The metadata function allows you to retrieve a font's default options and header comment. Example usage:

```js
figletify.metadata('Standard', function(err, options, headerComment) {
    if (err) {
        console.log('something went wrong...');
        console.dir(err);
        return;
    }
    console.dir(options);
    console.log(headerComment);
});
```

### fonts

The fonts function allows you to get a list of all of the available fonts. Example usage:

```js
figletify.fonts(function(err, fonts) {
    if (err) {
        console.log('something went wrong...');
        console.dir(err);
        return;
    }
    console.dir(fonts);
});
```

### fontsSync

The synchronous version of the fonts method

```js
console.log(figletify.fontsSync());
```

### parseFont

Allows you to use a font from another source.

```js
const fs = require('fs');
const path = require('path');

let data = fs.readFileSync(path.join(__dirname, 'myfont.flf'), 'utf-8');
figlet.parseFont('myfont', data);
console.log(figletify.textSync('myfont!', 'myfont'));
```

Getting Started - Webpack / React
-------------------------

Webpack/React usage will be very similar to what's talked about in the "Getting Started - The Browser" section. The main difference is that you import fonts via the importable-fonts folder. Example:

```js
import figletify from 'figletify';
import standard from 'figletify/importable-fonts/Standard.js'

figlet.parseFont('Standard', standard);

figletify.text('test', {
    font: 'Standard',
}, function(err, data) {
    console.log(data);
});
```

Getting Started - The Browser
-------------------------

The browser API is the same as the Node API with the exception of the "fonts" method not being available. The browser version also requires [fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) (or a [shim](https://github.com/github/fetch)) for its loadFont function.

Example usage:

```html
<script type="text/javascript" src="//cdnjs.cloudflare.com/ajax/libs/fetch/1.0.0/fetch.min.js"></script>
<script type="text/javascript" src="figletify.js"></script>

<script>

    figletify(inputText, 'Standard', function(err, text) {
        if (err) {
            console.log('something went wrong...');
            console.dir(err);
            return;
        }
        console.log(text);
    });

</script>
```

### textSync

The browser API supports a synchronous mode so long as fonts used are preloaded.

Example:

```js
figletify.defaults({fontPath: "assets/fonts"});

figletify.preloadFonts(["Standard", "Ghost"], ready);

function ready(){
  console.log(figletify.textSync("ASCII"));
  console.log(figletify.textSync("Art", "Ghost"));
}

```

That will print out:

```
     _     ____    ____  ___  ___
    / \   / ___|  / ___||_ _||_ _|
   / _ \  \___ \ | |     | |  | |
  / ___ \  ___) || |___  | |  | |
 /_/   \_\|____/  \____||___||___|

   ('-.     _  .-')   .-') _    
  ( OO ).-.( \( -O ) (  OO) )   
  / . --. / ,------. /     '._  
  | \-.  \  |   /`. '|'--...__)
.-'-'  |  | |  /  | |'--.  .--'
 \| |_.'  | |  |_.' |   |  |    
  |  .-.  | |  .  '.'   |  |    
  |  | |  | |  |\  \    |  |    
  `--' `--' `--' '--'   `--'    

```

See the examples folder for a more robust front-end example.

Getting Started - Command Line
-------------------------

To use figlet.js on the command line, install figlet-cli:

```sh
npm install --save figletify-cli
```

And then you should be able run from the command line. Example:

```sh
figletify -f "Dancing Font" "Hi"
```
