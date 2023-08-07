## AWS Access Token Rotation

This is a simple script to facilitate rotating access tokens on AWS.

### Why?

AWS access tokens can live for a very long time if no attention is paid to them. They pose a great potential risk since they can grant bad actors access to critical infrastracture of our apps.

### Usage

Clone this repo and run the rotate script:

`./rotate [-kdhv] [-p profile] [-u username] [-c callback]`

The script expects a profile with iam permissions to perform actions on the target user. It also expects a callback script to run with the new token. This allows updating consumers of the token programmatically. If no callback is provided, the new token will be printed out to the console if in verbose mode.

Alternatively, you can use this repo as a submodule of another script that handles the callbacks involved for updating the consumers of the access tokens.

Run `./rotate -h` for more details of the flags and how the script works.

### Prerequisites

- [AWS CLI](https://aws.amazon.com/cli/)
- [jq](https://jqlang.github.io/jq/)
- A user with an access token and a profile set in your aws configs. The user needs the following permissions on the target user:
  - `iam:ListAccessKeys`
  - `iam:CreateAccessKey`
  - `iam:DeleteAccessKey`
