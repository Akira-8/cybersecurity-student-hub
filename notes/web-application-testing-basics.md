---
layout: note
title: Web Application Testing Basics
permalink: /notes/web-application-testing-basics/
---

# Web Application Testing Basics

Web application testing is a major part of cybersecurity and pentesting.

The goal is to understand how a web application works, identify weaknesses, and test it in an ethical and authorized way.

## Why Web Testing Matters

Many organizations rely on web applications.

If a web application has weak authentication, poor input handling, or insecure logic, it may expose sensitive data or allow unauthorized access.

## Core Concepts

### Request and Response
A browser sends an HTTP request to a server, and the server sends back an HTTP response.

Understanding requests and responses is one of the first important skills in web security.

### Parameters
Applications often take user input through:

- URL parameters
- forms
- headers
- cookies
- JSON bodies

Testing often focuses on how the application handles that input.

### Authentication
Authentication checks who the user is.

Examples:
- username and password
- MFA
- session-based login

### Authorization
Authorization checks what the user is allowed to do.

A common mistake is when a user can access data or actions they should not have access to.

### Session
A session helps the application remember that a user is logged in.

Security testing often checks whether sessions are properly protected.

## Common Areas to Test

- login forms
- registration pages
- password reset flows
- file upload features
- search boxes
- user profile functionality
- admin panels
- API endpoints

## Common Vulnerability Categories

Examples of common web issues include:

- SQL injection
- cross-site scripting
- broken access control
- insecure direct object references
- command injection
- weak authentication
- weak session management
- file upload issues

## Simple Testing Methodology

A basic approach can be:

1. map the application
2. identify pages and endpoints
3. understand authentication and roles
4. inspect requests and responses
5. test input handling
6. test access control
7. document findings carefully

## Useful Tools

- Burp Suite
- browser developer tools
- FFUF
- curl
- Postman

## Good Testing Habits

- understand the application before testing deeply
- keep notes of endpoints and behavior
- test one thing at a time
- compare normal behavior vs unexpected behavior
- stay within legal scope
- document evidence clearly

## Final Note

Good web testing is not only about using tools.  
It is about understanding application behavior, user roles, data flow, and trust boundaries.
