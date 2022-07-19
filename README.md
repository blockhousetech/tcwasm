# tcwasm

In this repository, we demonstrate the use of Transparency Center (TC) in confidential program analysis. More specifically, we show how to set up a web-assembly (WASM) analyzer in transparency center, and then use it for some simple program analysis tasks.

### Quick Start

In this section, we go through basic steps for setting up and runing Seraph WASM analyzer in Google's Confidential Computing platform, a cloud-based trusted execution envrionment (TEE) on which Transparency Center can build. If you are not familiar with TEE or Confidential Computing, please refer to [Confidential Computing  |  Google Cloud](https://cloud.google.com/confidential-computing) for more information.

Before we start, please make sure that you already have an Google account, set up a Google Cloud project, enable billing for your project, and have Compute Engine API enabled. If that's not the case, or if you are not sure, please refer to [Create a Confidential VM instance in the Cloud console | Google Cloud](https://cloud.google.com/compute/confidential-vm/docs/create-confidential-vm-instance) for more instructions.

##### Step 1: Set Up Confidential Computing Instance

To set up a confidential computing instance, just follow the typical process of creating new VM instances in Google Compute Engine Console. More specifically, visit Google Cloud Console ([https://console.cloud.google.com](https://console.cloud.google.com)), select `Compute Engine` in the product navigation menu, choose `VM instances` page, and then click `CREATE INSTANCE` button at the top of the page.

![Create VM Instance](./images/create-instance.png)

In the following `Create an instance` page, we then click button to `ENABLE` Confidential VM service. Please note that by enabling Confidential VM service, the system will automatically change some of our VM settings, e.g., `Machine type` and `Boot disk image`. Just leave these settings as default, and click `CREATE` at the bottom of page to start creating Confidential VM instance. Wait for this process to finish, it may take several minutes.

![Enable Confidential Service](./images/confidential-vm.png)

To validate if Confidential Computing service is enabled for our newly created VM, click instance name (e.g., "instance-1") to see VM instances `DETAILS`, then click `Cloud Logging` to see VM logs. In the logging results panel, find and check `sevLaunchAttestationReportEvent` for integrity report. If that's the case, we can be sure that our VM instance is indeed protected by Confidential Computing service.

![Attestation Report](./images/attestation.png)

For more detailed instructions, please refer to [Validating instances using Cloud Monitoring | Confidential VM | Google Cloud](https://cloud.google.com/compute/confidential-vm/docs/monitoring).

##### Step 2: Pull and Run Seraph WASM Analyzer

Now that we have set up a Confidential Computing VM instance, it's time to install and run Seraph for WASM program analysis. The simplest way to do this is to leverage the prebuilt Seraph Docker image ([add link here]()), which we will show you in this guide.

To run Docker image, we first need to set up a Docker Engine envrionment in the VM:

```bash
# The following scripts assumes an Ubuntu 18.04 bionic operating system,
# and requires a stable SSH connection to the VM, if that is not the case,
# refer to https://cloud.google.com/compute/docs/instances/connecting-to-instance
# for more information.

# (1) Set up apt package repository
$ sudo apt-get update
$ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
$ sudo mkdir -p /etc/apt/keyrings
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# (2) Install docker engine from repository
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

If there are any problem with Docker Engine installation, please refer to [Install Docker Engine on Ubuntu | Docker Documentation](https://docs.docker.com/engine/install/ubuntu/).

Then, pull and run Seraph Docker image, test if installation succeeds:

```bash
# The following scripts assumes an Ubuntu 18.04 bionic operating system,
# and requires a stable SSH connection to the VM, if that is not the case,
# refer to https://cloud.google.com/compute/docs/instances/connecting-to-instance
# for more information.

$ 
```

##### Step 3: Experiment with Some Analysis Tasks

### What's Next?

In the above section, while demonstrating basic steps for spining up program analyzer in Transparency Center, we intentionally omit some technical details, e.g., the process to establish trust between multiple conterparties. This is intended to make this guide smoother and more comprehensible. For readers curious about the underlying challenges and our approaches, please refer to our coming technical paper "Trusted And Confidential Program Analysis" for more details.