
# SINCE THE UPSTREAM aws-actions/configure-aws-credentials@master IS UPDATED, USE THAT ONE INSTEAD. [MORE INFO HERE](https://github.com/elseu/sdu-awesome-actions#login-to-aws).

------------
# AWS Federated Login Action

> Action to get an access to AWS via OpenID Connect (OIDC)

## Table of Contents <!-- omit in toc -->

- [Purpose](#purpose)
- [Requirements](#requirements)
- [Inputs](#inputs)
- [Outputs](#outputs)
- [Usage](#usage)
- [Maintainers](#maintainers)
- [Contributing](#contributing)
- [License](#license)

## Purpose

You can use this action to authenticate to an Open ID Connect in AWS. This uses [Github's OpenID Connect (OIDC)](https://github.com/github/roadmap/issues/249.).

## Requirements

The action requires you to have:
* A configured OIDCProvider in AWS. Instructions [Terraform](https://stackoverflow.com/a/69243572/16982049)/[CloudFormation](https://awsteele.com/blog/2021/09/15/aws-federation-comes-to-github-actions.html).
* An AWS IAM Profile with specific trust policy. Instructions [Terraform](https://stackoverflow.com/a/69243572/16982049)/[CloudFormation](https://awsteele.com/blog/2021/09/15/aws-federation-comes-to-github-actions.html).

## Inputs

The action has two possible inputs:

* `role-arn` (required): AWS ARN of AWS IAM Role to assume (required).
* `session-duration` (optional): Time in seconds that the session keys need to be valid (AWS_ACCESS_* only). Default 1000s. 

## Outputs

* `token`: the bearer token you can use to communicate with your cluster. Note that this is only valid for a few minutes.
* `raw`: the raw output of `aws eks get-token`. This is a JSON structure that includes extra metadata.
* `aws_web_identity_token_file`: the web identity token file which can be used by the [AWS cli/SDK](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-role.html#cli-configure-role-oidc).
* `aws_access_key_id`: AWS access key id associated with an IAM role.
* `aws_secret_access_key`: AWS access key associated with an IAM role.
* `aws_session_token`: Session token value from STS for temporary security credentials 

All outputs are masked in your logging.

## Usage

In this example we log in with AWS, get a token, and then pass the token to an input in a next step:

```yaml
- name: Configure AWS authentication
  id: configure-aws
  uses: elseu/sdu-federated-aws-login-action@1.0.0
  with:
    role-arn: arn:aws:iam::123456789012:role/gha-role

- run: aws sts get-caller-identity --region eu-west-1

```


## Maintainers

- [Johan Steenhoven](https://github.com/sbkg0002) (Sdu)

## Contributing

Please create a branch named `feature/X` or `bugfix/X` from `master`. When you are done, send a PR to one of the maintainers.

## License

MIT License

Copyright (c) 2021 Sdu Uitgevers BV

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

© 2021 Sdu Uitgevers BV
