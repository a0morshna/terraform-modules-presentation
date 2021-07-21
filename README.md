# Terraform Modules Presentation
by Alexandra Morshna

> -----

![Image](https://github.com/a0morshna/terraform-modules-presentation/blob/main/slides/Terraform-Modules.jpg)

> -----

![Image](https://github.com/a0morshna/terraform-modules-presentation/blob/main/slides/Terraform-Modules(1).jpg)

> -----

![Image](https://github.com/a0morshna/terraform-modules-presentation/blob/main/slides/Terraform-Modules(2).jpg)

> -----

![Image](https://github.com/a0morshna/terraform-modules-presentation/blob/main/slides/Terraform-Modules(3).jpg)

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

> -----

##  Useful Links: 
1. [Link for github solutions. ](https://github.com/GoogleCloudPlatform/solutions-terraform-cloudbuild-gitops/tree/e6bcec81715f52a9a9c7f547926fe4a05c102268)

2. [Link for an article. ](https://www.freecodecamp.org/news/terraform-modules-explained/)

3. [Link for terraform registry. ](https://registry.terraform.io/namespaces/terraform-google-modules)

4. [Link for github some modules examples. ](https://github.com/terraform-google-modules)

 