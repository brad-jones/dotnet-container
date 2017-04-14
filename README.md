# Containers for Dotnet, VsCode & Rider
Recently started working with [dotnet core 1.1](https://www.microsoft.com/net/core)
on my Fedora 25 workstation. Problem is dotnet core is not yet offically supported
on the latest version of Fedora. There are a few binary incompatibilities.

So the solution was to actually run dotnet with the help of docker,
the plan is to deploy our app with docker anyway, so why not use docker
for everything.

__THESE CONTAINERS ARE NOT FOR PRODUCTION USE BUT FOR LOCAL DEVELOPMENT__

## Docker Run Scripts
Under `./bin` there are some simple bash scripts that build and execute
`docker run` commands for each container. You may either copy these scripts into
a location that is on your _PATH_ or you may add the `./bin` folder to your path.

## Container 1: bradjones/dotnet
This container extends the offical [microsoft/dotnet](https://hub.docker.com/r/microsoft/dotnet/)
container and sets up [su-exec](https://github.com/ncopa/su-exec) to execute a 
given command as the same user as your host such that generated files will have
the correct ownership, etc.

So with this container and the included run script `./bin/dotnet` you can
execute the `dotnet` toolchain as if it was installed onto your local host system.

## Container 2: bradjones/dotnet-ide
This container does not provide any addtional functionality by it's self,
it only serves as the base image for both the vscode and rider images.
It installs a bunch of X server stuff, Mono, NodeJs, TypeScript, etc.

## Container 3: bradjones/dotnet-rider
This container extends `bradjones/dotnet-ide` and installs
[JetBrain's Rider IDE](https://www.jetbrains.com/rider/).

You can easily run this with the included run script: `./bin/rider`.

## Container 4: bradjones/dotnet-vscode
This container extends `bradjones/dotnet-ide` and installs
[Microsoft's Visual Studio Code Editor](https://code.visualstudio.com/).

You can easily run this with the included run script: `./bin/code`.

## Know Issues:

- The way I have setup the run scripts for the containers, your working
  directory must be with-in your host users home directory. Attempting run
  any of the containers outside of this will result in failure.
