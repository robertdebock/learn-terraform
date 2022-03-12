# Build infrastructure SQL database

|expected time|requirements|
|-------------|------------|
| 60 minutes  | a computer |

Goal: Learn how to create GCP SQL server and instance resources using Terraform.

## Explanation

There are many GCP resources available, lets setup a managed MySQL instance.

## Howto

Using the [sql_database_instance](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/sql_database_instance) and [sql_database](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/sql_database) we're going to create a managed MySQL database.

## Demo

[Example code](https://github.com/robertdebock/terraform-gcp-database)

## Assignment

### Easy

Use the [example code](https://github.com/robertdebock/terraform-gcp-database) and use the settings:

- Set `database_version` to "MYSQL_8_0" for the `google_sql_database.default`.
- Add another database on `google_sql_database_instance.default`.
- Set the `charset` to "koi8u".

### Hard

Use the [documentation](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/sql_database) to create a database with these characteristics:

- `charset` = "koi8u".
- `collation` = "utf32_general_ci"

Add variables for `charset` and `collation`.
Add validation on the variables so that you can only pick supported values.

Add a [user](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/sql_user) to the database instance so you test MySQL later.

### Testing things

Most machines have `telnet` installed: `telnet YOUR_FQDN 3306`.
Some machines have `mysql` installed: `mysql -u YOUR_USER -p -h YOUR_FQDN`.

## View the results

| [GCP](https://console.cloud.google.com/sql/instances) |

## Questions

1. What are valid choices for `database_version`?
2. What happens if I change the `database_version` to this resource?
3. Could I make a virtual machine and install MySQL myself?
4. Will this work: 1. Create the db, `deletion_protection=true`. 2. Change `deletion_protection` to `false`, 3 Run `terraform destroy`.
