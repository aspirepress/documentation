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

## How to run AspireSync

NOTE: AspireSync runs in a Docker container, so make sure you have Docker installed. You can run Docker on [Windows or Mac natively](https://docs.docker.com/engine/install/) but these instructions will not cover those situations. The documentation assumes you are running Linux, MacOS Mach or Windows WSL2. If you want to build your own Docker container head on over to the [AspireSync README file](https://github.com/aspirepress/AspireSync/blob/main/README.md) for prerequisites and instructions.

You may need to prefix all commands with `sudo` depending on your permission level for your login.

1. `git clone https://github.com/aspirepress/AspireSync` to retrieve  the code base to your environment
2. You will need to setup an [ssh public key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) using this command `ssh-keygen -t ed25519 -C "<YOUR GITHUB EMAIL>"`
3. Check ssh-agent is running:
`eval $(ssh-agent)`
``eval `ssh-agent```
4. Run `ssh-add` to add your identity
5. You can setup a maximum lifetime for keys. For example `ssh-add -t 8h00` will make the key last for 8 hours.
6. Add the SSH public key as an authentication key in your [GitHub account](https://github.com/settings/keys)
7. `git config --global --add safe.directory <your AspireSync directory>`
8. `git submodule update --init && cp .env.dist .env` to create database migrations and create template .env file
9. `make init` to build the Docker container for AspireSync
10. `make list` to see available AspireSync commands
11. `make run` which will run the container.
12. `aspiresync <command>` to execute your desired command.



To use AspireSync from a DockerHub container you can use:

`sudo docker run -it --rm aspirepress/aspiresync sh`

This will run a local docker instance and enter you into a shell ready for use.

### Configuration

These configuration values are required for the Postgres database:

| Env Variable | Description                                    |
| ------------ | ---------------------------------------------- |
| DB_USER      | The username for the database                  |
| DB_PASS      | The password for the database                  |
| DB_NAME      | Name of the database to insert the information |
| DB_HOST      | The hostname of the database                   |
| DB_SCHEMA    | The schema in the database to use              |

The ~/config/autoload/defaults.global.php file must be edited 
### Repository Storage

AspireSync stores the repository assets to a location of your choosing, either in S3(-compatible) storage or local storage on your environment

You can configure the following enviornment variables to determine where assets are stored.

| Env Variable          | Description                                                                                                                                                 |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| UPLOAD_ASSETS_ADAPTER | Which adapter to use for file system uploads (current options are `upload_local_filesystem` or `upload_aws_s3`)                                             |
| UPLOAD_DIR            | The fully qualified directory path to upload files into if UPLOAD_ASSETS_ADAPTER is set to `upload_local_filesystem`                                        |
| AWS_BUCKET            | The bucket to use for Amazon S3 uploads                                                                                                                     |
| AWS_REGION            | Defaults to `us-east-2`, this is the Amazon region to use                                                                                                   |
| AWS_S3_ENDPOINT       | This is a hard-coded bucket endpoint, useful for S3-compatible storage. This is not a required parameter and will default to `null`                         |
| AWS_S3_KEY            | For users of access keys with AWS IAM, this is the access key. If this is not provided, the client will attempt authenticaton through an attached IAM role. |
| AWS_S3_SECRET         | The companion secret to the `AWS_S3_KEY`; this is optional and if omitted will default to IAM role authentication.                                          |

### Usage of AspireSync

 | Command                 | Arguments                          | Options                                        | Description                                                                                           |
 | ----------------------- | ---------------------------------- | ---------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
 | `meta:download:plugins` | None                               | [--update-all or -u] [--plugins]               | Downloads metadata for plugins.                                                                       |
 | `meta:download:themes`  | None                               | [--update-all or -u] [--themes]                | Downloads metadata for themes.                                                                        |
 | `meta:import:plugins`   | None                               | [--update-list]                                | Imports the downloaded metadata for plugins. Assumes you've run `meta:download:plugins`               |
 | `meta:import:themes`    | None                               | [--update-list]                                | Imports the downloaded metadata for themes. Assumes you've run `meta:download:themes`                 |
 | `download:plugins`      | [num-to-pull=latest]               | [--plugins [--force-download or -f]            | Downloads any plugins outstanding from the last time the command was run. Defaults to latest version, |
 | `download:themes`       | [num-to-pull=latest]               | [--themes] [--force-download or  -f]           | Downloads any themes outstanding from the last time the command was run. Defaults to latest version.  |
 | `util:upload`           | action<plugins, themes>            | [--slugs] [--limit] [--offset] [--clean or -c] | Uploads any downloaded plugins/themes to your file system (right now supports S3).                    |
 | `util:clean`            | None                               | None                                           | Cleans the data directory of any files that remain.                                                   |
 | `run:all`               | [asset-type<all, plugins, themes>] | None                                           | Runs the four commands for themes/plugins or both. A shortcut to a full run of the downloader.        |

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


