# ecr-template
Template for deploying Docker containers to [Amazon Elastic Container 
Registry](https://aws.amazon.com/ecr)

## Usage

### Setup

1. Create a new repo by following the [Creating a repository from a 
   template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template) 
   guide.

2. Clone the template locally

```bash
git clone github.com/your_username/repo
```

3. Modify the `makefile.json` file

Should be self-explanitory

`aws:account_id`    : Your AWS account ID
`aws:ecr:region`    : Region your registry is located
`aws:ecr:uri`       : URI for your registry
`docker:image_name` : Name for the Docker image. This must also match the 
`repositry` name you created in Step 1.
``

Example

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

### Deploy locally
