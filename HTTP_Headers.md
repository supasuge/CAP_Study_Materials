# HTTP Security Response Headers Study Sheet

###### Table Of Contents
- [HTTP Security Response Headers Study Sheet](#http-security-response-headers-study-sheet)
          - [Table Of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Security Headers Checklist](#security-headers-checklist)
    - [X-Frame-Options](#x-frame-options)
    - [X-XSS-Protection](#x-xss-protection)
    - [X-Content-Type-Options](#x-content-type-options)
    - [Referrer-Policy](#referrer-policy)
    - [Content-Type](#content-type)
    - [Set-Cookie](#set-cookie)
    - [Strict-Transport-Security (HSTS)](#strict-transport-security-hsts)
    - [Content-Security-Policy (CSP)](#content-security-policy-csp)
    - [Access-Control-Allow-Origin](#access-control-allow-origin)
    - [Cross-Origin-Opener-Policy (COOP)](#cross-origin-opener-policy-coop)
    - [Cross-Origin-Embedder-Policy (COEP)](#cross-origin-embedder-policy-coep)
    - [Cross-Origin-Resource-Policy (CORP)](#cross-origin-resource-policy-corp)
    - [Permissions-Policy](#permissions-policy)
  - [Headers to Remove or Modify](#headers-to-remove-or-modify)
  - [Implementation Examples](#implementation-examples)
    - [PHP](#php)
    - [Apache (.htaccess)](#apache-htaccess)
    - [IIS (Web.config)](#iis-webconfig)
    - [Nginx](#nginx)
    - [Express (Node.js)](#express-nodejs)
  - [Testing Tools](#testing-tools)
  - [References](#references)

## Introduction
HTTP Security Headers enhance web security by preventing vulnerabilities like XSS, Clickjacking, and information disclosure. This study sheet covers key security headers, recommendations, and implementation examples.

## Security Headers Checklist

### X-Frame-Options

- **Purpose**: Prevents clickjacking by controlling page rendering in frames
- **Recommendation**: `X-Frame-Options: DENY`
- **Vulnerabilities Prevented**:
    - Clickjacking attacks
    - UI redress attacks
- **Implications**:
    - Prevents your content from being embedded in other sites' iframes
    - May impact legitimate iframe usage if set too restrictively
- **Note**: Use CSP frame-ancestors if possible (obsoletes X-Frame-Options)

### X-XSS-Protection

- **Purpose**: Stops pages from loading when reflected XSS detected
- **Recommendation**: `X-XSS-Protection: 0` (turn off, use CSP instead)
- **Vulnerabilities Prevented**:
    - Some types of reflected Cross-Site Scripting (XSS) attacks
- **Implications**:
    - Can actually introduce XSS vulnerabilities in otherwise safe websites
    - Modern browsers have deprecated or removed support for this header
- **Note**: Can create vulnerabilities in some cases; prefer Content Security Policy

### X-Content-Type-Options

- **Purpose**: Prevents MIME type sniffing
- **Recommendation**: `X-Content-Type-Options: nosniff`
- **Vulnerabilities Prevented**:
    - MIME type confusion attacks
    - Malicious file execution through MIME type misinterpretation
- **Implications**:
    - Forces browsers to stick to the declared Content-Type
    - May break functionality if Content-Type headers are set incorrectly

### Referrer-Policy

- **Purpose**: Controls referrer information in requests
- **Recommendation**: `Referrer-Policy: strict-origin-when-cross-origin`
- **Vulnerabilities Prevented**:
    - Information leakage through Referer header
    - Cross-origin information disclosure
- **Implications**:
    - Limits the information sent in the Referer header
    - May impact analytics or affiliate systems relying on full referrer information

### Content-Type

- **Purpose**: Indicates the media type of the resource
- **Recommendation**: `Content-Type: text/html; charset=UTF-8`
- **Vulnerabilities Prevented**:
    - XSS attacks through content type misinterpretation
    - Character encoding-based attacks
- **Implications**:
    - Ensures correct rendering and interpretation of content
    - Critical for preventing XSS in certain scenarios
- **Note**: Always set correctly to prevent XSS

### Set-Cookie

- **Purpose**: Sends cookies from server to user agent
- **Recommendation**: See Session Management Cheat Sheet for details
- **Vulnerabilities Prevented**:
    - Cross-Site Scripting (XSS)
    - Cross-Site Request Forgery (CSRF)
    - Session hijacking
- **Implications**:
    - Proper configuration is crucial for secure session management
    - Incorrect settings can expose sessions to various attacks

### Strict-Transport-Security (HSTS)

- **Purpose**: Enforces HTTPS connections
- **Recommendation**: `Strict-Transport-Security: max-age=63072000; includeSubDomains; preload`
- **Vulnerabilities Prevented**:
    - Man-in-the-Middle (MitM) attacks
    - Protocol downgrade attacks
    - Cookie hijacking
- **Implications**:
    - Forces HTTPS for all connections
    - Can cause access issues if SSL/TLS is misconfigured
- **Note**: Use carefully to avoid access issues

### Content-Security-Policy (CSP)

- **Purpose**: Specifies allowed content origins
- **Recommendation**: Customize based on your needs (see CSP Cheat Sheet)
- **Vulnerabilities Prevented**:
    - Cross-Site Scripting (XSS)
    - Clickjacking
    - Formjacking
    - Malicious resource injection
- **Implications**:
    - Provides fine-grained control over resource loading
    - Can break functionality if not configured correctly
- **Resources**: [Content Security Policy Cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html)
### Access-Control-Allow-Origin

- **Purpose**: Controls cross-origin resource sharing
- **Recommendation**: Set specific origins, e.g., `Access-Control-Allow-Origin: https://yoursite.com`
- **Vulnerabilities Prevented**:
    - Unauthorized cross-origin access
    - Data theft through malicious cross-origin requests
- **Implications**:
    - Restricts which domains can access your resources
    - Critical for APIs and services meant to be accessed by specific origins

### Cross-Origin-Opener-Policy (COOP)

- **Purpose**: Isolates browsing context
- **Recommendation**: `Cross-Origin-Opener-Policy: same-origin`
- **Vulnerabilities Prevented**:
    - Cross-origin attacks like Spectre
    - Cross-window scripting attacks
- **Implications**:
    - Isolates your window/tab from others
    - May break integrations that rely on window references

### Cross-Origin-Embedder-Policy (COEP)

- **Purpose**: Controls loading of cross-origin resources
- **Recommendation**: `Cross-Origin-Embedder-Policy: require-corp`
- **Vulnerabilities Prevented**:
    - Data leaks through timing attacks
    - Spectre-like attacks
- **Implications**:
    - Ensures all resources are explicitly allowed to be loaded
    - Can break functionality if third-party resources are not properly configured

### Cross-Origin-Resource-Policy (CORP)

- **Purpose**: Controls which origins can include a resource
- **Recommendation**: `Cross-Origin-Resource-Policy: same-site`
- **Vulnerabilities Prevented**:
    - Side-channel attacks like Spectre
    - Unauthorized resource usage
- **Implications**:
    - Limits resource sharing to same-site contexts
    - May require adjustments for CDN or third-party hosted content

### Permissions-Policy

- **Purpose**: Controls browser feature usage
- **Recommendation**: `Permissions-Policy: geolocation=(), camera=(), microphone=()`
- **Vulnerabilities Prevented**:
    - Unauthorized use of sensitive browser features
    - Potential privacy violations
- **Implications**:
    - Restricts which features your site can use
    - Enhances user privacy and security by limiting feature scope

## Implementation Examples

### PHP

```php
header("X-Frame-Options: DENY");
```

### Apache (.htaccess)

```apache
<IfModule mod_headers.c>
Header always set X-Frame-Options "DENY"
</IfModule>
```

### IIS (Web.config)

```xml
<system.webServer>
 <httpProtocol>
   <customHeaders>
     <add name="X-Frame-Options" value="DENY" />
   </customHeaders>
 </httpProtocol>
</system.webServer>
```

### Nginx

```nginx
add_header "X-Frame-Options" "DENY" always;
```

### Express (Node.js)

```javascript
const helmet = require('helmet');
const app = express();
app.use(helmet.frameguard({ action: "sameorigin" }));
```

## Testing Tools

- Mozilla Observatory
- SmartScanner
- [Venom](https://github.com/ovh/venom): Test suite to validate HTTP security response headers configurations against [OSHP recommendations](https://owasp.org/www-project-secure-headers/#div-bestpractices) 
## References
- [Mozilla Developer Network (MDN) Web Docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- [OWASP Secure Headers Project](https://owasp.org/www-project-secure-headers/)
- [Content Security Policy (CSP) Quick Reference Guide](https://content-security-policy.com/)
	- [OWASP Content Security Policy Cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html)

