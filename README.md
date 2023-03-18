# Phishing Websites Features
One of the challenges faced by our research was the unavailability of reliable training datasets. In fact, this challenge faces any researcher in the field. However, although plenty of articles about predicting phishing websites using data mining techniques have been disseminated these days, no reliable training dataset has been published publically, maybe because there is no agreement in literature on the definitive features that characterize phishing websites, hence it is difficult to shape a dataset that covers all possible features.

In this article, we shed light on the important features that have proved to be sound and effective in predicting phishing websites. In addition, we proposed some new features, experimentally assign new rules to some well-known features and update some other features.
# Scope

⚠️ Official support for building Pages with Actions is in public beta at the moment.

# Usage

See [action.yml](action.yml)

<!-- TODO: document custom workflow -->

# Artifact validation

While using this action is optional, we highly recommend it since it takes care of producing (mostly) valid artifacts.

A Pages artifact must:

- Be called `github-pages`
- Be a single [`gzip` archive][gzip] containing a single [`tar` file][tar]

The [`tar` file][tar] must:

- be under 10GB in size
- not contain any symbolic or hard links

# Release instructions

In order to release a new version of this Action:

1. Locate the semantic version of the [upcoming release][release-list] (a draft is maintained by the [`draft-release` workflow][draft-release]).

2. Publish the draft release from the `main` branch with semantic version as the tag name, _with_ the checkbox to publish to the GitHub Marketplace checked. :ballot_box_with_check:

3. After publishing the release, the [`release` workflow][release] will automatically run to create/update the corresponding the major version tag such as `v0`.

   ⚠️ Environment approval is required. Check the [Release workflow run list][release-workflow-runs].

# License

The scripts and documentation in this project are released under the [MIT License](LICENSE).

<!-- references -->
[pages]: https://pages.github.com
[release-list]: https://github.com/actions/upload-pages-artifact/releases
[draft-release]: .github/workflows/draft-release.yml
[release]: .github/workflows/release.yml
[release-workflow-runs]: /actions/workflows/release.yml
[gzip]: https://en.wikipedia.org/wiki/Gzip
[tar]: https://en.wikipedia.org/wiki/Tar_(computing)
