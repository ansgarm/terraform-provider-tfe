---
layout: "tfe"
page_title: "Terraform Enterprise: tfe_policy"
description: |-
  Manages policies.
---

# tfe_policy

Policies are rules enforced on Terraform runs. You can use policies to validate that the Terraform plan complies with security rules and best practices.
Two policy-as-code frameworks are integrated with Terraform Enterprise: Sentinel and Open Policy Agent (OPA).

Policies are configured on a per-organization level and are organized and
grouped into policy sets, which define the workspaces on which policies are
enforced during runs.


## Example Usage

Basic usage for Sentinel:

```csharp
using Constructs;
using HashiCorp.Cdktf;
/*Provider bindings are generated by running cdktf get.
See https://cdk.tf/provider-generation for more details.*/
using Gen.Providers.Tfe;
class MyConvertedCode : TerraformStack
{
    public MyConvertedCode(Construct scope, string name) : base(scope, name)
    {
        new Policy.Policy(this, "test", new PolicyConfig {
            Description = "This policy always passes",
            EnforceMode = "hard-mandatory",
            Kind = "sentinel",
            Name = "my-policy-name",
            Organization = "my-org-name",
            Policy = "main = rule { true }"
        });
    }
}
```

Basic usage for Open Policy Agent(OPA):

```csharp
using Constructs;
using HashiCorp.Cdktf;
/*Provider bindings are generated by running cdktf get.
See https://cdk.tf/provider-generation for more details.*/
using Gen.Providers.Tfe;
class MyConvertedCode : TerraformStack
{
    public MyConvertedCode(Construct scope, string name) : base(scope, name)
    {
        new Policy.Policy(this, "test", new PolicyConfig {
            Description = "This policy always passes",
            EnforceMode = "mandatory",
            Kind = "opa",
            Name = "my-policy-name",
            Organization = "my-org-name",
            Policy = "package example rule[\\\"not allowed\\\"] { false }",
            Query = "data.example.rule"
        });
    }
}
```

## Argument Reference

The following arguments are supported:

* `Name` - (Required) Name of the policy.
* `Description` - (Optional) A description of the policy's purpose.
* `Organization` - (Optional) Name of the organization. If omitted, organization must be defined in the provider config.
* `Kind` - (Optional) The policy-as-code framework associated with the policy.
   Defaults to `Sentinel` if not provided. Valid values are `Sentinel` and `Opa`.
* `Query` - (Optional) The OPA query to identify a specific policy rule that
   needs to run within your Rego code. Required for all OPA policies.
* `Policy` - (Required) The actual policy itself.
* `EnforceMode` - (Optional) The enforcement level of the policy. Valid
  values for Sentinel are `Advisory`, `HardMandatory` and `SoftMandatory`. Defaults
  to `SoftMandatory`. Valid values for OPA are `Advisory` and `Mandatory`. Defaults
  to `Advisory`.

## Attributes Reference

* `Id` - The ID of the policy.

## Import

Policies can be imported; use `<ORGANIZATION NAME>/<POLICY ID>` as the
import ID. For example:

```shell
terraform import tfe_policy.test my-org-name/pol-wAs3zYmWAhYK7peR
```

<!-- cache-key: cdktf-0.17.0-pre.15 input-4e8f4f5ed088f5c33fbf8a7f4f936d7ead065966966016c8c512cc7b99e8b6cf -->