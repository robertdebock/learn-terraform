# Sentinel

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|60 minutes   |A computer with Sentinel installed, terraform knowledge. |

Goal: Understand what Sentinel is and how to write rules.

## Explanation

Sentinel is a HashiCorp tool that can enforce policies (or rules). Sentinel ties into Terraform Enterprise and Terraform Cloud, both commercial producs.

```
+--- code ---+    +--- Terraform -------+    +----------+
| - main.tf  | -> | cloud or enterprise | -> | Sentinel | -> Provider(s).
+------------+    +---------------------+    +----------+
      ^                   ^
     \o/                 \o/
  DEV |               SEC |
     / \                 / \
```

Another way to explain the order is this list:

1. main.tf - Terraform code.
2. plan
3. Sentinel - Sentinel inspects the plan.
4. apply

The intent of Sentinel is that a security person (SEC) write a policy (rules) and the developers (DEV) write terraform code. After Terraform has rendered a plan, Sentinel checks for violations and continues execution when all rules are passed.

There are alternative methods, but none are as convenient or secure as Sentinel:

### Azure policies

Although very complete in features, this only applies to Azure, plus if a policy is violated, Terraform "errors out" instead of a nice method. Feedback is quite late.

### Terraform modules

You can set standards in Terraform modules, but users do not _have_ to use modules, so this is not a water tight solution.

## Demo

After installing Sentinel, try these commands on the Sentinel CLI. The Sentinel CLI is used to develop, troubleshoot and test rules.

Let's experiment a bit with a very simple policy.

Write a policy:

```bash
cat << EOF > region.policy
param region

main = rule {
  region in ["ams1", "ams2", "ams3"]
}
EOF
```

Write a passing test:

```bash
mkdir -p test/region
echo << EOF > test/region/pass-ams1.hcl
param "region" {
  value = "ams1"
}
EOF
```

Write a failing test:

```bash
echo << EOF > test/region/fail-ams4.hcl
param "region" {
  value = "ams4"
}

test {
  rules = {
    main = false
  }
}
EOF
```

Now try the policy

```bash
sentinel test
```

You should see this:

```text
PASS - region.sentinel
  PASS - test/region/fail-ams4.hcl
  PASS - test/region/pass-ams1.hcl
```

That was the _debug_ or _troubleshoot_ mode, using sentinel CLI.

Now lets have a look at a [realistic example](https://github.com/robertdebock/sentinel-azure-policies).

## Assignment

If you don't have or can't have Sentinel installed, try the [Sentinel playground](https://play.sentinelproject.io/)

- [ ] Install [HashiCorp Sentinel](https://docs.hashicorp.com/sentinel/downloads).
- [ ] Clone this [example repository](https://github.com/robertdebock/sentinel-azure-policies).
- [ ] Find the `mandatory_tags` in `mandatory_tags.sentinel`.
- [ ] Expend the tags with `costcenter`.
- [ ] (Manually) add the tag `costcenter` to `test/mandatory_tags/mock-tfplan-pass.sentinel`.
- [ ] Run `sentinel test`.

## Questions:

1. Can you build Sentinel into a pipeline yourself, without using Terraform Enterprise or Terraform Cloud?

## Sources

- [HashiCorp on Sentinel](https://www.hashicorp.com/sentinel)
- [Sentinel examples](https://www.terraform.io/docs/cloud/sentinel/examples.html)
- [Writing Sentinel policies](https://docs.hashicorp.com/sentinel/writing)
