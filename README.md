# Gordon
Docker image for [Gordon](https://github.com/jorgebastida/gordon), based on the [Lambda Docker Image](https://github.com/lambci/docker-lambda)

* Requires Docker to be installed and running :whale2: [Docker Install](https://docs.docker.com/engine/installation/)
* Alias it to easily build and deploy using Lambda compatible Libc libraries (No more ELF errors)
* Ensure you have the AWS API env vars set for access key, secret key and default region
```bash
$ git clone git@github.com:danielwhatmuff/gordon-docker.git && cd gordon-docker && docker build -t gordon .
$ alias gordonshell='docker run -ti -e AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY -e AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID -e AWS_DEFAULT_REGION=$AWS_DEFAULT_REGION -v $(pwd):/var/task  --rm gordon bash'
$ alias >> ~/.bash_profile
$ cd yourgordonproject
$ gordonshell
gordonshell> source yourvirtualenv/bin/activate
gordonshell> pip install -r requirements.txt
gordonshell> gordon build && gordon apply
```

# Known Issues
* On Mac - if you leave the Docker daemon running for too long, you will get time drift and gordon commands may fail (so will AWS CLI commands) - to fix, just restart the daemon
