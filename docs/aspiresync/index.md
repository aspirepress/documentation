---
layout: default
title: Welcome to AspireGuide - AspireSync
permalink: /aspiresync/
---

## What is AspireSync?

[AspireSync](https://github.com/aspirepress/AspireSync) is an open source project that downloads and updates the canonical WordPress plugins and themes repository.

Here are the current main features of AspireSync:

- Download themes and plugins from the WordPress .org repository and upload them to local storage or AWS S3 storage
- Store metadata and other information about every version of every plugin
- Download the latest version of a plugin/theme, or all versions, or a subset
- Handles closed and not found plugins/themes
- Updates only those items that are updated in SVN, so you don't have to pull the entire repository
- Supports Postgres database out of the box for metadata storage
- Operates in up to 24 parallel tasks to allow for a speedy download and sync

## How to install and run AspireSync

NOTE: AspireSync runs in a Docker container, so make sure you have Docker installed. You can run Docker on [Windows or Mac natively](https://docs.docker.com/engine/install/) but these instructions will not cover those situations. The documentation assumes you are running Linux, MacOS Mach or Windows WSL2. To build and use your own Docker container with AspireSync, follow the instructions in the [AspireSync README file](https://github.com/aspirepress/AspireSync/blob/main/README.md).

[See the AspireSync README for a QuickStart install.](https://github.com/aspirepress/AspireSync?tab=readme-ov-file#quick-start)

