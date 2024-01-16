# Renovate Bug Resolving Private Terraform Registries Terragrunt Files

This repository contains an example to reproduce a bug cause when resolving private Terraform registries on Terragrunt files

The repository contains a [`terragrunt.hcl`](/terragrunt.hcl) file with a dependency to a module published in a private Terraform registry.
To simplify the example, the host of the private Terraform registry is **fictional** so it forces Renovate to **fail** the analysis, and the dependency **is an existent** Terraform Module available in the official Hashicorp Terraform registry:
https://registry.terraform.io/modules/miguelhrocha/helloworld/aws/latest

Renovate is installed and configured too.

## Expected behavior

Renovate **fails** resolving dependency as the private Terraform registry points to an inexistent host.

## Actual behavior

Renovates **resolves** the dependency as the module provide by the Hashicorp Terraform Registry (https://registry.terraform.io). And **tries to update**
the version of the module [`miguelhrocha/helloworld/aws`](https://registry.terraform.io/modules/miguelhrocha/helloworld/aws/latest) to the **latest version 1.1.0**.


## Relevant logs

Output of Terragrunt on `terragrunt init`

```console
$ terragrunt init
WARN[0000] No double-slash (//) found in source URL /briancain/helloworld/aws. Relative paths in downloaded Terraform code may not work. 
ERRO[0000] 1 error occurred:
        * error downloading 'tfr://registry.domain.com/briancain/helloworld/aws?version=2020.4.21': Get "https://registry.domain.com/.well-known/terraform.json": dial tcp: lookup registry.domain.com on 127.0.0.53:53: no such host
 
ERRO[0000] Unable to determine underlying exit code, so Terragrunt will exit with error code 1
```
