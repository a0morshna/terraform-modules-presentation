# Terraform Modules Presentation
by Alexandra Morshna

> -----

![Image](https://github.com/a0morshna/terraform-modules-presentation/blob/main/slides/Terraform-Modules.jpg)

> -----

![Image](https://github.com/a0morshna/terraform-modules-presentation/blob/main/slides/Terraform-Modules1.jpg)

> -----

![Image](https://github.com/a0morshna/terraform-modules-presentation/blob/main/slides/Terraform-Modules2.jpg)

> -----

![Image](https://github.com/a0morshna/terraform-modules-presentation/blob/main/slides/Terraform-Modules3.jpg)

> -----

## Module Code:

### Firewall Rule:

```

resource "google_compute_firewall" "allow-http" {
    name       = var.name
    network    = "default"

    allow {
        protocol = "tcp"
        ports    = ["8080","443","22","80","5000"]

    }
    source_ranges = ["0.0.0.0/0"]
}

```

### Machine Instance:

```

resource "google_compute_instance" "http_server" {
  zone         = var.zone
  name         = var.name
  machine_type = var.machine_type

  metadata_startup_script = "sudo apt-get update "

  boot_disk {
    initialize_params {
      image = var.image
    }
  }

  network_interface {
    network = "default"
    access_config {
      // Ephemeral IP
    }
  }
}

```

### Create GCS bucket:

> main.tf
```

resource "google_storage_bucket" "bucket" {
  name                        = var.name
  project                     = var.project_id

  versioning {
    enabled = var.versioning
  }
}

```

> version.tf
```

terraform {
  required_version = ">= 0.13"
  required_providers {

    google = {
      source  = "hashicorp/google"
      version = "~> 3.53"
    }
  }

  provider_meta "google" {
    module_name = "blueprints/terraform/terraform-google-cloud-storage:simple_bucket/v2.1.0"
  }

}

```

> -----

##  Useful Links: 
1. [Link for github solutions. ](https://github.com/GoogleCloudPlatform/solutions-terraform-cloudbuild-gitops/tree/e6bcec81715f52a9a9c7f547926fe4a05c102268)

2. [Link for an article. ](https://www.freecodecamp.org/news/terraform-modules-explained/)

3. [Link for terraform registry. ](https://registry.terraform.io/namespaces/terraform-google-modules)

4. [Link for github some modules examples. ](https://github.com/terraform-google-modules)

 