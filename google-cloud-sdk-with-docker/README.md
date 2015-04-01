## google/cloud-sdk + docker

This docker container image adds the docker client to google/cloud-sdk.

The `gcloud` command on CoreOS is actually an alias defined in `/etc/profile.d/google-cloud-sdk.sh`. The alias looks like this:
```
alias gcloud="(docker images google/cloud-sdk || docker pull google/cloud-sdk) > /dev/null;docker run -t -i --net="host" -v $HOME/.config:/.config google/cloud-sdk gcloud"
```
So the gcloud tool actually runs in a docker container. Because of this, `gcloud preview docker` does not work, because docker is not installed in that container. The command returns with an error: `ERROR: (gcloud.preview.docker) Docker is not installed.`.

To solve this problem the `google/cloud-sdk` container needs the docker client installed and access to the docker unix socket to communicate with the docker daemon. This container adds docker. Make sure to execute with `-v /var/run/docker.sock:/var/run/docker.sock` to allow the docker client access to the host's docker daemon unix socket.

This docker container image is available in the docker registry as automated build: [geertjohan/google-cloud-sdk-with-docker](https://registry.hub.docker.com/u/geertjohan/google-cloud-sdk-with-docker/).

### Usage in CoreOS
Add the following to your `cloud-config.yaml` file.

```
write_files:
  - path: /opt/gcloud
    permissions: 0755
    content: |
      #!/bin/bash
      (docker images geertjohan/google-cloud-sdk-with-docker || docker pull geertjohan/google-cloud-sdk-with-docker) > /dev/null;
      docker run -t -i --net="host" -v $HOME/.config:/.config -v /var/run/docker.sock:/var/run/docker.sock geertjohan/google-cloud-sdk-with-docker gcloud "$@"
  - path: /opt/gcutil
    permissions: 0755
    content: |
      #!/bin/bash
      (docker images geertjohan/google-cloud-sdk-with-docker || docker pull geertjohan/google-cloud-sdk-with-docker) > /dev/null;
      docker run -t -i --net="host" -v $HOME/.config:/.config -v /var/run/docker.sock:/var/run/docker.sock geertjohan/google-cloud-sdk-with-docker gcutil"
  - path: /opt/gsutil
    permissions: 0755
    content: |
      #!/bin/bash
      (docker images geertjohan/google-cloud-sdk-with-docker || docker pull geertjohan/google-cloud-sdk-with-docker) > /dev/null;
      docker run -t -i --net="host" -v $HOME/.config:/.config -v /var/run/docker.sock:/var/run/docker.sock geertjohan/google-cloud-sdk-with-docker gsutil "$@"
  - path: /etc/profile.d/google-cloud-sdk.sh
    permissions: 0644
    content: |
      #!/bin/sh
      alias gcloud="/opt/gcloud"
      alias gcutil="/opt/gcutil"
      alias gsutil="/opt/gsutil"
```
