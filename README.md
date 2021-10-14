# .NET6 in devcontainer [![Open in Visual Studio Code](https://open.vscode.dev/badges/open-in-vscode.svg)](https://open.vscode.dev/NikiforovAll/devcontainer-for-dotnet6-demo)


This repository demonstates how to use devcontainers to configure consistent developer environment focused on the project needs.

All you need to do is to open repository in VSCode and run 'Remote-Containers: Open Folder in Container...'.

`dotnet run --project ./src/App/`

## Setup
Base container:

* Source: <https://github.com/NikiforovAll/dev-containers/tree/master/containers/dotnet>
* GitHub Container Registry <https://github.com/NikiforovAll/dev-containers/pkgs/container/devcontainers%2Fdotnet>
* Docker Hub <https://hub.docker.com/repository/docker/nikiforovall/devcontainers-dotnet>

As you can see, everything is you need is already in devcontainer.

1. Base image, you can create custom-tailor devcontainer for your needs. 🐳
2. VSCode settings and used extensions. 👩‍💻
3. (Extra) Mount dotfiles, you can use dotfiles by providing vscode special settings (see example below).

```json
{
    "name": ".NET 6 devcontainer",
    "image": "nikiforovall/devcontainers-dotnet:latest", // https://github.com/NikiforovAll/dev-containers/tree/master/containers/dotnet
    "settings": {
        "terminal.integrated.defaultProfile.linux": "/bin/bash",
        "dotfiles.installCommand": "",
        "remote.containers.dotfiles.repository": "https://github.com/NikiforovAll/dotfiles.git",
        "remote.containers.dotfiles.installCommand": "~/dotfiles/src/dev-container/boot/install.sh",
        "remote.containers.dotfiles.targetPath": "~/dotfiles",
    },
    // Add the IDs of extensions you want installed when the container is created.
    "extensions": [
        // dotnet
        "ms-dotnettools.csharp",
        "formulahendry.dotnet-test-explorer",
        "tintoy.msbuild-project-tools",
        "nikiforovall.surround-with-csharp",
        //git
        "eamodio.gitlens",
        "mhutchie.git-graph",
        "codezombiech.gitignore",
        // MISC
        "k--kato.docomment",
        "yzhang.markdown-all-in-one",
        "dotjoshjohnson.xml",
        "editorconfig.editorconfig",
        "naumovs.trailing-semicolon",
    ]
}
```

### MISC 

Common CLI tools are baked into base devcontainer. See [source code](https://github.com/NikiforovAll/dev-containers/tree/master/containers/dotnet) for more details.

```bash
# (excerpt)
# ...
apt-get -y install --no-install-recommends \
    tree \
    silversearcher-ag \
    lnav \
    fasd
    fd-find \
    bat \
    ripgrep

# fzf https://github.com/junegunn/fzf#key-bindings-for-command-line
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install --key-bindings --completion --no-update-rc

# fd https://github.com/sharkdp/fd
# dpkg -i ./tmp/library-scripts/fd_8.1.1_amd64.deb

# # https://github.com/sharkdp/bat
# dpkg -i ./tmp/library-scripts/bat_0.16.0_amd64.deb

# # https://github.com/BurntSushi/ripgrep
# dpkg -i ./tmp/library-scripts/ripgrep_12.1.1_amd64.deb

EXA_URL="https://github.com/ogham/exa/releases/download/v0.9.0/$EXA_FILENAME"
curl -sL $EXA_URL -o /tmp/$EXA_FILENAME exa
unzip "/tmp/$EXA_FILENAME" -d /tmp &>/dev/null
mv "/tmp/$EXA_BUILD" /usr/local/bin/exa
# ...
```
