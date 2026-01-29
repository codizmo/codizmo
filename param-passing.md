# Handling external URL parameters

Here's how the external URL parameter handling works:

- Codizmo uses the OpenSCAD parameter comment syntax with an small extension allowing to specify external URLs. Remote pages opend this way, can then send parameter values back to update the UI element for that specific parameter.

- External URLs in OpenSCAD comments like `// [Set the value here](https://codizmo.github.io/codizmo/getpval)
` are detected by Codizmo's link parsing system and show the remote page in a new window. This may just be a static web page providing extended explanations about a parameter or an interavtive web UI allowing the user define parameter values with any UI needed to do this in the best possible way. 

- If the external URLs in an OpenSCAD comment is ended with a `#` like `// [Set the value here](https://codizmo.github.io/codizmo/getpval#)` the remote page will be shown in an iFrame. If the remote system does not allow to have its pages shown in an iFrame, Codizmo will fall back to a new browser window to show the remote UI page.

- After showing the remote page in an iFrame or a new brwoser window, Codizmo waits for a postMessage event from the external URL and validates the origin URL of the message to improve the level of security. It only accepts messages from the same origin as the original remoteURL.

- After a postMessage from the remote page is received, Codizmo updates the corresponding parameter value
   and closes the window or iFrame.

- Codizmo automatically tracks from which parameter the remote page has been called and writes the value entered into that specific parameter field. This makes it possible to use the same remote page for multiple parameters in parallel.

- In addtition to the automated parameter / remote page matching, a remote page may optionally specify the parameterName in the message posted to route the value returned to that parameter.


## On the remote page
  For your remote page, use the following postMessage format to send the value entered by the user back to Codizmo

```Javascript
  // Updated postMessage format for the remote page
  const message = {
      type: 'selection',
      value: selectedValue,           // The actual value to set
      text: selectedText,             // Human-readable description (optional)
      parameterName: 'Level',         // Optional: specify parameter name 
      timestamp: new Date().toISOString(),
      source: 'github-pages-selector'
  };

  // Send to parent window - the origin will be automatically validated
  window.parent.postMessage(message, '*');
```
