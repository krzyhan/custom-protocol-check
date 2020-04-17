# Custom Protocol Check in Browser

[![npm version](https://badge.fury.io/js/%40krzyhan%2Fcustom-protocol-check.svg)](https://badge.fury.io/js/%40krzyhan%2Fcustom-protocol-check) [![Pull requests](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://www.npmjs.com/package/@krzyhan/custom-protocol-check) [![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/krzyhan/custom-protocol-check/blob/master/LICENSE)

Detect whether a custom protocol is available in browser (Chrome, Firefox, Safari, iOS, IE8-IE11 and Edge)

The implementation is different from one browser to another, sometimes depend on which OS you are. Most of them are hacks, meaning that the solution is not the prettiest.

_**Important feature:** If current tab is not active when it's trying to detect focus then it would attempt to open protocol as soon as focus is back on current tab. It is more useful when there is a long running process and at the end of that process we need to detect whether that file can be opened using custom protocol. User might be doing his work on different tabs or applications so in such cases library would try to detect custom protocol as soon as current tab gets focus._

- Chrome and iOS: using window onBlur to detect whether the focus is stolen from the browser. When the focus is stolen, it assumes that the custom protocol launches external app and therefore it exists.
- Firefox (Version >= 64): using hidden iframe onBlur to detect whether the focus is stolen. When the focus is stolen, it assumes that the custom protocol launches external app and therefore it exists.
- Firefox (Version < 64): try to open the handler in a hidden iframe and catch exception if the custom protocol is not available.
- Safari: using hidden iframe onBlur to detect whether the focus is stolen. When the focus is stolen, it assumes that the custom protocol launches external app and therefore it exists.
- IEs and Edge in Win 8/Win 10: the cleanest solution. IEs and Edge in Windows 8 and Windows 10 does provide an API to check the existence of custom protocol handlers. Other older IE versions are not supported.

# Examples

```js
import customProtocolCheck from 'custom-protocol-check';

customProtocolCheck(
  'mycustomprotocol://params',
  () => {
    console.log('Custom protocol not found.');
  },
  () => {
    console.log('Custom protocol found and opened the file successfully.');
  }
);
```

# Known Issues

- In some protocol such as "mailto:", IE seems to trigger the fail callback while continuing on opening the protocol just fine (tested in IE11/Win 10). This issue doesn't occur with a custom protocol.

# Special Thanks

custom-protocol-check is forked from https://github.com/vireshshah/custom-protocol-check. Many thanks to Ismail Habib Muhammad and Viresh Shah

##### Happy Coding!
