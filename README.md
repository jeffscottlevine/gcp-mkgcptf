mktf(1) -- Launch a GCP Ubuntu instance and set up Terraform
=============================================

## SYNOPSIS

    mktf
         -x, --prefix NEW_RESOURCE_PREFIX (required)
         -p, --project PROJECT_ID         (required)
         -z, --zone ZONE                  (reguired)
         -n, --network NETWORK            (required)
        [-t, --machine-type MACHINE_TYPE] (optional)
        [-h, --help]                      (optional)
        [-s, --random-suffix]             (optional)

## DESCRIPTION

The mktf command creates an Ubuntu instance and installs Terraform.
The goal of this command is to make getting started with Terraform easier.

More specifically, mktf performs the tasks listed below.

1. Optionally creates a random suffix used for resource names. and creates Terraform scripts for the Google Cloud provider,
2. Creates a service account that will be used when creating the instance.
3. Creates a Google Cloud Storage bucket for holding Terraform state.
4. Creates a Google Cloud Ubuntu instance.
5. Installs Terraform on the instances.
6. Creates Terraform code files on the instance in /usr/local/etc/tf for the backend state, providers, regional providers, and so forth.
7. Modifies /etc/bash.bashrc on the instance to notify a user upon login of the location of the Terraform files.
8. Modifies /etc/bash.bashrc on the instance to set up .virmrc if it does not already exist.

## OPTIONS

     -x, --prefix NEW_RESOURCE_PREFIX (required)
        This option specifiesthe prefix for names of the resources created by mygcptf.
        This includes the service account, the GCS bucket for Terraform state, and the instance.
        This does not include resources created by Terraform.

     -p, --project PROJECT_ID         (required)
        This option specifies the exiting project ID in which the resources will be created.

     -z, --zone ZONE                  (reguired)
        This option specifies the zone in which the instance will be created.

     -n, --network NETWORK            (required)
        This option specifies the name of an existing network to which the interface
        of the instance will be attached.  This has only been tested for networks
        that have been created with automatic subnets.

    [-t, --machine-type MACHINE_TYPE] (optional)
        This option specifies the machine type of the Ubuntu instance.  The default is
        e2-micro.

    [-h, --help]                      (optional)
        This option displays a help message

    [-s, --random-suffix]             (optional)
        This option appends a random suffix to each of the resources created by mktf.
        This does not include the resources created within Terraform.

## SECURITY NOTES

The service account that is created to launch the Terraform instance contains the permissions listed below.

* roles/owner

* roles/resourcemanager.projectIamAdmin

* roles/iam.serviceAccountUser

## EXAMPLES

    ./mktf -x my-instance -p my-project -n my-network -z us-west2-b -s

## COPYRIGHT

mktf is copyright (c) 2020, Jeffrey S. Levine. Released under the Apache
license.
