<!-- markdownlint-disable MD033 MD041 -->

![LiveWyer Banner](./.github/img/github-banner.png?raw=true)

<p align="center">
    <a href="https://livewyer.io" ><img src="https://badgen.net/badge/Website/livewyer.io" alt="LiveWyer Website badge" /></a>
    <a href="https://twitter.com/LiveWyerUK"><img src="https://badgen.net/badge/twitter/@LiveWyerUK" alt="Twitter badge" /></a>
    <a href="https://www.linkedin.com/company/livewyer"><img src="https://badgen.net/badge/LinkedIn/LiveWyer" alt="LinkedIn badge" /></a>
</p>

<h1 align="center">Vale Packages</h1>

## Overview

We have adopted Vale to improve the quality and consistency of our written content across the company. This repository contains custom Vale packages designed to enforce style guidelines and maintain clear, consistent writing. In this repository you will find all the necessary resources to use them in your workflow.

You can find more information about Vale at [vale.sh](https://vale.sh/docs).

### Packages

All available packages can be found in the [packages](./packages/) directory.

This repository contains three packages, each with its own functionality and style:

* [general](./packages/general/): used as a foundational package for github and website packages, it enforces company-wide style and vocabulary.
* [github](./packages/github/): used for documentation stored in GitHub, it applies a formal style and GitHub vocabulary.
* [website](./packages/website/): used for LiveWyer websites, applies a formal style for website content and a less formal style for blog posts, includes website vocabulary.

The table below displays the enabled and disabled styles in our packages. For more details about the styles used, please refer to the official [Package Hub](https://vale.sh/hub/).

| Styles      | General | Github | Website |
|-------------|:-------:|:------:|:-------:|
| Vale        |    ✅    |   ✅    |    ✅    |
| Microsoft   |    ✅    |   ✅    |   ✅/❌   |
| alex        |    ✅    |   ✅    |    ✅    |
| Readability |    ✅    |   ✅    |    ✅    |
| Joblint     |    ✅    |   ✅    |    ✅    |
| LiveWyer    |    ✅    |   ✅    |    ✅    |
| write-good  |    ❌    |   ✅    |   ✅/❌   |
| proselint   |    ❌    |   ✅    |   ✅/❌   |

***Note:** Combination of ✅ and ❌ marks indicates that the style is enabled in the package but applied only to specific content.*

## Guide

### How to use a package

To use this package:

* Place the files from the `usage` directory in the root of your repository
* Replace `<package>` placeholder in `.vale.ini` file with the correct name: `website` or `github`. Refer to the [working-example.vale.ini](./usage/working-example.vale.ini) file to make sure you updated it correctly.
* Execute the respective commands as commented in the `usage/.vale.ini` file.

## Contributing

We value your feedback and suggestions!
If you have any ideas or want to report issues, please create an [issue](https://github.com/livewyer-ops/vale-packages/issues/new/choose).
Additionally, you can submit your contributions by opening a [pull request](https://github.com/livewyer-ops/vale-packages/pulls).

### How to update a package

Prerequisites:

* Permissions to upload release assets in [vale-packages](https://github.com/livewyer-ops/vale-packages) repository
* [zip CLI](https://infozip.sourceforge.net/license.html) or any other tool that allows you to create a `zip` archive
* [gh CLI](https://cli.github.com/)

To update these packages, start by updating files in the respective directories. Once you are satisfied with the package content:

* Create a Pull Request with your changes and assign the respective label to it, so it can be released. Refer to the [Releases](#releases) section for more details.
* Merge a Pull Request and wait for the new release to be created.
* Create and upload `zip` archives using the following command:

```bash
# Replace <tag> value with the tag of your release
export RELEASE_TAG=<tag>

cd packages
# Create zip archives
zip -r general.zip general
zip -r website.zip website
zip -r github.zip github
# Upload zip archives to a GitHub Release
gh release upload $RELEASE_TAG general.zip website.zip github.zip --clobber
# Remove unneeded files
rm -rf general.zip website.zip github.zip

cd ../
```

***Note:** Once you have finished, please ensure to update the release tag in `github/.vale.ini`, `website/.vale.ini` and `usage/.vale.ini` to the one you just created.*

### Releases

The releases in this repository are managed using the [Auto Release Pipeline](./.tekton/release.yaml). This pipeline automatically generates GitHub tags, releases, and changelog based on the [**labels**](https://intuit.github.io/auto/docs/configuration/autorc#labels) of your Pull Requests (PRs). To include your PR in an upcoming release, make sure to add the appropriate labels. If you want to initiate a new release, add the `release` label to your PR. For detailed information about the labels and the tool itself, refer to the [official documentation of the Auto tool](https://intuit.github.io/auto/docs).

Before committing to this repository, familiarize yourself with the [auto Configuration File](./.autorc).

### Markdown Lint

The markdown lint in this repositry is managed using the [Markdown Lint Pipeline](./.tekton/markdown-lint.yaml). This pipeline automatically lints `md` files using [markdownlint CLI](https://github.com/DavidAnson/markdownlint).

Before committing to this repository, familiarize yourself with the [markdownlint Configuration File](./.markdownlint-cli2.yaml).

---

Copyright © 2024 LiveWyer, Licensed under the `MIT` License; you may not use this file except in compliance with the [License](LICENSE).

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations under the [License](LICENSE).
