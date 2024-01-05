# How to fix `Cannot connect to the docker damien` errors after installing Rancher Desktop

The most likely problem is that Docker Desktop was not fully uninstalled before installing Rancher.

From a solution from the Rancher github: [here](https://github.com/rancher-sandbox/rancher-desktop/issues/2534#issuecomment-1485193048)

> I've also found that if you've had Docker Desktop installed previously, the following seems to help.
>
> I did the following:
>
> - Shut down Rancher Desktop
> - Follow the instructions here: https://docs.docker.com/desktop/uninstall/ (both the UI and CLI uninstall process)
> - Deleted the ~/.docker directory created by Docker Desktop
> - Start Rancher Desktop
> - Enable the dockerd (moby) setting
