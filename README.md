
# grace-tf-module-budget

Terraform module for AWS budgets that is used in GRACE. This module is a supporting module that is required for [grace-core](https://github.com/GSA/grace-core) but may be used independently by other projects if required.

## Contributors

This module was created by the GRACE DevSecOps team. The master branch is maintained by this same group of contributors. For information on contributing, see [CONTRIBUTING.md](https://github.com/gsa/grace-tf-module/budget/CONTRIBUTING.md)

## License

The license for this software is documented in [LICENSE.md](https://github.com/gsa/grace-tf-module-budget/LICENSE.md)

## Instructions

Use Terraform to call this module in your code. Below is an example to create a budget notification for a new GRACE tenant named "tenant1":

    ```hcl
    module "tenant_1_budget" {
        source = "github.com/gsa/grace-tf-module-budget/terraform/modules/budget"

        name = "tenant1"

        budget_notifications = [
            {
                protocol = "email"
                endpoint = "tenant.owner+tenant1alerts@gsa.gov"
            },
        ]

        account_ids = [
            "${module.tenant_1_prod.account_id}",
            "${module.tenant_1_staging.account_id}",
            "${module.tenant_1_dev.account_id}",
            "${module.tenant_1_mgmt.account_id}",
            ]
        }
    ```

### Required variables

You must supply the following variables to the module:

* name: a simple name that will be used for displaying the resulting budget notification within AWS.
* budget_notifications: A list of protocol and endpoints to add to the SNS topic that will be created.
* account_ids: List of subaccount IDs that will be associated with the budget notification.

### Authors

[Jason G. Miller](mailto:jasong.miller@gsa.gov)

#### Developer / Company / Employer

General Services Administration Information Technology (GSAIT)
