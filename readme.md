<br />
<div align="center">
   <img alt="Banner" src="https://github.com/krejdster/audiobookshelf-editorpro/raw/master/images/EditProHeader.gif" width="600">
</div>

# About

[Audiobookshelf](https://github.com/advplyr/audiobookshelf/) is a self-hosted audiobook and podcast server.

# ABS EditPro - Fork changes

I have hundreds of scattered audiobooks with pretty bad metadata. And I love Audiobookshelf. It's great for listening audiobooks and very good for improving metadata. But embedding metadata directly to files and quick metadata operations are not possible because UI has to stay clean for casual user.

How about we don't care about clean UI anymore and make the UI as cluttered as possible to achieve fastest metadata editing / improving / embedding possible? Welcome to Audiobookshelf EditPro.

Audiobookshelf EditPro is a swiss tool for ninja editing of broken metadata. With this tool, it's easy to quickly do all of the metadata operations directly on the book's page:
- quick edit most important details
- quick access button for chapter editor
- quick glance information whether audiobook was already converted from single mp3 files to m4b
- quick access button for m4b conversion
- quick access button to directly embed metadata to file
- quick access button to rescan the library directly from book's page
- this version of Audiobookshelf has all the confirmation messages disabled for quick UI movement
- BIG BUTTONS for easy and fast metadata hacking

This is not a production-ready app. This is not a Docker container to run in your homelab. It's a hacked version of Audiobookshelf that will make editing your metadata a breeze.

<img alt="ABS EditPro Screenshot" src="https://github.com/krejdster/audiobookshelf-editorpro/raw/master/images/EditPro.jpg" width="800">

## Workflow

- Run ABS EditPro on your local machine
- Import all the books you want to fix either from your local machine or NFS/SMB share
- Go through all the books by quickly editing most crucial metadata
- Scrape more data from the internet
- Embed all supported metadata directly to M4B file or MP3 files
- Queue M4B conversion in the background and move on to another book
- Force rescan library directly from the book page because it might get messy after a while
- Keep listening and enjoying audiobooks instead of fighting with metadata!!!

# Run from source

### Dev Container Setup

The easiest way to begin developing this project is to use a dev container. An introduction to dev containers in VSCode can be found [here](https://code.visualstudio.com/docs/devcontainers/containers).

Required Software:

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [VSCode](https://code.visualstudio.com/download)

_Note, it is possible to use other container software than Docker and IDEs other than VSCode. However, this setup is more complicated and not covered here._

<div>
<details>
<summary>Install the required software on Windows with <a href=(https://docs.microsoft.com/en-us/windows/package-manager/winget/#production-recommended)>winget</a></summary>

<p>
Note: This requires a PowerShell prompt with winget installed.  You should be able to copy and paste the code block to install.  If you use an elevated PowerShell prompt, UAC will not pop up during the installs.

```PowerShell
winget install -e --id Docker.DockerDesktop; `
winget install -e --id Microsoft.VisualStudioCode
```

</p>
</details>
</div>

<div>
<details>
<summary>Install the required software on MacOS with <a href=(https://snapcraft.io/)>homebrew</a></summary>

<p>

```sh
brew install --cask docker visual-studio-code
```

</p>
</details>
</div>

<div style="padding-bottom: 1em">
<details>
<summary>Install the required software on Linux with <a href=(https://brew.sh/)>snap</a></summary>

<p>

```sh
sudo snap install docker; \
sudo snap install code --classic
```

</p>
</details>
</div>

After installing these packages, you can now install the [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack) extension for VSCode. After installing this extension open the command pallet (`ctrl+shift+p` or `cmd+shift+p`) and select the command `>Dev Containers: Rebuild and Reopen in Container`. This will cause the development environment container to be built and launched.

You are now ready to start development!

### Manual Environment Setup

If you don't want to use the dev container, you can still develop this project. First, you will need to install [NodeJs](https://nodejs.org/) (version 20) and [FFmpeg](https://ffmpeg.org/).

Next you will need to create a `dev.js` file in the project's root directory. This contains configuration information and paths unique to your development environment. You can find an example of this file in `.devcontainer/dev.js`.

You are now ready to build the client:

```sh
npm ci
cd client
npm ci
npm run generate
cd ..
```

### Development Commands

After setting up your development environment, either using the dev container or using your own custom environment, the following commands will help you run the server and client.

To run the server, you can use the command `npm run dev`. This will use the client that was built when you ran `npm run generate` in the client directory or when you started the dev container. If you make changes to the server, you will need to restart the server. If you make changes to the client, you will need to run the command `(cd client; npm run generate)` and then restart the server. By default the client runs at `localhost:3333`, though the port can be configured in `dev.js`.

You can also build a version of the client that supports live reloading. To do this, start the server, then run the command `(cd client; npm run dev)`. This will run a separate instance of the client at `localhost:3000` that will be automatically updated as you make changes to the client.

If you are using VSCode, this project includes a couple of pre-defined targets to speed up this process. First, if you build the project (`ctrl+shift+b` or `cmd+shift+b`) it will automatically generate the client. Next, there are debug commands for running the server and client. You can view these targets using the debug panel (bring it up with (`ctrl+shift+d` or `cmd+shift+d`):

- `Debug server`—Run the server.
- `Debug client (nuxt)`—Run the client with live reload.
- `Debug server and client (nuxt)`—Runs both the preceding two debug targets.
