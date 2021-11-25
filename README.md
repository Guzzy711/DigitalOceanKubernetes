# DigitalOceanKubernetes

## Cluster installation
### System
The cluster will consist of 6 VCPUS, 12 GB of Memory and 240 GB storage. This storage might not be enough if the solution is used in a production environment. 


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
<email    10               true              <UUID>    active
```


