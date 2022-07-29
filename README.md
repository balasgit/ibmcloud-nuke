# ibmcloud-nuke

Remove all resources from an IBM Cloud account.

## Install the IBM Cloud CLI & plugins

In order to use this script you must have installed the IBM Cloud CLI. If you need to do that run the following:
```
curl -fsSL https://clis.cloud.ibm.com/install/linux | sh
```

Once IBM Cloud CLI installed,  install several plugins for the script to execute successfully.
install them run the following commands:

```
ibmcloud plugin install -f code-engine
```

```
ibmcloud plugin install -f container-registry
```

```
ibmcloud plugin install -f container-service
```

```
ibmcloud plugin install -f cloud-functions
```

```
ibmcloud plugin install -f infrastructure-service
```

```
ibmcloud plugin install -f schematics
```

```
ibmcloud plugin install cloud-object-storage
```

```
ibmcloud plugin install vpc-infrastructure
```

```
ibmcloud target -g <Resource-Group>
```

*** Use 'ibmcloud plugin repo-plugins -r 'IBM Cloud'' to list plugins available in the repo ***

```
ibmcloud plugin repo-plugins -r 'IBM Cloud'
```

Getting plug-ins from repository 'IBM Cloud'...

Repository: IBM Cloud
Status             Name                                          Versions                       Description   
Update Available   cloud-object-storage                          1.5.0, 1.4.0, 1.3.1...         Manage Cloud Object Storage service   
Update Available   observe-service                               1.0.82, 1.0.61, 1.0.54...      Manage logging and monitoring configurations for IBM Cloud Kubernetes Service clusters   
Not Installed      cbr                                           1.0.0                          Manage Context Based Restrictions   
Not Installed      qiskit-runtime[qr]                            0.1.5                          [Beta] Manage Qiskit Runtime   
Not Installed      cloud-internet-services[cis]                  1.14.4, 1.14.2, 1.14.1...      Manage Cloud Internet Service   
Not Installed      dbaas-cli[dbaas]                              2.1.7, 2.1.6, 2.1.2...         Manage Hyper Protect DBaaS clusters   
Not Installed      cloud-databases[cdb]                          0.11.0, 0.10.10, 0.10.9...     Manage Cloud databases   
Not Installed      key-protect[kp]                               0.6.11, 0.6.10, 0.6.9...       Manage encryption keys on IBM Cloud   
Not Installed      doi[doi]                                      0.3.8, 0.3.7, 0.3.5...         Integrate with DevOps Insights service   
Not Installed      tke                                           1.3.0, 1.2.3, 1.1.4...         Manage the master key of Cloud HSMs from Hyper Protect Crypto service   
Not Installed      analytics-engine                              1.0.186, 1.0.181, 1.0.177...   Manage Analytics Engine service   
Not Installed      event-streams                                 2.3.2, 2.3.1, 2.3.0...         Manage Event Streams service   
Not Installed      power-iaas[pi]                                0.3.17, 0.3.13, 0.3.12...      Manage IBM Cloud Power Virtual Server service   
Not Installed      hpnet                                         1.0.2, 1.0.1                   Manage Hyper Protect Secure Network   
Not Installed      dvaas[watson-query]                           1.0.2                          Manage data virtualization as a service   
Not Installed      cloud-dns-services[dns]                       0.7.0, 0.6.2, 0.5.3...         Manage IBM Cloud Dns Service   
Not Installed      dl-cli                                        0.4.11, 0.4.10, 0.4.9...       Manage Direct Link   
Not Installed      watson                                        0.0.11, 0.0.10, 0.0.9...       Manage Watson services   
Not Installed      catalogs-management                           2.1.20, 2.1.19, 2.1.18...      Manage personal catalogs and offerings   
Not Installed      analytics-engine-v3[ae-v3]                    1.0.9, 1.0.5, 1.0.0            Manage serverless Spark instances and run applications   
Not Installed      hpcs                                          0.0.1                          Manage Hyper Protect Crypto Services Instances   
Not Installed      event-notifications[en/event-notifications]   0.1.1, 0.1.0, 0.0.8...         IBM Cloud Event Notifications.   
Not Installed      hpvs                                          1.4.19, 1.4.17, 1.4.15...      Manage Hyper Protect Virtual Server service   
Not Installed      push-notifications[push]                      1.0.5, 1.0.4, 1.0.3...         [Deprecated] Manage IBM Cloud Push Notifications service.   
Not Installed      secrets-manager[sm]                           0.1.21, 0.1.20, 0.1.19...      Manage IBM Cloud Secrets Manager secrets and secret groups.   
Not Installed      app-configuration[ac]                         1.0.9, 1.0.8, 1.0.7...         Interact with IBM Cloud App Configuration service instance   
Not Installed      monitoring                                    0.2.12, 0.2.9, 0.2.8...        Manage IBM Cloud monitoring   
Not Installed      logging                                       0.0.8, 0.0.7, 0.0.6...         Manage IBM Cloud logging   
Not Installed      cloudant[cl]                                  0.0.5, 0.0.4, 0.0.3            Manage Cloudant service   
Not Installed      hpcs-cert-mgr[hpcs-cert-mgr]                  1.0.0                          Manage the client certificates for IBM Cloud Hyper Protect Crypto Services   
Not Installed      atracker[at]                                  0.2.12, 0.1.13, 0.1.7...       Manage IBM Cloud Activity Tracker   
Not Installed      tg-cli[tg]                                    0.8.2, 0.7.1, 0.6.1...         Manage Transit Gateway service   
Not Installed      cra[cra]                                      0.1.22, 0.1.21, 0.1.20...      Integrate with Code Risk Analyzer   
Installed          code-engine                                   1.38.1, 1.38.0, 1.37.0...      Manage Code Engine components   
Installed          schematics[sch]                               1.12.1, 1.12.0, 1.11.1...      Managing IBM Cloud resources with Terraform   
Installed          vpc-infrastructure[infrastructure-service]    5.0.1, 5.0.0, 4.2.0...         Manage Virtual Private Cloud infrastructure service   
Installed          cloud-functions[wsk/functions/fn]             1.0.59, 1.0.58, 1.0.56...      Manage Cloud Functions   
Installed          container-service[kubernetes-service]         1.0.431, 1.0.430, 1.0.426...   Manage IBM Cloud Kubernetes Service clusters   
Installed          container-registry                            0.1.571, 0.1.566, 0.1.560...   Manage IBM Cloud Container Registry content and configuration. 

## Caution!

Be aware that *IBM Cloud Nuke* is a very destructive tool, be very careful while using it. Otherwise you might delete production data. **Do NOT run this application on an IBM Cloud account where you cannot afford to lose all resources.**

Some safety precautions have been put in place.

1. By default *IBM Cloud Nuke* only lists all nukeable resources. You need to add `-n` flag to actually delete resources.
1. A config file can be used to specify names and IDs of resources to skip over.

The project itself is just a shell script that is required be run by an authenticated IBM Cloud user. The shell script will find and delete the following resources:

* Kubernetes and OpenShift clusters
* Container Registry namespaces
* Applications (Cloud Foundry or Stater Kits)
* Services (like Cloudant, Watson services, Object Storage (and their underlying buckets), etc)
* Classic Baremetal servers
* Classic Virtual servers
* Code Engine projects (and their underlying jobs)
* Cloud Functions Namespaces (and their underlying actions)
* API keys (excluding ones requires for managing Kubernetes clusters)
* Satellite locations
* Gen2 VPCs
* VPC Subnet
* VPC Loadbalancer
  

## CLI options

```bash
main.sh [-n] [-c <path-to-config-file>]
```

* `-n`: Specify "no dry run". Resources will be deleted.
* `-c`: Specify a config file for IDs/names of resources to be saved from deletion. The tool will automatically look for a file called `ibmcloud-nuke` in the local directory.

## Using the CLI

1. Clone the repo.

   ```bash
   git clone
   ```

2. Log into IBM Cloud.

   ```bash
   ibmcloud login --sso
   ```
3. Switch to Resource Group where you want to list and delete resources

   ```bash
   ibmcloud target -g <resource-group>
   ```
4. Switch to region where you want to list and delete resources

   ```bash
   ibmcloud target -r <region us-south,eu-gb>
   ```

4. Run the CLI.

   Perform a dry run:

   ```bash
   ./main.sh
   ```

   Delete all resources (will skip over any resorces found in `.ibmcloud-nuke`):

   ```bash
   ./main.sh -n
   ```

   Delete all resources but skip resources list in `myfile.txt`:

   ```bash
   ./main.sh -c myfile.txt
   ```

## TODO

1. The project needs support for deleting the following types of resources:

   * [Schematics Workspaces](https://cloud.ibm.com/docs/schematics?topic=schematics-schematics-cli-reference#schematics-workspace-delete)

