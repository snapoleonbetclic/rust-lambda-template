# AWS Lambda with Rust template

This project is a Rust-based AWS Lambda function built with
the [`cargo-lambda`](https://github.com/cargo-lambda/cargo-lambda) tool.
The function can be deployed using either the [Serverless Framework (SLS)](https://www.serverless.com/)
or [AWS SAM (Serverless Application Model)](https://aws.amazon.com/serverless/sam/).
This guide provides a step-by-step approach to set up, build, test, and deploy the function.

## Prerequisites

- **Rust**: Install Rust by following the instructions at [rust-lang.org](https://www.rust-lang.org/).
- **cargo-lambda**: This is a Cargo extension for working with AWS Lambda functions in Rust. You can install it by
  running:
  ```bash
  cargo install cargo-lambda
  ```
- **Serverless Framework (SLS) or AWS SAM**:
    - To install SLS, run: `npm install -g serverless`
    - To install AWS SAM CLI,
      follow [these instructions](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html).

## Commands Overview

# Project Name: AWS Lambda with Rust

This project is a Rust-based AWS Lambda function built with the `cargo-lambda` tool. The function can be deployed using
either the Serverless Framework (SLS) or AWS SAM (Serverless Application Model). This guide provides a step-by-step
approach to set up, build, test, and deploy the function.

## Prerequisites

- **Rust**: Install Rust by following the instructions at rust-lang.org.
- **cargo-lambda**: This is a Cargo extension for working with AWS Lambda functions in Rust. You can install it by
  running:
  ```bash
  cargo install cargo-lambda
  ```
- **Serverless Framework (SLS)** or **AWS SAM**:
    - To install SLS, run:
  ```bash
      npm install -g serverless
  ```
    - To install AWS SAM CLI,
      follow [those instructions](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html).

## Commands Overview

`cargo-lambda` offers several commands to help with building, testing, and deploying Rust Lambda functions. Here’s a
breakdown of the most commonly used commands:

### 1. Build the Lambda Function

The `cargo lambda build` command compiles the Lambda function, ensuring it’s in a format AWS Lambda expects. The command
will output the build artifacts into the `target/lambda/` directory.

Command:
cargo lambda build --release

- `--release`: Builds the Lambda in release mode, optimizing it for production.
- `--arm64`: Builds the Lambda for ARM64 architecture, useful for Apple M1 chips.
- `--x86_64`: Builds the Lambda for x86_64 architecture, useful for Intel chips.
- `--output-format`: Specifies the output format for the build artifacts. You will need this to be set to 'zip' for AWS
  Lambda.

### 2. Test the Lambda Locally

Testing the Lambda locally can help with debugging before deploying. Use `cargo lambda invoke` to send a sample event to
the function:

Command:
cargo lambda invoke --remote

- `--remote`: Tests the function against an AWS Lambda instance, allowing you to see how it behaves in the actual
  environment.

Alternatively, you can invoke the Lambda locally using sample events. For instance:

Command:

```bash
  cargo lambda invoke --data-file sample_event.json
  cargo lambda invoke --data-ascii "{ \"firstName\": \"snap\" }"
```

### 3. Watch Mode for Real-Time Changes

To speed up development, use `cargo lambda watch`. This command will rebuild the function automatically whenever a
source file is changed. It’s useful for rapid iteration and debugging.

Command:

```bash
  cargo lambda watch
```

### 4. Deploying with Serverless Framework (SLS)

If using Serverless Framework for deployment, set up your `serverless.yml` file, specifying details like the Lambda
function name, runtime, and handler. Then run:

Command:

```bash
  sls deploy
```

After deployment, you can invoke the Lambda directly via:

Command:

```bash
  sls invoke -f functionName
```

### 5. Deploying with AWS SAM

With AWS SAM, create a `template.yml` file with necessary configurations for the Lambda function, including handler,
runtime, and memory settings.

To build and package the function for deployment:

Command:
sam build
sam deploy --guided

- `sam build`: Compiles the project using the configurations in `template.yml`.
- `sam deploy`: Deploys the Lambda function interactively, allowing you to specify parameters like the stack
  name and region.

## Summary of Commands

| Command                                | Description                                                  |
|----------------------------------------|--------------------------------------------------------------|
| `cargo lambda build --release`         | Builds the function in release mode.                         |
| `cargo lambda invoke --remote`         | Invokes the function remotely in AWS Lambda.                 |
| `cargo lambda invoke --data-file file` | Invokes locally using a sample event file.                   |
| `cargo lambda watch`                   | Watches for changes and automatically rebuilds the function. |
| `sls deploy`                           | Deploys the function using Serverless Framework.             |
| `sam build`                            | Builds the function for deployment with AWS SAM.             |
| `sam deploy`                           | Deploys the function with AWS SAM, .                         |

This guide should equip you with the knowledge to develop, test, and deploy AWS Lambda functions in Rust
using `cargo-lambda`, Serverless Framework, or AWS SAM.
