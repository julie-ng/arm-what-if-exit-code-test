# ARM `what-if` Test

### Goal

Does `what-if` use an exit code so we can automate checking for configuraiton drift without analyzing output?

### Result - Nope

To detect programmatically detect configuration change, you would need to process result output 😕

```bash
$ az deployment sub what-if \
➜       --location westeurope \
➜       --name armExitCodeTestDeploymentChangedTags \
➜       --template-file ./rg-storage-acct.json \
➜       --parameters \
➜           rgName=arm-test-rg \
➜           storagePrefix=armtest \
➜           rgLocation=westeurope
Note: The result may contain false positive predictions (noise).
You can help us improve the accuracy of the result by opening an issue here: https://aka.ms/WhatIfIssues.

Resource and property changes are indicated with these symbols:
  ~ Modify
  = Nochange

The deployment will update the following scopes

Scope: /subscriptions/<REDACTED>

  ~ resourceGroups/arm-test-rg [2020-06-01]
    ~ tags.demo: "false" => "true"

Scope: /subscriptions/<REDACTED>/resourceGroups/arm-test-rg

  = Microsoft.Storage/storageAccounts/armtest<REDACTED> [2019-06-01]

Resource changes: 1 to modify, 1 no change.

arm-test main [!] at took 18s 
```

### References

- [Azure Docs: ARM template deployment what-if operation](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/template-deploy-what-if?tabs=azure-cli)
- [Azure CLI Reference: az deployment sub what-if](https://docs.microsoft.com/en-us/cli/azure/deployment/sub?view=azure-cli-latest#az_deployment_sub_what_if)

