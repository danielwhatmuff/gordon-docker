# Gordon
Docker image for [Gordon](https://github.com/jorgebastida/gordon), based on the [Lambda Docker Image](https://github.com/lambci/docker-lambda)

* Requires Docker to be installed and running :whale2: [Docker Install](https://docs.docker.com/engine/installation/)
* Alias it to easily build and deploy using Lambda compatible Libc libraries (No more ELF errors)
* Ensure you have the AWS API env vars set for access key, secret key and default region - or use config files

## Or pull the image from Docker Hub
```bash
$ docker pull danielwhatmuff/gordon
```

## Using exported AWS_DEFAULT_REGION, AWS_SECRET_ACCESS_KEY and AWS_ACCESS_KEY_ID env vars
```
$ git clone git@github.com:danielwhatmuff/gordon-docker.git && cd gordon-docker && docker build -t gordon .
$ alias gordonshell='docker run -ti -e AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY -e AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID -e AWS_DEFAULT_REGION=$AWS_DEFAULT_REGION -v $(pwd):/var/task  --rm gordon bash'
$ alias >> ~/.bash_profile
$ cd yourgordonproject
$ gordonshell
gordonshell> gordon build && gordon apply
```

## Using cross account IAM role from CLI config ~/.aws/credentials or ~/.aws/config
* Example CLI config:-
```bash
[profile myprofile]
region = ap-southeast-2
role_arn = arn:aws:iam::ACCOUNTNUMBER:role/YourCrossAccountAssumableRole
```
* Mount the config into the container and set AWS_PROFILE
```
$ alias gordonshell='docker run -ti -e AWS_PROFILE=$AWS_PROFILE -e -v $(pwd):/var/task -v ~/.aws/:/root/.aws  --rm gordon bash'
gordonshell> gordon build && gordon apply
```

```bash
```

# Known Issues
* On Mac - if you leave the Docker daemon running for too long, you will get time drift and gordon commands may fail (so will AWS CLI commands) - to fix, just restart the daemon
