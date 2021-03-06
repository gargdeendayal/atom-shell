# crash-reporter

An example of automatically submitting crash reporters to remote server:

```javascript
crashReporter = require('crash-reporter');
crashReporter.start({
  productName: 'YourName',
  companyName: 'YourCompany',
  submitUrl: 'https://your-domain.com/url-to-submit',
  autoSubmit: true
});
```

## crashReporter.start(options)

* `options` Object
  * `productName` String, default: Atom-Shell
  * `companyName` String, default: GitHub, Inc
  * `submitUrl` String, default: http://54.249.141.255:1127/post
    * URL that crash reports would be sent to as POST
  * `autoSubmit` Boolean, default: true
    * Send the crash report without user interaction
  * `ignoreSystemCrashHandler` Boolean, default: false
  * `extra` Object
    * An object you can define which content will be send along with the report.
    * Only string properties are send correctly.
    * Nested objects are not supported.

# crash-reporter payload

The crash reporter will send the following data to the `submitUrl` as `POST`:

* `rept` String - eg. atom-shell-crash-service
* `ver` String - The version of atom-shell
* `platform` String - eg. win32
* `process_type` String - eg. browser
* `ptime` Number
* `_version` String - The version in `package.json`
* `_productName` String - The product name in the crashReporter `options` object
* `prod` String - Name of the underlying product. In this case Atom-Shell
* `_companyName` String - The company name in the crashReporter `options` object
* `upload_file_minidump` File - The crashreport as file
* All level one properties of the `extra` object in the crashReporter `options` object
