---
layout: "tfe"
page_title: "Terraform Enterprise: tfe_team_project_access"
description: |-
  Get information on team permissions on a project.
---

# Data Source: tfe_team_project_access

Use this data source to get information about team permissions for a project.

## Example Usage

```typescript
import * as constructs from "constructs";
import * as cdktf from "cdktf";
/*Provider bindings are generated by running cdktf get.
See https://cdk.tf/provider-generation for more details.*/
import * as tfe from "./.gen/providers/tfe";
class MyConvertedCode extends cdktf.TerraformStack {
  constructor(scope: constructs.Construct, name: string) {
    super(scope, name);
    new tfe.dataTfeTeamProjectAccess.DataTfeTeamProjectAccess(this, "test", {
      projectId: "my-project-id",
      teamId: "my-team-id",
    });
  }
}

```

## Argument Reference

The following arguments are supported:

* `teamId` - (Required) ID of the team.
* `projectId` - (Required) ID of the project.

## Attributes Reference

In addition to all arguments above, the following attributes are exported:

* `id` The team project access ID.
* `access` - The type of access granted to the team on the project.

<!-- cache-key: cdktf-0.17.0-pre.15 input-204103613e94c6b9eafe1ca3f90afd99a5659e7479ad472937135a7066629cf3 -->