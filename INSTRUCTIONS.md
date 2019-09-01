# Virt-A-Mate Registry: How to add a new script

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

## Example

Given that you already have a repo for your script and pressed the Fork button on vam-registry;

Clone your fork

    > cd C:\Dev # Your dev folder
    > git clone https://github.com/{user}/vam-registry.git
    Cloning into 'vam-registry'...
    (some more git feedback)
    > cd vam-registry
    > git remote add upstream https://github.com/vam-community/vam-registry.git

Publish your script

    > cd C:\VaM
    > party publish --package-name {my-package} --package-version 1.0.0 --registry "C:\Dev\vam-registry\v1\index.json" "https://github.com/{user}/{plugin-repo}/releases/download/{version}/{file}.cs"
    Release Notes: {Type some short release notes}
    Looks like a new package in the registry! Please provide some information about this new package, or press CTRL+C if you want to abort.
    Author Name: {Username}
    GitHub Profile URL: {Optional}
    Reddit Profile URL: {Optional}
    Description: {A short description of your plugin}
    Tags (comma-separated list): {Some tags to help find your plugin}
    Package Homepage URL: {Usually a URL to your reddit post}
    Package Repository URL: {Usually a URL to your GitHub repo}
    JSON written to D:\Dev\vam-party\TestData\Registry\v1\index.json

Push your new script:

    cd C:\Dev\vam-registry
    git add --all
    git commit -m "Added {package name}"
    git push

Now you can go on https://github.com/vam-community/vam-registry and create the pull request!
