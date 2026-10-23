# Moso

**Moso** is a minimal macOS menu bar app written in Swift. This is a fork of
[rschiang/moso], which is based on the awesome [Pomodoro] project. Other
pomodoro apps do too much, don't look good, or have ads. Moso does exactly what
it needs to do, and doesn't have ads.

Moso runs the classic Pomodoro schedule: 25-minute tasks with 5-minute breaks.
When a task or a break is over, it sends a notification.

![Moso screenshot](docs/screenshot.png)

The name [Moso] derived from Taiwanese Hakka <ruby>摸<rt>mò</rt>挲<rt>sò</rt></ruby>,
which means fiddling around out of procrastination.

## Why forking Moso?

I've forked Moso to add a few improvements that I felt I needed for me to be
comfortable.

Also, the main reason to use Moso as a base was that it's very simple and to
the point. This means that if you're a developer you can audit its code in a
few minutes to understand it does exactly what it advertises, no more, no less.

## Download

Download Moso from the [releases] page.

## Making a release

Releases are built by the `macOS Universal Build + DMG` GitHub Actions workflow
whenever a tag starting with `v` is pushed. The workflow builds a universal
(Apple Silicon + Intel) app and attaches two downloads to the GitHub release for
that tag:

- `Moso.dmg`: disk image with the app and an `Applications` shortcut.
- `Moso.zip`: the zipped `Moso.app`.

The app version is taken from the tag (without the leading `v`); builds that are
not triggered by a tag use version `0.0.0`.

There are two ways to make a release. In both cases, first make sure `main`
contains everything that should go into the release.

### From the GitHub web page

1. On the [releases] page, click **Draft a new release**.
2. Choose a new tag (e.g. `v1.2.3`) targeting `main`, fill in the title and
   release notes, and click **Publish release**.
3. Publishing the release creates the tag, which triggers the workflow. Wait for
   it to finish in the [Actions] tab; it uploads the DMG and the zip to the
   existing release.

### From the command line

1. Create and push a tag for the new version:

   ```sh
   git checkout main
   git pull
   git tag v1.2.3
   git push origin v1.2.3
   ```

2. Wait for the workflow to finish in the [Actions] tab. Since no release exists
   for the tag, it creates one named after the tag, with auto-generated release
   notes, and attaches the DMG and the zip.
3. Optionally, edit the release notes on the [releases] page.

### If the build fails

The workflow builds the code at the tagged commit, so re-running it won't pick up
fixes made afterwards. Fix the problem on `main`, delete the release (if it was
created) and the tag, and make the release again:

```sh
gh release delete v1.2.3 --yes
git tag -d v1.2.3
git push origin :refs/tags/v1.2.3
```

## License

Moso is released under [MIT License].

[Moso]: https://www.moedict.tw/:摸挲

[rschiang/moso]: https://github.com/rschiang/moso

[Pomodoro]: https://github.com/apas/pomodoro

[releases]: https://github.com/xrubioj/moso/releases

[Actions]: https://github.com/xrubioj/moso/actions

[MIT License]: LICENSE.md
