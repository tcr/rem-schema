# REM: REST easy.

*VERSION: 0.3.0*

This is the common repository for all REM implementations. It contains
several default manifests for various popular REST APIs.

   * *[rem-node](https://github.com/timcameronryan/rem-node)* - REM for Node.js
   * *[rem-browser](https://github.com/timcameronryan/rem-browser)* - REM for the browser

## Specification

This is wildly subject to change. :3

### Top-Level

   * **base** &mdash; The beginning part of the URL, that is unchanged for all API calls. For instance, Tumblr API calls start with `http://api.tumblr.com/v2`. This property can be a string, or an array of `[regexString, base]` to match against the URL. Dropbox uses the host `api.dropbox.com`, except for file content, which uses `api-content.dropbox.com`. The value of `base` for Dropbox is `[["^/(files(_put)?|thumbnails)/.*", "https://api-content.dropbox.com/1"], "https://api.dropbox.com/1"]`.
   * **suffix** &mdash; Suffix for the API call. e.g. `"suffix": ".json"`
   * **params** &mdash; A string map of default query parameters to use. Version 3 of the Google Docs API has a required `v=3` parameter, and so has a `params` value of `{"v": "3"}`.
   * **configParams** &mdash; A string map of default query parameters to use from the API configuration. Usually APIs are defined with a `key` and a `secret` parameter, but this 

   * **format** &mdash; A hash map of formats that the API can return, out of `xml` or `json`. Each format is a map of properties to combine with the top-level object, e.g. `{"xml": {"params": {"format": "xml"}}}`
   * **uploadFormat** &mdash; Format that uploads should be submitted as. One of `json` or `form`.

   * **auth** &mdash; Object describing the authentication type of this API. The "type" parameter specifies the auth type. All other options are auth-specific.

### `oauth` Authentication

   * "version" &mdash; One of "1.0", "1.0a", or "2.0"
   * "scopeSeparator" &mdash; Separator for scope values. Google Docs uses ` `, Facebook uses `,`, etc.
   * "validate" &mdash; Endpoint (sans `base` or `suffix`) to hit to see if the credentials are still valid.
   * "oob" &mdash; Boolean. If authentication can be done without a server (out-of-band).
   * "oobVerifier" &mdash; Boolean. If out-of-band authentication requires a verification code. Dropbox doesn't, Twitter does, etc.
   * "oobCallback" &mdash; String. Value to be used in place of a callback URL when doing out-of-band authentication. This value is "oob" for some services, or omitted in other services.
   * "requestEndpoint", "accessEndpoint", "authorizeEndpoint" &mdash; **OAuth 1.0 only.** Full URL endpoints for OAuth services.
   * "base" &mdash; **OAuth 2.0 only.** Base URL for all OAuth endpoints.

### `cookies` Authentication

   * "cookies" &mdash; a string array of cookies to preserve for your authentication session.

### `aws-signature` Authentication

This object has no properties. Used for AWS query-signing `Signature` property.