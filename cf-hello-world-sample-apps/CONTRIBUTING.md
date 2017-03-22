## Pull Requests

Feel free to submit a pull request.

Our commit message format is as follows:

``` 
Tag: Short description (fixes #1234)

Longer description here if necessary 
```

The first line of the commit message (the summary) must have a specific format. This format is checked by our build tools.

The Tag is one of the following:

- **Fix** - for a bug fix.
- **New** - implemented a new feature.
- **Update** - for a backwards-compatible enhancement.
- **Breaking** - for a backwards-incompatible enhancement or feature.
- **Docs** - changes to documentation only.
- **Build** - changes to build process only.
- **Upgrade** - for a dependency upgrade.

Use the labels of the issue you are working on to determine the best tag.

The message summary should be a one-sentence description of the change, and it must be 72 characters in length or shorter. The issue number should be mentioned at the end. If the commit doesn't completely fix the issue, then use ``(refs #1234)`` instead of ``(fixes #1234)``.

Here are some good commit message summary examples:
```
Build: Update Travis to only test Node 0.10 (refs #734)
Fix: Semi rule incorrectly flagging extra semicolon (fixes #840)
Upgrade: Esprima to 1.2, switch to using Esprima comment attachment (fixes #730)
```
The commit message format is important because these messages are used to create a changelog for each release. The tag and issue number help to create more consistent and useful changelogs.
