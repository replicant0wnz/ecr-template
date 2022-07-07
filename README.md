# ecr-template

[![GitHub Actions](https://img.shields.io/badge/use%20this-template-blue?logo=github)](https://github.com/badges/shields/generate)
[![Latest commit](https://img.shields.io/github/last-commit/replicant0wnz/ecr-template)](https://github.com/replicant0wnz/ecr-template/commits/main)
[![LICENSE](https://img.shields.io/github/license/replicant0wnz/ecr-template)](https://github.com/replicant0wnz/ecr-template/blob/main/LICENSE)

![Makefile](https://repository-images.githubusercontent.com/506043534/2a6e120c-bd26-4ea9-99f0-2e42431a47b4)

Template for deploying Docker containers to [Amazon Elastic Container 
Registry](https://aws.amazon.com/ecr) (ECR). It allows you to either deploy 
locally via the command line or by [Github Actions](https://github.com/actions).

## Usage

### Setup

#### New repo

1. Create a new repo by following the [Creating a repository from a 
   template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template) 
   guide.

2. Clone the repo

    ```bash
    git clone github.com/your_username/repo
    ```

3. Copy the files and `Dockerfile` needed for your container to the cloned repo.

#### Existing repo

1. Clone this repo

    ```bash
    git clone github.com/replicant0wnz/ecr-template
    ```

2. Copy the `Makefile`, `makefile.json`, and the `.github/workflows/release.yml` 
   files to your repo directory.

    ```bash
    cp Makefile makefile.json .github/workflows/release.yml /path/to/your/repo
    ```

#### Modify the `makefile.json` file

1. `aws:account_id`    : Your AWS account ID<br>
`aws:ecr:region`    : Region your registry is located<br>
`aws:ecr:uri`       : URI for your registry<br>
`docker:image_name` : Name for the Docker image (Must match the `repository` 
name you created in ECR)

    Example:

    ```json
    {
        "aws": {
            "account_id" : "123456789012",
            "ecr" : {
                "region" : "us-east-1",
                "uri" : "public.ecr.aws/your_ecr"
            }
        },
        "docker": {
            "image_name" : "alpine"
        }
    }

    ```

### Deploying to ECR

#### Via the command line

1. Setup your AWS credentials via the `AWS_ACCESS_KEY_ID` and 
   `AWS_SECRET_ACCESS_KEY` environment variables. 

    Example:

    ```bash
    export AWS_ACCESS_KEY_ID=`grep aws_access_key_id ~/.aws/credentials | awk '{print $3}'`
    export AWS_SECRET_ACCESS_KEY=`grep aws_secret_access_key ~/.aws/credentials | awk '{print $3}'`
    ```
2. Execute `make all`

#### Github Actions via a tag

1. Setup your AWS credntials under Settings -> Secrets -> Actions. Refer to
   [Encrypted secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets) 

   Example:

   ![Example](https://github.com/replicant0wnz/ecr-template/blob/assets/secrets.png)

2. Update the following section of `.github/actions/release` with the version tag you'd like
   to use. ie `v1.*` or `1.*` or `release-*` etc

   ```yaml
    on: 
      push:
        tags:
          - 1.*
   ```

3. Tag the release to deploy. Example:

   ```bash
   git tag 1.1.2 ; git push origin --tags
   ```
