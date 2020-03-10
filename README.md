# Vault AppRole Terraform module

Terraform module which creates Vault AppRole

## Usage

```hcl
module "approle" {
  source = "github.com/makezbs/terraform-vault-approle.git"

  role_name   = "mySuperApp"
  policy_name = "mySuperApp"
  policy      = <<EOT
  path "secret/data/mySuperApp" {
    capabilities = ["read","list","update"]
  }
  EOT
}
```

## Providers

| Name | Version |
|------|---------|
| vault | ~> 2.8 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:-----:|
| disallowed\_policies | List of disallowed policies for given role. | `list(string)` | <pre>[<br>  "default"<br>]</pre> | no |
| display\_name | String containing the token display name | `string` | n/a | yes |
| explicit\_max\_ttl | If set, will encode an explicit max TTL onto the token in number of seconds. This is a hard cap even if token\_ttl and token\_max\_ttl would otherwise allow a renewal. | `any` | n/a | yes |
| name | Common name for policy and token | `string` | n/a | yes |
| no\_default\_policy | Flag to not attach the default policy to this token | `bool` | n/a | yes |
| no\_parent | Flag to create a token without parent | `bool` | `true` | no |
| num\_uses | The number of allowed uses of this token | `number` | n/a | yes |
| orphan | If true, tokens created against this policy will be orphan tokens. | `bool` | n/a | yes |
| path\_suffix | Tokens created against this role will have the given suffix as part of their path in addition to the role name. | `string` | n/a | yes |
| period | The period of this token | `number` | n/a | yes |
| policy | String containing a Vault policy | `string` | n/a | yes |
| renew\_increment | The renew increment | `number` | n/a | yes |
| renew\_min\_lease | The minimal lease to renew this token | `number` | n/a | yes |
| renewable | Wether to disable the ability of the token to be renewed past its initial TTL. | `bool` | `"true"` | no |
| token\_period | If set, indicates that the token generated using this role should never expire. The token should be renewed within the duration specified by this value. At each renewal, the token's TTL will be set to the value of this field. Specified in seconds. | `number` | n/a | yes |
| ttl | The TTL period of this token | `string` | `"4h"` | no |

## Outputs

| Name | Description |
|------|-------------|
| client\_token | Client vault token |
| token\_id | Token ID |
