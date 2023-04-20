# Prepare local system

## Download latest Ubuntu LTS 
```
docker pull ubuntu:jammy
```

## Connect to Ubuntu image
```
docker run -i -t ubuntu:jammy bash
```

## Update the image
```
apt update && apt upgrade -y && apt autoclean
```

## Install additional tools
```
apt-get install curl nano tmux -y
```

## Install the gcloud CLI
```
apt-get install apt-transport-https ca-certificates gnupg
```

# Installation
1. Add the gcloud CLI distribution URI as a package source. If your distribution supports the signed-by option, run the following command:
```
echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If your distribution doesn't support the signed-by option, run the following command:
```
echo "deb https://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
```

2. Import the Google Cloud public key. If your distribution's apt-key command supports the --keyring argument, run the following command:
```
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If your distribution's apt-key command doesn't support the --keyring argument, run the following command:
```
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If your distribution (Debian 11+ or Ubuntu 21.10+) doesn't support apt-key, run the following command:
```
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | tee /usr/share/keyrings/cloud.google.gpg
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If you can't get latest updates due to an expired key, [obtain the latest apt-get.gpg key file](https://cloud.google.com/compute/docs/troubleshooting/known-issues#keyexpired).

3. Update and install the gcloud CLI:
```
apt-get update && apt-get install google-cloud-cli
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;For additional apt-get options, such as disabling prompts or dry runs, refer to the apt-get man pages.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Docker Tip:** If installing the gcloud CLI inside a Docker image, use a single RUN step instead:
```
RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] http://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg  add - && apt-get update -y && apt-get install google-cloud-cli -y
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If apt-key command is not supported:
```
RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] http://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | tee /usr/share/keyrings/cloud.google.gpg && apt-get update -y && apt-get install google-cloud-sdk -y
```
4. (Optional) Install any of the following [additional components](https://cloud.google.com/sdk/docs/components#additional_components):
- google-cloud-cli
- google-cloud-cli-anthos-auth
- google-cloud-cli-app-engine-go
- google-cloud-cli-app-engine-grpc
- google-cloud-cli-app-engine-java
- google-cloud-cli-app-engine-python
- google-cloud-cli-app-engine-python-extras
- google-cloud-cli-bigtable-emulator
- google-cloud-cli-cbt
- google-cloud-cli-cloud-build-local
- google-cloud-cli-cloud-run-proxy
- google-cloud-cli-config-connector
- google-cloud-cli-datastore-emulator
- google-cloud-cli-firestore-emulator
- google-cloud-cli-gke-gcloud-auth-plugin
- google-cloud-cli-kpt
- google-cloud-cli-kubectl-oidc
- google-cloud-cli-local-extract
- google-cloud-cli-minikube
- google-cloud-cli-nomos
- google-cloud-cli-pubsub-emulator
- google-cloud-cli-skaffold
- google-cloud-cli-spanner-emulator
- google-cloud-cli-terraform-validator
- google-cloud-cli-tests
- kubectl
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;For example, the google-cloud-cli-app-engine-java component can be installed as follows:
```
apt-get install google-cloud-sdk-skaffold google-cloud-sdk-terraform-tools google-cloud-sdk-gke-gcloud-auth-plugin -y
```
5.  Run gcloud init to get started:
```
gcloud init
```