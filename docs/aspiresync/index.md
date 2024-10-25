---
layout: default
title: Welcome to AspireSync
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
- Supports Postgres databse out of the box for metadata storage
- Operates in up to 24 parallel tasks to allow for a speedy download and sync

## How to install and run AspireSync

NOTE: AspireSync runs in a Docker container, so make sure you have Docker installed. You can run Docker on [Windows or Mac natively](https://docs.docker.com/engine/install/) but these instructions will not cover those situations. The documentation assumes you are running Linux, MacOS Mach or Windows WSL2. To build and use your own Docker container with AspireSync, follow the instructions in the [AspireSync README file](https://github.com/aspirepress/AspireSync/blob/main/README.md).

You may need to prefix commands with `sudo` depending on your permission level for your login.

1. `git clone https://github.com/aspirepress/AspireSync` to retrieve  the code base to your environment
   
2.  `make init` to build the Docker container for AspireSync
    
3. `make list` to see available AspireSync commands
    
4. `make run` which will run the container.
    
5. `aspiresync <command>` to execute your desired command.


To use AspireSync from a DockerHub container you can use:

`sudo docker run -it --rm aspirepress/aspiresync sh`

This will run a local docker instance and enter you into a shell ready for use.


## Contributing

AspirePress welcomes contributions from people like you. We encourage you to review
our [Contribution Guidelines](https://github.com/aspirepress/.github/blob/main/CONTRIBUTING.md).

## Code of Conduct

AspirePress also implements a [Code of Conduct](https://github.com/aspirepress/.github/blob/main/CODE_OF_CONDUCT.md),
adherance to which is required by all members of the project.

## Credits

AspirePress is a community project, powered by people just like you. Thank you to
our [contributors](https://github.com/aspirepress/.github/blob/main/CREDITS.md) for their generous participation in
AspirePress.


