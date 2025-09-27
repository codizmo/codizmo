# Handling external URL parameters

Here's how the external URL parameter handling works:

## Integration Summary

### For the UI side

  1. Parameter URLs: External URLs in OpenSCAD comments like // [Set the value 
  here](https://mataebi.github.io/openscad/param1#) are detected by the existing link parsing system
  2. IframeOverlay: Enhanced to listen for postMessage events from external URLs and validate
  origins for security
  3. Parameter Updates: When a postMessage is received, it updates the corresponding parameter value
   and closes the overlay
  4. Parameter Tracking: The system tracks which parameter each external URL belongs to

### For the remote page
  For your remote page, use the following postMessage format

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

## Key features
  - Security: Only accepts messages from the same origin as the iframe URL
  - Automatic parameter detection: The UI knows which parameter the external URL belongs to based on
   the comment context
  - Flexible parameter naming: The remote page can optionally specify parameterName in the message,
  otherwise it uses the detected parameter
  - Auto-close: The iframe overlay closes automatically after receiving a valid selection
  - Validation: Basic validation ensures messages come from expected sources

  The system will work with the existing OpenSCAD Editor comment syntax and the external URL will be able
  to send parameter values back to update the UI element for that specific parameter.
