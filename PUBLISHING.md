# How to add a new script

You will require some basic knowledge of [git](https://git-scm.com/) to publish a script. If you don't already know about this tool, then check out a quick tutorial and come back. It'll make things much easier to understand.

## TL;DR

In a nutshell, you need to:

1. Upload your script on GitHub and get a permanent link to it
2. Fork this repository
3. Use [party publish](https://github.com/vam-community/vam-party) to update the registry's `index.json`
4. Make a pull request

## Uploading your script to GitHub

You have two options to host your script files:

1. Make a [pull request](https://help.github.com/en/articles/creating-a-pull-request) on the [vam-packages GitHub repository](https://github.com/vam-community/vam-packages); this can be useful if you don't own the scripts.
2. Create your own [GitHub repository](https://help.github.com/en/articles/create-a-repo) and [push](https://help.github.com/en/articles/pushing-commits-to-a-remote-repository) your script on it.

Technically you can also use another host, but your scripts will then be marked as _untrusted_ to protect users privacy.

## Getting the download url to your script file

Note that we _strongly_ recommend you don't reference your `master` working file directly, since the file may change. You can either make a [release](https://help.github.com/en/articles/creating-releases) in your GitHub repository (the preferred option), or keep a copy of the file in a version folder (e.g. `publish/1.0.0/My Script.cs`).

To create a direct link from releases:

1. Go to the releases tab in your repository page
2. Find the release your want, and find the file you want under `assets`
3. Right-click, select `copy link address`

To create a direct link to the raw files:

1. Select the file you want to include on GitHub
2. Find the `Raw` button; right-click on it, and select `copy link address`

## Adding your script to the registry

You can now proceed with adding your script to the registry!

1. Install [party](https://github.com/vam-community/vam-party) if you don't have it already.
2. [Clone](https://help.github.com/en/articles/cloning-a-repository) this repository to your machine (if you already cloned it, make sure to [Pull](https://help.github.com/en/articles/getting-changes-from-a-remote-repository) to get the latest version)
3. [Fork](https://help.github.com/en/articles/fork-a-repo) the [vam-registry](https://github.com/vam-community/vam-registry) repository in your own account and [Push](https://help.github.com/en/articles/pushing-commits-to-a-remote-repository) your changes to it
4. Run `party publish {https://github.com/...} --registry {C:\vam-registry}\v1\index.json` where the values in `{}` should be replaced with yours. Check the [documentation](https://github.com/vam-community/vam-party/blob/master/USAGE.md#publish) for more parameters.
5. Commit your changes and [push](https://help.github.com/en/articles/pushing-commits-to-a-remote-repository)
6. [Create a Pull Request](https://help.github.com/en/articles/creating-a-pull-request), and if everything looks fine, someone will approve it and merge it.

## Versioning

Please follow the [Semantic Versioning (semver)](https://semver.org/) when selecting version numbers for your scripts. This will ensure users are aware when a new version of your script introduces breaking changes. In a nutshell:

- Increase the PATCH version when you fix bugs (e.g. `1.0.0` to `1.0.1`)
- Increase the MINOR version when you introduce new functionality (e.g. `1.0.1` to `1.1.0`)
- Increase the MAJOR version when you introduce breaking changes (e.g. `1.1.0` to `2.0.0`)

## Example

You should already have your script in GitHub, and forked the registry in your account. I'll use `acidbubbles` and the `TimeScaleController.cs` as an example.

Clone your fork

    > cd C:\Dev
    > git clone https://github.com/acidbubbles/vam-registry.git
    Cloning into 'vam-registry'...
    (some more git feedback)
    > cd vam-registry
    > git remote add upstream https://github.com/vam-community/vam-registry.git

Publish your script

    > cd C:\...\VaM
    > party publish --package-name time-scale-controller --package-version 1.0.0 --registry "C:\Dev\vam-registry\v1\index.json" "https://github.com/acidbubbles/vam-utilities/releases/download/v1.0.0/TimeScaleController.cs"
    Release Notes: Fixed some bugs
    Looks like a new package in the registry! Please provide some information about this new package, or press CTRL+C if you want to abort.
    Author Name: Acidbubbles
    GitHub Profile URL: https://github.com/acidbubbles
    Reddit Profile URL: https://www.reddit.com/user/acidbubbles/
    Description: Allows controlling the time scale in scenes
    Tags (comma-separated list): time,utility
    Package Homepage URL: https://reddit.com/...
    Package Repository URL: https://github.com/acidbubbles/vam-utilities
    JSON written to D:\Dev\vam-party\TestData\Registry\v1\index.json

Push your new script:

    cd C:\Dev\vam-registry
    git add --all
    git commit -m "time-scale-controller, by Acidbubbles"
    git push

Now you can go on https://github.com/vam-community/vam-registry and create the pull request!

## Special cases

### Non-script dependencies

When your plugin requires non-code files (such as `.wav` files), you can specify the dependencies by manually adding these files to your plugin version (under `files`):

    ...
    {
      "localPath": "/Custom/atom/person/morphs/female/My Required Morph.dsf"
    },
    ...

By doing so, you'll prevent users from automatically installing the plugin, unless they already have those files. Otherwise the `downloadUrl` link will be displayed so the can download it manually. If however they do have the files, it'll upgrade just fine.

### Files included in .vac by error

If you included a file by error in `.vac` files, you'll probably want them to still be linked to your plugin, but not downloaded when people install it manually. You can do this by adding `"ignore": true` to your file. This also means that when this file is missing, the plugin will still be considered correct.

### Dependencies

You can specify dependencies, so if multiple plugins depend on a set of morphs, you can create a package for these morphs, and depend on that package instead. Search for `dependencies` for examples.

### Non-downloadable packages

You can specify a hash but no download URL if you want. This will allow identifying the script, and can be useful when you may have older versions you don't want to re-publish, but still have them show up when running `party status`.
