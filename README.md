**SLS3-Legacy** – A fork of Serverless Framework v3 in order to support it a little bit longer.

It is using `sls3` command instead of original `sls` command in order to help separate from original v3 version. Everything else should be same, so original plugins should still work.

It was created mostly to avoid AWS deprecation of older nodejs runtimes which are used for custom resources and allow newer runtimes to be used.

<br/>

# Contents

- [Features](#features)
- [Quick Start](#quick-start)
- [Plugins](https://github.com/serverless/plugins)
- [Contributing](#contributing)
- [Community](#community)
- [Licensing](#licensing)

# <a name="features"></a>Features

- **Hyper-Productive** - Build more and manage less with serverless architectures.
- **Multiple Use-Cases** - Choose from tons of efficient serverless use-cases (APIs, Scheduled Tasks, Event Handlers, Streaming Data Pipelines, Web Sockets & more).
- **Infra & Code** - Deploys both code and infrastructure together, resulting in out-of-the-box serverless apps.
- **Easy** - Enjoy simple syntax to safely deploy deploy AWS Lambda functions, event sources and more without being a cloud expert.
- **Multi-Language** - Supports Node.js, Python, Java, Go, C#, Ruby, Swift, Kotlin, PHP, Scala, & F#
- **Full Lifecycle** - Manages the lifecycle of your serverless architecture (build, deploy, update, monitor, troubleshoot).
- **Multi-Domains** - Group domains into Serverless Services for easy management of code, resources & processes, across large projects & teams.
- **Multi-Environments** - Built-in support for multiple stages (e.g. development, staging, production).
- **Guardrails** - Loaded with automation, optimization and best practices.
- **Extensible** - Extend or modify the Framework and its operations via Plugins.
- **Plugin Ecosystem** - Extend or modify the Framework and its operations via Plugins.
- **Welcoming** - A passionate and welcoming community!

# <a name="quick-start"></a>Quick Start

Here's how to get started quickly, as well as some recommended development workflows.

## Installation

Install `sls3` module via NPM:

```bash
npm install -g sls3-legacy
```

_If you don’t already have Node.js on your machine, [install it first](https://nodejs.org/)._

## Creating A Service

To create your first project (known as a Serverless Framework "Service"), run the `sls3` command below, then follow the prompts.

```bash
# Create a new serverless project
serverless

# Move into the newly created directory
cd your-service-name
```

The `sls3` command will guide you to:

1. Create a new project
2. Configure your [AWS credentials](https://serverless.com/framework/docs/providers/aws/guide/credentials/)
3. Optionally set up a free Serverless Framework account with additional features.

Your new serverless project will contain a `serverless.yml` file. This file features simple syntax for deploying infrastructure to AWS, such as AWS Lambda functions, infrastructure that triggers those functions with events, and additional infrastructure your AWS Lambda functions may need for various use-cases. You can learn more about this in the [Core Concepts documentation](https://www.serverless.com/framework/docs/providers/aws/guide/intro).

The `sls3` command will give you a variety of templates to choose from. If those do not fit your needs, check out the [project examples from Serverless Inc. and our community](https://github.com/serverless/examples). You can install any example by passing a GitHub URL using the `--template-url` option:

```base
sls3 --template-url=https://github.com/serverless/examples/tree/v3/...
```

Please note that you can use `sls3` or `sls3-legacy` to run SLS3-Legacy commands.

## Deploying

If you haven't done so already within the `sls3` command, you can deploy the project at any time by running:

```bash
sls3 deploy
```

The deployed AWS Lambda functions and other essential information such as API Endpoint URLs will be displayed in the command output.

More details on deploying can be found [here](https://www.serverless.com/framework/docs/providers/aws/guide/deploying).

## Developing On The Cloud

Many Serverless Framework users choose to develop on the cloud, since it matches reality and emulating Lambda locally can be complex. To develop on the cloud quickly, without sacrificing speed, we recommend the following workflow...

To deploy code changes quickly, skip the `serverless deploy` command which is much slower since it triggers a full AWS CloudFormation update. Instead, deploy code and configuration changes to individual AWS Lambda functions in seconds via the `deploy function` command, with `-f [function name in serverless.yml]` set to the function you want to deploy.

```bash
sls3 deploy function -f my-api
```

More details on the `deploy function` command can be found [here](https://www.serverless.com/framework/docs/providers/aws/cli-reference/deploy-function).

To invoke your AWS Lambda function on the cloud, you can find URLs for your functions w/ API endpoints in the `serverless deploy` output, or retrieve them via `serverless info`. If your functions do not have API endpoints, you can use the `invoke` command, like this:

```bash
sls3 invoke -f hello

# Invoke and display logs:
sls3 invoke -f hello --log
```

More details on the `invoke` command can be found [here](https://www.serverless.com/framework/docs/providers/aws/cli-reference/invoke).

To stream your logs while you work, use the `sls logs` command in a separate terminal window:

```bash
sls3 logs -f [Function name in serverless.yml] -t
```

Target a specific function via the `-f` option and enable streaming via the `-t` option.

## Developing Locally

Many Serverless Framework users rely on local emulation to develop more quickly. Please note, emulating AWS Lambda and other cloud services is never accurate and the process can be complex. We recommend the following workflow to develop locally...

Use the `invoke local` command to invoke your function locally:

```bash
sls3 invoke local -f my-api
```

You can also pass data to this local invocation via a variety of ways. Here's one of them:

```bash
sls3 invoke local --function functionName --data '{"a":"bar"}'
```

More details on the `invoke local` command can be found [here](https://www.serverless.com/framework/docs/providers/aws/cli-reference/invoke-local)

Serverless Framework also has a great plugin that allows you to run a server locally and emulate AWS API Gateway. This is the `serverless-offline` command.

More details on the **serverless-offline** plugins command can be found [here](https://github.com/dherault/serverless-offline)

## Monitoring, Secrets & Collaboration

If you're looking for easy, out-of-the-box monitoring, secrets management and collaboration features, sign into the Serverless Framework Dashboard. It's free!

```bash
sls3 login
```

## Remove your service

If you want to delete your service, run `remove`. This will delete all the AWS resources created by your project and ensure that you don't incur any unexpected charges. It will also remove the service from Serverless Dashboard.

```bash
sls3 remove
```

More details on the `remove` command can be found [here](https://www.serverless.com/framework/docs/providers/aws/cli-reference/remove).

# <a name="licensing"></a>Licensing

SLS3-Legacy is licensed under the [MIT License](./LICENSE.txt).

All files located in the node_modules and external directories are externally maintained libraries used by this software which have their own licenses; we recommend you read them, as their terms may differ from the terms in the MIT License.
