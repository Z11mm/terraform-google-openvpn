# Terraform OpenVPN GCP
A terraform module to setup OpenVPN on GCP


## Usage

```hcl
module "openvpn" {
  source     = "../modules/terraform-openvpn-gcp"
  region     = var.region
  project_id = var.project_id
  network    = module.vpc.network
  subnetwork = module.vpc.public_subnetwork
  output_dir = "${path.module}/openvpn"
  users      = ["bob", "alice"]
}

```

## Doc generation

Code formatting and documentation for variables and outputs is generated using [pre-commit-terraform hooks](https://github.com/antonbabenko/pre-commit-terraform) which uses [terraform-docs](https://github.com/segmentio/terraform-docs).


And install `terraform-docs` with
```bash
go get github.com/segmentio/terraform-docs
```
or
```bash
brew install terraform-docs.
```

## Contributing

Report issues/questions/feature requests on in the issues section.

Full contributing guidelines are covered [here](CONTRIBUTING.md).

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| terraform | >= 0.14 |

## Providers

| Name | Version |
|------|---------|
| google | n/a |
| local | n/a |
| null | n/a |
| random | n/a |
| tls | n/a |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| disk\_size\_gb | n/a | `string` | `"30"` | no |
| labels | Labels, provided as a map | `map` | `{}` | no |
| machine\_type | Machine type to create, e.g. n1-standard-1 | `string` | `"n1-standard-1"` | no |
| metadata | Metadata, provided as a map | `map` | `{}` | no |
| network | The name or self\_link of the network to attach this interface to. Use network attribute for Legacy or Auto subnetted networks and subnetwork for custom subnetted networks. | `string` | `"default"` | no |
| network\_tier | Network network\_tier | `string` | `"STANDARD"` | no |
| output\_dir | Folder to store all user openvpn details | `string` | `"openvpn"` | no |
| prefix | prefix to use for all resource | `string` | `""` | no |
| project\_id | The GCP Project ID | `any` | `null` | no |
| region | The GCP Project Region | `any` | `null` | no |
| remote\_user | The user to operate as on the VM. SSH Key is generated for this user | `string` | `"ubuntu"` | no |
| route\_only\_private\_ips | Routes only private IPs through the VPN (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16) | `bool` | `false` | no |
| service\_account | Service account to attach to the instance. See https://www.terraform.io/docs/providers/google/r/compute_instance_template.html#service_account. | <pre>object({<br>    email  = string,<br>    scopes = set(string)<br>  })</pre> | <pre>{<br>  "email": null,<br>  "scopes": []<br>}</pre> | no |
| source\_image | The source image for the image family. If not specified, terraform will try to create a new instance template anytime an update for an image familty is release | `string` | `"ubuntu-2004-focal-v20210415"` | no |
| source\_image\_family | n/a | `string` | `"ubuntu-2004-lts"` | no |
| source\_image\_project | n/a | `string` | `"ubuntu-os-cloud"` | no |
| subnetwork | The name of the subnetwork to attach this interface to. The subnetwork must exist in the same region this instance will be created in. Either network or subnetwork must be provided. | `any` | `null` | no |
| tags | network tags to attach to the instance | `list` | `[]` | no |
| users | list of user to create | `list(string)` | `[]` | no |
| zone | The GCP Zone to deploy VPN Compute instance to | `any` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| users | Created Users |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
