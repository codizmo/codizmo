# Parameter Help for the Online OpenSCAD Renderer 

[More information](HOWTO)

## Simple explanation
To show a simple explanation underneath a parameter field add a comment above it

```
// Set the number of copies here
copies = 3;
```

## Extended explanations on external pages
If a parameter needs more than a simple explanation create a web page documenting it and write the link to it im Markdown notation
```
// Find more information [here](https://oscad.github.io/ "More information about multiple divisions")
multiple_divisions = "10, 30, 70";
```
These pages are opened in a separate window / tab by default. But if you add a hashtag at the end of the URL it will be opened in an iFrame on the same page. Note however, that may services do not allow to show content stored on them to be shown in an iframe. So make sure that there are no blank spaces at the end of the URL in these cases.
