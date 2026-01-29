# Using external UI pages to set parameters

## The need for external parameter UIs

There are cases where the information to be entered by the user into one or more parameter fields of a parametric model may be so complex that OpenSCAD's standard parameter elements, even if documented with a [static webpage as described here](README.md), will not be enough. Instead, it might be necessary to provide an advanced user interface on an external web page, making it possible for a user to reasonably provide their input for a parametric model to get the desired result.

## Codizmo's external parameter UI interface

- Codizmo uses the OpenSCAD parameter comment syntax with a simple extension allowing to specify external URLs. Remote UI pages opened this way can then send parameter values back to update the UI element for that specific parameter. These pages may be [created and hosted on GitHub as explained here](HOWTO.md), for example.
- External URLs in OpenSCAD comments like `// [Set the value here](https://codizmo.github.io/codizmo/getpval)` are detected by Codizmo's link parsing system and show the remote page in a new window. This may just be a static web page providing extended explanations about a parameter, or an interactive web UI allowing the user to define parameter values with any UI needed to do this in the best possible way.
- If the external URL in an OpenSCAD comment ends with a `#` like `// [Set the value here](https://codizmo.github.io/codizmo/getpval#)`, the remote page will be shown in an iframe. If the remote system does not allow its pages to be shown in an iframe, Codizmo will fall back to a new browser window to show the remote UI page.
- After showing the remote page in an iframe or a new browser window, Codizmo waits for a postMessage event from the external URL and validates the origin URL of the message to improve the level of security. It only accepts messages from the same origin as the original remote URL.
- After a postMessage from the remote page is received, Codizmo updates the corresponding parameter value and closes the window or iframe.
- Codizmo automatically tracks from which parameter the remote page has been called and writes the value entered into that specific parameter field. This makes it possible to use the same remote page for multiple parameters in parallel.
- In addition to the automated parameter/remote page matching, a remote page may optionally specify the parameterName in the message posted to route the value returned to that parameter.

## Passing back parameter values from remote pages

For your remote page, use the following postMessage format to send the value entered by the user back to Codizmo:

```javascript
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
