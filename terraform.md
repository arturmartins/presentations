---
title: Terraform

---

# Terraform

Follow along: http://robertdebock.nl/

<img src="https://api.qrserver.com/v1/create-qr-code/?size=350x350&data=http://robertdebock.nl/presentations/terraform/"/>

---

# What

Infrastructure as code

---

# Why

- Much quicker
- Repeatable
- Versionable & history
- Easy collaboration

---

# Examples

Mostly stolen from the [Terraform documentation](https://www.terraform.io/docs/providers/do/).

---

# Define

```hsl
resource "digitalocean_droplet" "web_1" {
  image  = "ubuntu-18-04-x64"
  name   = "web_1"
  region = "ams3"
  size   = "s-1vcpu-1gb"
}
```

----

# Pass data

```hsl
resource "digitalocean_loadbalancer" "public" {
  name   = "loadbalancer-1"
  region = "ams3"

  forwarding_rule {
    entry_port     = 80
    entry_protocol = "http"

    target_port     = 80
    target_protocol = "http"
  }

  healthcheck {
    port     = 22
    protocol = "tcp"
  }

  droplet_ids = [digitalocean_droplet.web_1.id]
}
```

---

# Dry-run

```bash
terraform plan
```

---

# Apply!

```bash
terraform apply
```

---

# Save money

```bash
terraform destroy
```