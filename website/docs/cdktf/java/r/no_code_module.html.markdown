---
layout: "tfe"
page_title: "Terraform Enterprise: tfe_no_code_module"
description: |-
  Manages no code settings for registry modules
---

# tfe_no_code_module

Creates, updates and destroys no-code module for registry modules.

**NOTE:** This resource is currently in beta and isn't generally
available to all users. It is subject to change or be removed.

## Example Usage

Basic usage:

```java
import software.constructs.*;
import com.hashicorp.cdktf.*;
/*Provider bindings are generated by running cdktf get.
See https://cdk.tf/provider-generation for more details.*/
import gen.providers.tfe.organization.*;
import gen.providers.tfe.registryModule.*;
import gen.providers.tfe.noCodeModule.*;
public class MyConvertedCode extends TerraformStack {
    public MyConvertedCode(Construct scope, String name) {
        super(scope, name);
        Organization tfeOrganizationFoobar = new Organization(this, "foobar", new OrganizationConfig()
                .email("admin@company.com")
                .name("my-org-name")
                );
        RegistryModule tfeRegistryModuleFoobar = new RegistryModule(this, "foobar_1", new RegistryModuleConfig()
                .moduleProvider("my_provider")
                .name("test_module")
                .organization(Token.asString(tfeOrganizationFoobar.getId()))
                );
        /*This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.*/
        tfeRegistryModuleFoobar.overrideLogicalId("foobar");
        NoCodeModule tfeNoCodeModuleFoobar = new NoCodeModule(this, "foobar_2", new NoCodeModuleConfig()
                .organization(Token.asString(tfeOrganizationFoobar.getId()))
                .registryModule(Token.asString(tfeRegistryModuleFoobar.getId()))
                );
        /*This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.*/
        tfeNoCodeModuleFoobar.overrideLogicalId("foobar");
    }
}
```

Creating a no-code module with variable options:

```java
import software.constructs.*;
import com.hashicorp.cdktf.*;
/*Provider bindings are generated by running cdktf get.
See https://cdk.tf/provider-generation for more details.*/
import gen.providers.tfe.organization.*;
import gen.providers.tfe.registryModule.*;
import gen.providers.tfe.noCodeModule.*;
public class MyConvertedCode extends TerraformStack {
    public MyConvertedCode(Construct scope, String name) {
        super(scope, name);
        Organization tfeOrganizationFoobar = new Organization(this, "foobar", new OrganizationConfig()
                .email("admin@company.com")
                .name("my-org-name")
                );
        RegistryModule tfeRegistryModuleFoobar = new RegistryModule(this, "foobar_1", new RegistryModuleConfig()
                .moduleProvider("my_provider")
                .name("test_module")
                .organization(Token.asString(tfeOrganizationFoobar.getId()))
                );
        /*This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.*/
        tfeRegistryModuleFoobar.overrideLogicalId("foobar");
        NoCodeModule tfeNoCodeModuleFoobar = new NoCodeModule(this, "foobar_2", new NoCodeModuleConfig()
                .organization(Token.asString(tfeOrganizationFoobar.getId()))
                .registryModule(Token.asString(tfeRegistryModuleFoobar.getId()))
                .variableOptions(List.of(new NoCodeModuleVariableOptions()
                        .name("ami")
                        .options(List.of("ami-0", "ami-1", "ami-2"))
                        .type("string")
                        , new NoCodeModuleVariableOptions()
                        .name("region")
                        .options(List.of("us-east-1", "us-east-2", "us-west-1"))
                        .type("string")
                        ))
                );
        /*This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.*/
        tfeNoCodeModuleFoobar.overrideLogicalId("foobar");
    }
}
```

## Argument Reference

The following arguments are supported:

- `name` - (Required) Name of the variable set.
- `organization` - (Optional) Name of the organization. If omitted, organization must be defined in the provider config.
- `registryModule` - (Required) The ID of the registry module to associate with the no code module.
- `enabled` - (Required) Whether or not no-code module is enabled for the associated registry module
- `versionPin` - (Optional) The version of the module to pin to.
- `variableOptions` - (Optional) A list of variable options to associate with the no code module.
  - `name` - (Required) The name of the variable option.
  - `type` - (Required) The type of the variable option.
  - `options` - (Required) A list of options for the variable option.

## Attributes Reference

- `id` - The ID of the no code module.

## Import

No-code modules can be imported; use `<NO CODE MODULE ID>` as the import ID. For example:

```shell
terraform import tfe_no_code_module.test nocode-qV9JnKRkmtMa4zcA
```

<!-- cache-key: cdktf-0.17.0-pre.15 input-f45f0a7ff6791ae2440f6cc8504b29ba6ecca4890fe7c716eab795392bfbb79b -->