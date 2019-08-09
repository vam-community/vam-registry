# Virt-A-Mate Scripts Registry

[![Build Status](https://travis-ci.org/vam-community/vam-registry.svg?branch=master)](https://travis-ci.org/vam-community/vam-registry)

This is where the [Party](https://github.com/vam-community/vam-party) package manager will get the list of all scripts.

This repository and the maintainers are not affiliated in any way with Virt-A-Mate or its developers.

## How to add a new script

First, make sure it has been uploaded to your own GitHub account. Note that even though other servers are supported, they will be marked as untrusted in order to protect users privacy.

Once uploaded, you'll need to get their download URL Go on https://github.com and open your repository. We want a URL that will not change when you modify your plugin later.

- If you use releases: Go in releases, find the release you want, and right-click, copy link address.
- If you don't use releases: [Select your commit, and Browse files](https://stackoverflow.com/questions/4004860/link-to-a-specific-current-revision-on-github). Then, select the file you want to include, and right-click, copy link address on the Raw button.

Run `party package Path\To\Script` to get the list of files and their hash. This will get you a JSON like this:

```json
{
  "files": [
    {
      "filename": "MyScript.cs",
      "url": "",
      "hash": {
        "type": "sha256",
        "value": "0000000000000000000000000000000000000000000000000000000000000000"
      }
    }
  ]
}
```

Replace the `url` with the one you got before.

Now that we have the list of files, we need to create the new script.

First, fork and clone the https://github.com/vam-community/vam-registry.

You can now add your plugin to the list.

Here's a template to get you started:

```json
{
  "name": "your-plugin-name",
  "author": {
    "name": "your-username",
    "profile": "https://github.com/your-username"
  },
  "homepage": "https://github.com/your-username/your-plugin-name",
  "repository": "https://github.com/your-username/your-plugin-name",
  "versions": [
    {
      "version": "2.0.4",
      "files": [
        /* The files retrieved before */
      ]
    }
  ]
}
```

You can add your script anywhere, as long as it's somewhere in the list.

You also need to make sure your JSON is valid, and formatted correctly! You can use [VSCode](https://code.visualstudio.com/) to do that (open the `index.json` file, and <kbd>ctrl</kbd> <kbd>shift</kbd> <kbd>p</kbd>, format, enter).

You can finally push your changes and open a pull request. You can find more about opening pull requests here: [Creating a pull request](https://help.github.com/en/articles/creating-a-pull-request).

This process will eventually be made easier, but for now this will allow high security, low maintenance and high transparency. In the event this registry becomes popular, a dedicated server with authentication will replace it.
