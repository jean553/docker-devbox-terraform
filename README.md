# Terraform Docker

Dockerfile and documentation to run Terraform commands into an isolated container.

Based on Terraform documentation from [here](https://developer.hashicorp.com/well-architected-framework/operational-excellence/verify-hashicorp-binary#create-alpine-linux-container-with-hashicorp-tools).

## Build the image

```sh
docker build -t docker-devbox-terraform . \
    --build-arg PRODUCT=terraform \
    --build-arg VERSION=1.11.4          # set Terraform version here
```

## Run Terraform commands

```sh
docker run -it \
    -w /terraform \
    -v $(pwd):/terraform \
    -v ~/.aws/credentials:/root/.aws/credentials \
    -v ~/.config/scw/config.yaml:/root/.config/scw/config.yaml \     # required for Scaleway cloud provider;
    -e AWS_PROFILE=scw \                                             # optional, if your configuration is setup with several profiles;
    docker-devbox-terraform \
    terraform plan
```
