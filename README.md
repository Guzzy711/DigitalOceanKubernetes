# DigitalOceanKubernetes

Hello and welcome to my write up for my kubernetes installation. I have no prior experience with kubernetes, and very inexperrienced with docker too - this will be interesting. 

## Requirements
ELK stack consists of three components:
- **(E)lasticSearch**
- **(L)ogstash**
- **(K)ibana**
- (*Fluentd*)

And then something to ship our logs - here we will use Fluentd for collecting, transforming and shipment of our logs to the backend of Elastic. 

## Cluster installation
### System
The cluster will consist of 6 VCPUS, 12 GB of Memory and 240 GB storage. This storage might not be enough if the solution is used in a production environment. 

I chose a cluster consisting of 1 pool with 3 pods for elastic, and 1 for kibana. 
I had to install homebrew in order to install and configure doctl. Dotctl is Digital Oceans own cmd line interface. 


```bash
# installing homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
# installing dotctl
brew install doctl
```
After that i needed to create an API-key for dotctl to communicate with my DO-account.

```bash
dotctl auth init
    OUTPUT: Enter your access token: 
            Validating token... OK
doctl auth list
    OUTPUT:
        default (current)
```

To Verify that dotctl is correctly setup:
```bash
doctl account get
    OUTPUT: 

Email                 Droplet Limit    Email Verified    UUID                                    Status
<email                   10               true              <UUID>                               active
```

Now we should be able to run our kubernetes cluster management command

```bash
doctl kubernetes cluster kubeconfig save <id>

    OUTPUT:
        Notice: Adding cluster credentials to kubeconfig file found in "/Users/admin/.kube/config" 
        Notice: Setting current-context to do-lon1-k8s-1-21-5-do-0-lon1-<>
```
However it might take some time for DO to provision your newly created cluster.

## Namespace
Now we need to create a namespace to install all of our logging capabilities on. A namespace is a virtual cluster, which means that we can seperate our objects within our cluster. 