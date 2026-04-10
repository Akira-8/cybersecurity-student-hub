---
layout: note
title: Burp Suite Basics
description: Learn how to inspect and modify web traffic during testing.
permalink: /notes/burp-suite-basics/
---

# Burp Suite Basics

Burp Suite is one of the most important tools for web application security testing.

It is used to inspect, modify, and analyze HTTP and HTTPS traffic between the browser and the web application.

## What Burp Suite Does

Burp Suite helps you:
- capture web requests and responses
- test web input
- inspect cookies and headers
- analyze application behavior
- repeat and modify requests
- support manual web security testing

## Main Parts of Burp Suite

### Proxy
The Proxy lets Burp sit between your browser and the target application.

This allows you to intercept and inspect web traffic.

### HTTP History
This shows past requests and responses seen by Burp.

### Repeater
Repeater lets you manually edit and resend requests.

This is very useful for testing how an application reacts to changes.

### Intruder
Intruder is used for automated request testing.

It can help with controlled testing in authorized environments.

### Decoder
Decoder helps with encoding and decoding data.

### Comparer
Comparer helps compare different responses or pieces of data.

## Why Burp Suite Is Useful

Burp helps you understand:
- what data the browser sends
- how the server responds
- how cookies and tokens work
- how input changes affect behavior
- whether access control is working correctly

## What to Look at in Requests

When viewing a request, pay attention to:
- HTTP method
- URL path
- query parameters
- cookies
- headers
- body content
- authentication tokens

## What to Look at in Responses

When viewing a response, pay attention to:
- status code
- response body
- redirects
- cookies
- security headers
- error messages
- changes in content

## Common Testing Areas

Burp Suite is often used to inspect:
- login forms
- registration forms
- password reset requests
- profile updates
- file uploads
- API requests
- role-based actions
- hidden fields and parameters

## Important Security Concepts

### Cookies
Cookies are often used to keep a user logged in.

### Session Tokens
Session tokens help the application recognize the same user across requests.

### Headers
Headers give extra information about the request or response.

### Parameters
Parameters are values sent in the URL, body, or headers.

## Good Beginner Workflow

A simple workflow with Burp Suite can be:

1. open the target application
2. capture traffic with the Proxy
3. review the request and response
4. send interesting requests to Repeater
5. change one value at a time
6. compare results
7. document observations

## Good Habits

- understand the normal request first
- change one thing at a time
- keep notes
- compare server responses carefully
- stay within authorized scope
- learn the application before testing deeply

## Final Note

Burp Suite is powerful, but the tool is not the skill.

The real skill is understanding web traffic, application logic, and how to interpret changes in behavior.
