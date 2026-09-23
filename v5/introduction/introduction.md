# Introduction

## Summary

Dotkernel Frontend is a Mezzio and Laminas skeleton for server-rendered web applications with user accounts.
It ships a contact page, generic content pages and user accounts as working examples of its file architecture.
This page also links to the rest of the documentation, the live demo and the project status badges.

## Details

Dotkernel Frontend is an application (skeleton) based on Mezzio microframework using Laminas components.
It's designed as a web starter package suitable for frontend applications.
The current functionality is included as a proof of concept and to showcase Frontend's file architecture:

- Contact us page
- Generic page with copy
- User accounts

Use these building blocks as an example for your own custom code.

Read on to find out more about the application:

- A technical **overview** to understand technical requirements and included packages
- A step-by-step **installation** guide to get you up and running in minutes
- Detailed **how-tos** for working with the current features

Check out our [demo](https://v5.dotkernel.net/).

![OSS Lifecycle](https://img.shields.io/osslifecycle/dotkernel/frontend)
![Packagist Dependency Version](https://img.shields.io/packagist/dependency-v/dotkernel/frontend/php)

[![GitHub issues](https://img.shields.io/github/issues/dotkernel/frontend)](https://github.com/dotkernel/frontend/issues)
[![GitHub forks](https://img.shields.io/github/forks/dotkernel/frontend)](https://github.com/dotkernel/frontend/network)
[![GitHub stars](https://img.shields.io/github/stars/dotkernel/frontend)](https://github.com/dotkernel/frontend/stargazers)
[![GitHub license](https://img.shields.io/github/license/dotkernel/frontend)](https://github.com/dotkernel/frontend/blob/5.0/LICENSE.md)

[![Continuous Integration](https://github.com/dotkernel/frontend/actions/workflows/continuous-integration.yml/badge.svg?branch=5.0)](https://github.com/dotkernel/frontend/actions/workflows/continuous-integration.yml)
[![codecov](https://codecov.io/gh/dotkernel/frontend/graph/badge.svg?token=BQS43UWAM4)](https://codecov.io/gh/dotkernel/frontend)
[![Qodana](https://github.com/dotkernel/frontend/actions/workflows/qodana_code_quality.yml/badge.svg)](https://github.com/dotkernel/frontend/actions/workflows/qodana_code_quality.yml)
[![PHPStan](https://github.com/dotkernel/frontend/actions/workflows/static-analysis.yml/badge.svg?branch=5.0)](https://github.com/dotkernel/frontend/actions/workflows/static-analysis.yml)

## FAQ

### **Q: Is Dotkernel Frontend a finished product?**

A: No. The contact page, the content pages and the user accounts are a proof of concept that shows where your own code goes.
Use them as examples, and change or remove them as your application needs.

### **Q: Which version of Frontend does this documentation cover?**

A: Version 5, which is the `5.0` branch of `dotkernel/frontend`.

### **Q: Does Frontend use request handlers or controllers?**

A: Action controllers.
Each controller extends `Dot\Controller\AbstractActionController`, and the `{action}` route parameter selects the method to run, for example `/user/login` runs `UserController::loginAction()`.

### **Q: Where can I see Frontend running?**

A: The demo is at https://v5.dotkernel.net/.
