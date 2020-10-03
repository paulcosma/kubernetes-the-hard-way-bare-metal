# Prerequisites

## Hardware Requirements

8 GB of RAM (Preferably 16 GB)
50 GB Disk space

Provision a Debian 10 "Loadbalancer VM" with the following configs:
    
    | VM            |  VM Name   | CPU  | RAM       | IP        |
    | -----------   | ---------  |:----:| :--------:| :--------:|
    | loadbalancer  | kube00     | 1    | 512 MiB   | 10.2.35.0 |

This machine can be used to install the necessary tools and perform all steps.

## Running Commands in Parallel with tmux

[tmux](https://github.com/tmux/tmux/wiki) can be used to run commands on multiple compute instances at the same time. Labs in this tutorial may require running the same commands across multiple compute instances, in those cases consider using tmux and splitting a window into multiple panes with synchronize-panes enabled to speed up the provisioning process.

> The use of tmux is optional and not required to complete this tutorial.

![tmux screenshot](images/tmux-screenshot.png)

> Enable synchronize-panes by pressing `ctrl+b` followed by `shift+:`. Next type `set synchronize-panes on` at the prompt. To disable synchronization: `set synchronize-panes off`.

Next: [Installing the Client Tools](02-client-tools.md)