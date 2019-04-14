# terraform-provider-awsjr
Terraform provider adding additional functionality to the AWS codepipeline provisioner.

# Setup
Either download the accompanying binary or compile from source.  Then install the compiled plugin 
according to Terraform docs [here](https://www.terraform.io/docs/extend/how-terraform-works.html#terraform-plugins).

# Usage
Configure the provider as described [here](https://www.terraform.io/docs/configuration-0-11/providers.html).

Example:
```bash
provider "awsjr" {
  access_key = "XXXXX"
  secret_key = "XXXXX"
  region = "us-west-2"
}
```

The resource awsjr_code_pipeline can now be used in the exact same manner as [aws_codepipeline](https://www.terraform.io/docs/providers/aws/r/codepipeline.html), with
the additional ability to conditionally exclude a stage from the pipeline using the _exclude_ property.

Example:
```bash
resource "awsjr_code_pipeline" "main" {
  ...

  stage {
    name = "DeploySIT"
    exclude = "${var.exclude-sit}" // true|false
    ...
  }
}
```

> Note:  An excluded stage is still created in the state file in order to retain properties.  It just additionally
contains an _exclude_ property that excludes it from the pipeline.
