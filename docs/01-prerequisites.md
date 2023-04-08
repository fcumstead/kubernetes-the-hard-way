# Prerequisites

## Google Cloud Platform

This tutorial leverages the [Google Cloud Platform](https://cloud.google.com/) to streamline provisioning of the compute infrastructure required to bootstrap a Kubernetes cluster from the ground up. [Sign up](https://cloud.google.com/free/) for $300 in free credits.

[Estimated cost](https://cloud.google.com/products/calculator#id=873932bc-0840-4176-b0fa-a8cfd4ca61ae) to run this tutorial: $0.23 per hour ($5.50 per day).

> The compute resources required for this tutorial exceed the Google Cloud Platform free tier.

## Google Cloud Platform SDK

### Install the Google Cloud SDK

Follow the Google Cloud SDK [documentation](https://cloud.google.com/sdk/) to install and configure the `gcloud` command line utility.

Verify the Google Cloud SDK version is 425.0.0 or higher:

```
gcloud version
```

### Set a Default Compute Region and Zone

This tutorial assumes a default compute region and zone have been configured.

If you are using the `gcloud` command-line tool for the first time `init` is the easiest way to do this:

```
gcloud init
```

Create a new gcloud configuration for your project on the machine you will use to access it.

```
gcloud config configurations create [NAME]
```

Set the Google Cloud project name to the active gcloud configuration.

```
gcloud config set project [PROJECT-NAME]
```

Then be sure to authorize the Google account that has some type of access/ownership of this project.:

```
gcloud auth login
```

Then se the below command if you are developing code in something like a local development environment and it would be easier to use user credentials than setup a service account.:

```
gcloud auth application-default login
```

Next set a default compute region and compute zone:

```
gcloud config set compute/region us-east1
```

Set a default compute zone:

```
gcloud config set compute/zone us-east1-c
```

> **NOTE**: Use the `gcloud compute zones list` command to view additional regions and zones.

Review all the configurations that exist on your machine.

```
gcloud config configurations list
```

Change default configuration that is active to switch between projects.

```
gcloud config configurations activate [NAME]
```

Review only the active project.

```
gcloud projects list
```

Review the details of the current active configuration such as the name, region, account.

```
gcloud config list 
```

Set an attribute of the current active configuration

```
gcloud config set [ATTRIBUTE] [NAME of ATTRIBUTE]
```

List the authenticate user ids and the currently active one, which will have a * next to what shows in the terminal.

```
gcloud auth list
```

Above should show the current active account that you’ve configured with your current active project.


## Running Commands in Parallel with tmux

[tmux](https://github.com/tmux/tmux/wiki) can be used to run commands on multiple compute instances at the same time. Labs in this tutorial may require running the same commands across multiple compute instances, in those cases consider using tmux and splitting a window into multiple panes with synchronize-panes enabled to speed up the provisioning process.

> The use of tmux is optional and not required to complete this tutorial.

![tmux screenshot](images/tmux-screenshot.png)

> Enable synchronize-panes by pressing `ctrl+b` followed by `shift+:`. Next type `set synchronize-panes on` at the prompt. To disable synchronization: `set synchronize-panes off`.

Next: [Installing the Client Tools](02-client-tools.md)
