## Creating an Azure Container Service cluster using the Azure CLI

##### Create a resource group:
```
~ sauryadas$ azure group create <resource-group-name> <location>
```

##### Generate a skeleton(configuration file) to set parameters:
```
~ sauryadas$ azure container config create --parameter-file <parameter-file-name.json>
```
##### Deploy the cluster using the command:
```
~ sauryadas$ azure container create <resource-group-name> <container-service-name> --parameter-file <parameter-file-name.json>
```

It takes about 15 minutes to deploy the cluster.

Please copy the code below into a  parameter json file (acstemplate.json) to deploy a Swarm cluster.
```
{
  "provisioningState": "",
  "orchestratorProfile": {
    "orchestratorType": "Swarm"
  },
  "masterProfile": {
    "count": 1,
    "dnsPrefix": “acsDnsMaster12345”,
    "fqdn": ""
  },
  "agentPoolProfiles": [
    {
      "name": “acsAgent12345”,
      "count": null,
      "vmSize": "Standard_A1",
      "dnsPrefix": "acsDnsAgent12345",
      "fqdn": ""
    }
  ],
  "linuxProfile": {
    "adminUsername": "azureuser",
    "ssh": {
      "publicKeys": [
        {
          "keyData": “<PLEASE-ENTER-YOUR-PUBLIC-SSH-KEY>“
        }
      ]
    }
  },
  "id": null,
  "name": "xplatContainer21664",
  "type": null,
  "location": "australiasoutheast",
  "tags": {}
}
```

*****Please make sure that you fill in the public SSH key. Every other required parameter is filled for your convenience*****

Follow instructions to generate SSH RSA keys in [section SSH Key Generation](https://github.com/Azure/azure-quickstart-templates/blob/master/101-acs-mesos/docs/SSHKeyManagement.md#ssh-key-generation)


##### List container service by resource group:
```
~ sauryadas$ azure container list <resource-group-name>
```

##### Display status of a container service:
```
~ sauryadas$ azure container show <resource-group-name> <container-service-name>
```

##### Delete a container:
```
~ sauryadas$ azure container delete <resource-group-name> <container-service-name>
```
