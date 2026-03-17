---
title: Home
layout: home
nav_order: 0
---

# VendorTools
{: .fs-9 }

A set of build tools designed to make creating Vendordeps for FRC easier.
{: .fs-6 .fw-300 }

[Library Template](https://github.com/ApolloFops/VendorTools-template){: .btn .btn-purple }
[Maven Repo Template](https://github.com/ApolloFops/VendorTools-maven-template){: .btn .btn-purple }

---

VendorTools is a set of build tools designed to replace the build scripts in the [WPILib Vendor
Template](https://github.com/wpilibsuite/vendor-template). By replacing the `publish.gradle` script
with a proper Gradle plugin, dependency developers no longer need to maintain their dependencies'
build systems themselves - just import the plugin and configure it, and you're set! Also,
VendorTools provides some CI workflows which are built to allow you to build and publish your
library entirely within GitHub (yes, even the Maven repo!).

This documentation also serves as a sort of unofficial documentation source for the Vendordep JSON
format.
