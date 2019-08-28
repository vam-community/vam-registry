# Virt-A-Mate Scripts Registry

[![Build Status](https://travis-ci.org/vam-community/vam-registry.svg?branch=master)](https://travis-ci.org/vam-community/vam-registry)

This is where the [Party](https://github.com/vam-community/vam-party) package manager will get the list of all scripts.

This repository and the maintainers are not affiliated in any way with Virt-A-Mate or its developers.

## How to add a new script

You first need to [Create a repository](https://help.github.com/en/articles/create-a-repo) and [Push](https://help.github.com/en/articles/pushing-commits-to-a-remote-repository) your script on it. _Note that even though other servers are supported, they will be marked as untrusted in order to protect users privacy._

Once your script has been uploaded, you'll need to get their download URL. We want a URL that will not change when you modify your plugin later, so you have two options:

1. **Using GitHub releases**: Go in your repository's [releases](https://help.github.com/en/articles/creating-releases), find the release you want, and right-click, copy link address.
2. **Using files directly in a commit**: [Select your commit, and Browse files](https://stackoverflow.com/questions/4004860/link-to-a-specific-current-revision-on-github). Then, select the file you want to include, then right-click and select the `copy link address` option on the `Raw` button.

You can then proceed with adding your script to the registry!

1. Install [Party](https://github.com/vam-community/vam-party) if you don't have it already.
2. [Clone](https://help.github.com/en/articles/cloning-a-repository) this repository to your machine (if you already cloned it, make sure to [Pull](https://help.github.com/en/articles/getting-changes-from-a-remote-repository) to get the latest version)
3. Run `party publish Path\To\MyScript.cs --registry Path\To\Cloned\Registry\v1\index.json`.
4. [Fork](https://help.github.com/en/articles/fork-a-repo) the [vam-registry](https://github.com/vam-community/vam-registry) repository in your own account and [Push](https://help.github.com/en/articles/pushing-commits-to-a-remote-repository) your changes to it
5. [Create a Pull Request](https://help.github.com/en/articles/creating-a-pull-request), and if everything looks fine, someone will approve it and merge it.
6. Brag about it! You can tell your users to download your script using `party get your-super-script`.

## Versioning

Please follow the [Semantic Versioning (semver)](https://semver.org/) when selecting version numbers for your scripts. This will ensure users are aware when a new version of your script introduces breaking changes. In a nutshell:

- Increase the PATCH version when you fix bugs (e.g. `1.0.0` to `1.0.1`)
- Increase the MINOR version when you introduce new functionality (e.g. `1.0.1` to `1.1.0`)
- Increase the MAJOR version when you introduce breaking changes (e.g. `1.1.0` to `2.0.0`)

## Why

Using GitHub likes this makes multiple garantees:

- Your privacy is protected, since no one can see who access GitHub
- A minimum level of quality, since everything will be approved and there's a small barrier to entry
- Excellent speed and uptime provided by GitHub servers
- Zero cost for the registry maintainers (except the time to maintain it)
