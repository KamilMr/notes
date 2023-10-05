## Access-Control-Expose-Headers
The Access-Control-Expose-Headers response header allows a server to

## Same Origin Policy
(https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)[Link];
🔒 The same-origin policy restricts interactions between different origins to enhance security by isolating potentially malicious documents.

### Facts
- 🌐 Same-origin policy prevents documents from one origin from accessing resources of another origin.
- ⚙️ It reduces attack vectors by isolating potentially harmful content.
- ❌ Cross-origin reads are generally disallowed, but leaks can occur through embedding.
- 🚫 Prevent cross-origin writes with Cross-Site Request Forgery (CSRF) tokens.
- 💡 Use CORS to allow controlled cross-origin access.
- 👥 JavaScript APIs like window.postMessage enable communication between different-origin documents.
- 🖼️ Certain resources, such as images and media, can be embedded cross-origin.
- 🍪 Cookies are also subject to same-origin restrictions in most cases.

### Origin Comparison
- ✅ URLs with the same scheme, host, and port have the same origin.
- ❌ Different protocol, port, or host leads to different origins.
- ℹ️ Examples provided for origin comparisons.

### Inherited Origins
- 🧬 Scripts from about:blank or javascript: URLs inherit the origin of the containing document.

### Changing Origin
- 🔄 Pages can change their own origin using document.domain, with limitations.
- 🌐 document.domain can be set to a superdomain for same-origin checks.

### Cross-Origin Script Access
- 📜 JavaScript APIs like iframe.contentWindow allow limited cross-origin interactions.
- 📨 Use window.postMessage for communication between documents of different origins.

### Cross-Origin Data Storage
- 📦 Web Storage and IndexedDB are separated by origin, preventing cross-origin access.
- 🍪 Cookies can be set for a domain or its parent, with limitations.

### Security Considerations
- 🔒 Secure practices include CSRF tokens, CORS, and careful embedding.
- ⚠️ Some properties and APIs have limitations on cross-origin access.ndicate which response headers should be made available to scripts running in the browser, in response to a cross-origin request.

## CORS
[link](https://developer.mozilla.org/en-US/docs/Glossary/CORS)

### Summary
🔒 CORS (Cross-Origin Resource Sharing) is a system that allows web servers to control cross-origin access to their resources by transmitting specific HTTP headers.

### Facts
- 🌐 **Access-Control-Allow-Origin**: Indicates if the response can be shared.
- 🍪 **Access-Control-Allow-Credentials**: Determines if response can be exposed with credentials.
- 📜 **Access-Control-Expose-Headers**: Lists headers that can be exposed in the response.
- ⚙️ **Access-Control-Allow-Methods**: Specifies allowed methods in response to a preflight request.
- ⏳ **Access-Control-Max-Age**: Defines how long preflight results can be cached.
- 📝 **Access-Control-Request-Method**: Used in preflight to specify the method for the actual request.
- 🌍 **Origin**: Indicates the source of a fetch.
- ⏱️ **Timing-Allow-Origin**: Specifies origins allowed to see attributes via Resource Timing API.

## Cookies

### Summary
🍪 An HTTP cookie is a small piece of data sent by a server to a browser. It's used for session management, personalization, and tracking user behavior. Cookies can have different lifetimes, scopes, and attributes.

### Facts
- An HTTP cookie is sent by a server to a browser, which can store and send it back to the server.
- Cookies are used for session management, personalization, and tracking user behavior.
- Cookies have attributes like expiration date, domain, and path that define their behavior.
- Session cookies expire when the session ends, while permanent cookies expire based on the "Expires" or "Max-Age" attribute.
- Secure and HttpOnly attributes can enhance cookie security.
- SameSite attribute controls when cookies are sent with cross-site requests.
- Cookie prefixes like "__Host-" and "__Secure-" add security layers.
- JavaScript can create and access cookies using Document.cookie.
- Cookies can be used for tracking and can be blocked by browsers.
- Privacy regulations like GDPR and ePrivacy Directive govern cookie use.
- Web Storage API and IndexedDB provide alternatives to cookies for storing data in the browser.

### Tips
- 🍪 Cookies remember things and help personalize online experiences.
- ⏰ Session cookies vanish when you close your browser; permanent ones stick around.
- 🔒 Secure and HttpOnly attributes keep cookies safe from various threats.
- 🌐 SameSite attribute controls when cookies travel between websites.
- 📝 Use cookies responsibly to respect user privacy and comply with regulations.
