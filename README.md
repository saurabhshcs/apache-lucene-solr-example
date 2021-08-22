# apache-lucene-solr-example
This is PoC setup for fetching batch records and making solr document and allow business text based search rather making routine db calls.


## Solr on Kubernetes on local Mac
### Setup Kubernetes and Dependencies
```shell
# Install Homebrew, if you don't have it already
/bin/bash -c "$(curl -fsSL \
	https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

# Install Docker Desktop for Mac (use edge version to get latest k8s)
brew cask install docker-edge

# Enable Kubernetes in Docker Settings, or run the command below:
sed -i -e 's/"kubernetesEnabled" : false/"kubernetesEnabled" : true/g' \
    ~/Library/Group\ Containers/group.com.docker/settings.json

# Start Docker for mac from Finder, or run the command below
open /Applications/Docker.app

# Install Helm, which we'll use to install the operator, and 'watch'
brew install helm watch
```
### Install an Ingress Controller
> Kubernetes services are by default only accessible from within the k8s cluster. To make them adressable from our laptop, we’ll add an ingress controller

```shell
# Install the nginx ingress controller
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/cloud/deploy.yaml

# Inspect that the ingress controller is running by visiting the Kubernetes dashboard 
# and selecting namespace `ingress-nginx`, or running this command:
kubectl get all --namespace ingress-nginx

# Edit your /etc/hosts file (`sudo vi /etc/hosts`) and replace the 127.0.0.1 line with:
127.0.0.1	localhost default-example-solrcloud.ing.local.domain ing.local.domain default-example-solrcloud-0.ing.local.domain default-example-solrcloud-1.ing.local.domain default-example-solrcloud-2.ing.local.domain dinghy-ping.localhost
```
> Once we have installed Solr to our k8s, this will allow us to address the nodes locally.



Follow me on - [Medium](https://saurabhshcs.medium.com) | [Linkedin](https://www.linkedin.com/in/saurabhshcs/) | [YouTube](https://www.youtube.com/channel/UCSQqjPw7_tfx1Ie4yYHbcxQ?pbjreload=102) | [StackOverFlow](https://stackoverflow.com/users/10719720/saurabhshcs?tab=profile)


