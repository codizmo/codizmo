# Parameter Help for the Codizmo Parametrizer 

[More information](HOWTO.md)

## Simple explanations
To show a simple explanation above a parameter field, add a comment above it. This will show the name of the parameter «Copies» followed by the explanation «Set the number of copies here»
```
// Set the number of copies here
copies = 3;
```

## Tooltips
Tooltips are elements that show helpful information on hover. To write a tooltip use the syntax of external links (see below) but instead of a URL use a string with a leading blank. This will show the parameter name «Precision» followed by the string «Manufacturing tolerance value» if the mouse hovers over the word «tolerance» the additional explanation «Measurement precision in millimeters» will be shown.
```
// Manufacturing [tolerance]( "Measurement precision in millimeters") value
precision = 0.1;
```
### Sepcial icons for tooltips
To show a circle with a question mark, an 'i' in a cricle around it or a light bulb as part of the comment and to show a tooltip use (?), (i) or (8) in the text part of a tooltip
```
// [(?)]( "This is a helpful tooltip")
Url_test_2 = "Another String";

// [(i)]( "Enable this for advanced users only") Complex processing mode
complex_mode = false;

// [(8)]( "This is a great idea")
great_idea = true;
```

## Extended explanations in iFrames or on external pages
If a parameter needs more than a simple explanation create a web page documenting it and write the link to it in Markdown notation
```
// Find more information [here](https://oscad.github.io/ "More information about multiple divisions")
multiple_divisions = "10, 30, 70";
```
These pages are opened in a separate window / tab by default. But if you add a hashtag at the end of the URL it will be opened in an iFrame on the same page.

Note however, that many services do not allow to show content stored on them in an iframe. So make sure that there are no blank spaces at the end of the URL in these cases.
