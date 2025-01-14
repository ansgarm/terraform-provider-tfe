---
layout: "tfe"
page_title: "Terraform Enterprise: tfe_notification_configuration"
description: |-
  Manages notifications configurations.
---

# tfe_notification_configuration

Terraform Cloud can be configured to send notifications for run state transitions.
Notification configurations allow you to specify a URL, destination type, and what events will trigger the notification.
Each workspace can have up to 20 notification configurations, and they apply to all runs for that workspace.


## Example Usage

Basic usage:

```typescript
import * as constructs from "constructs";
import * as cdktf from "cdktf";
/*Provider bindings are generated by running cdktf get.
See https://cdk.tf/provider-generation for more details.*/
import * as tfe from "./.gen/providers/tfe";
class MyConvertedCode extends cdktf.TerraformStack {
  constructor(scope: constructs.Construct, name: string) {
    super(scope, name);
    const tfeOrganizationTest = new tfe.organization.Organization(
      this,
      "test",
      {
        email: "admin@company.com",
        name: "my-org-name",
      }
    );
    const tfeWorkspaceTest = new tfe.workspace.Workspace(this, "test_1", {
      name: "my-workspace-name",
      organization: cdktf.Token.asString(tfeOrganizationTest.id),
    });
    /*This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.*/
    tfeWorkspaceTest.overrideLogicalId("test");
    const tfeNotificationConfigurationTest =
      new tfe.notificationConfiguration.NotificationConfiguration(
        this,
        "test_2",
        {
          destinationType: "generic",
          enabled: true,
          name: "my-test-notification-configuration",
          triggers: ["run:created", "run:planning", "run:errored"],
          url: "https://example.com",
          workspaceId: cdktf.Token.asString(tfeWorkspaceTest.id),
        }
      );
    /*This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.*/
    tfeNotificationConfigurationTest.overrideLogicalId("test");
  }
}

```

With `destinationType` of `email`:

```typescript
import * as constructs from "constructs";
import * as cdktf from "cdktf";
/*Provider bindings are generated by running cdktf get.
See https://cdk.tf/provider-generation for more details.*/
import * as tfe from "./.gen/providers/tfe";
class MyConvertedCode extends cdktf.TerraformStack {
  constructor(scope: constructs.Construct, name: string) {
    super(scope, name);
    const tfeOrganizationTest = new tfe.organization.Organization(
      this,
      "test",
      {
        email: "admin@company.com",
        name: "my-org-name",
      }
    );
    const tfeOrganizationMembershipTest =
      new tfe.organizationMembership.OrganizationMembership(this, "test_1", {
        email: "test.member@company.com",
        organization: "my-org-name",
      });
    /*This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.*/
    tfeOrganizationMembershipTest.overrideLogicalId("test");
    const tfeWorkspaceTest = new tfe.workspace.Workspace(this, "test_2", {
      name: "my-workspace-name",
      organization: cdktf.Token.asString(tfeOrganizationTest.id),
    });
    /*This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.*/
    tfeWorkspaceTest.overrideLogicalId("test");
    const tfeNotificationConfigurationTest =
      new tfe.notificationConfiguration.NotificationConfiguration(
        this,
        "test_3",
        {
          destinationType: "email",
          emailUserIds: [
            cdktf.Token.asString(tfeOrganizationMembershipTest.userId),
          ],
          enabled: true,
          name: "my-test-email-notification-configuration",
          triggers: ["run:created", "run:planning", "run:errored"],
          workspaceId: cdktf.Token.asString(tfeWorkspaceTest.id),
        }
      );
    /*This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.*/
    tfeNotificationConfigurationTest.overrideLogicalId("test");
  }
}

```

(**TFE only**) With `destinationType` of `email`, using `emailAddresses` list and `emailUsers`:

```typescript
import * as constructs from "constructs";
import * as cdktf from "cdktf";
/*Provider bindings are generated by running cdktf get.
See https://cdk.tf/provider-generation for more details.*/
import * as tfe from "./.gen/providers/tfe";
class MyConvertedCode extends cdktf.TerraformStack {
  constructor(scope: constructs.Construct, name: string) {
    super(scope, name);
    const tfeOrganizationTest = new tfe.organization.Organization(
      this,
      "test",
      {
        email: "admin@company.com",
        name: "my-org-name",
      }
    );
    const tfeOrganizationMembershipTest =
      new tfe.organizationMembership.OrganizationMembership(this, "test_1", {
        email: "test.member@company.com",
        organization: "my-org-name",
      });
    /*This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.*/
    tfeOrganizationMembershipTest.overrideLogicalId("test");
    const tfeWorkspaceTest = new tfe.workspace.Workspace(this, "test_2", {
      name: "my-workspace-name",
      organization: cdktf.Token.asString(tfeOrganizationTest.id),
    });
    /*This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.*/
    tfeWorkspaceTest.overrideLogicalId("test");
    const tfeNotificationConfigurationTest =
      new tfe.notificationConfiguration.NotificationConfiguration(
        this,
        "test_3",
        {
          destinationType: "email",
          emailAddresses: [
            "user1@company.com",
            "user2@company.com",
            "user3@company.com",
          ],
          emailUserIds: [
            cdktf.Token.asString(tfeOrganizationMembershipTest.userId),
          ],
          enabled: true,
          name: "my-test-email-notification-configuration",
          triggers: ["run:created", "run:planning", "run:errored"],
          workspaceId: cdktf.Token.asString(tfeWorkspaceTest.id),
        }
      );
    /*This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.*/
    tfeNotificationConfigurationTest.overrideLogicalId("test");
  }
}

```

## Argument Reference

The following arguments are supported:

* `name` - (Required) Name of the notification configuration.
* `destinationType` - (Required) The type of notification configuration payload to send.
  Valid values are:
  * `generic`
  * `email` available in Terraform Cloud or Terraform Enterprise v202005-1 or later
  * `slack`
  * `microsoftTeams` available in Terraform Cloud or Terraform Enterprise v202206-1 or later
* `emailAddresses` - (Optional) **TFE only** A list of email addresses. This value
  _must not_ be provided if `destinationType` is `generic`, `microsoftTeams`, or `slack`.
* `emailUserIds` - (Optional) A list of user IDs. This value _must not_ be provided
  if `destinationType` is `generic`, `microsoftTeams`, or `slack`.
* `enabled` - (Optional) Whether the notification configuration should be enabled or not.
  Disabled configurations will not send any notifications. Defaults to `false`.
* `token` - (Optional) A write-only secure token for the notification configuration, which can
  be used by the receiving server to verify request authenticity when configured for notification
  configurations with a destination type of `generic`. Defaults to `null`.
  This value _must not_ be provided if `destinationType` is `email`, `microsoftTeams`, or `slack`.
* `triggers` - (Optional) The array of triggers for which this notification configuration will
  send notifications. Valid values are `run:created`, `run:planning`, `run:needsAttention`, `run:applying`
  `run:completed`, `run:errored`, `assessment:drifted`, or `assessment:failed`.
  If omitted, no notification triggers are configured.
* `url` - (Required if `destinationType` is `generic`, `microsoftTeams`, or `slack`) The HTTP or HTTPS URL of the notification
  configuration where notification requests will be made. This value _must not_ be provided if `destinationType`
  is `email`.
* `workspaceId` - (Required) The id of the workspace that owns the notification configuration.

## Attributes Reference

* `id` - The ID of the notification configuration.

## Import

Notification configurations can be imported; use `<NOTIFICATION CONFIGURATION ID>` as the import ID. For example:

```shell
terraform import tfe_notification_configuration.test nc-qV9JnKRkmtMa4zcA
```

<!-- cache-key: cdktf-0.17.0-pre.15 input-3b80dcc8db0024281201a017d39c3703fde99f0f06d127f4149f1f1df6dc15d7 -->