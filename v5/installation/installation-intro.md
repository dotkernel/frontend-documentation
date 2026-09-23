# Introduction

## Summary

This tutorial installs Dotkernel Frontend from scratch: cloning the project, installing dependencies, configuring it, preparing the database and running it.
Each step lists the commands to run and the output to expect.

## Details

In this tutorial, we will install Dotkernel Frontend from scratch.
We will focus on these tasks:

- Highlight 3rd party tools required for the installation.
- Provide all the relevant commands with expected responses.
- Configure the development environment.
- Run the project.

By the end of this tutorial you will have a fully-functional Dotkernel Frontend on your selected environment and can begin coding.

## FAQ

### **Q: In which order should I follow the installation pages?**

A: Getting Started, Composer, Configuration Files, Doctrine ORM, Development Mode, then Running the Application.
If you hit permission errors, see the FAQ page.

### **Q: What do I need installed before I start?**

A: Git, PHP 8.2 or 8.3 with the required extensions, Composer, and MariaDB or MySQL.
Node.js and npm are needed only if you change the frontend assets.

### **Q: Can I install Frontend with `composer create-project`?**

A: Yes. `composer create-project dotkernel/frontend` installs the latest release, and `composer.json` enables development mode after the project is created.
This tutorial uses `git clone` instead, which installs the current default branch even if it has not been released.
