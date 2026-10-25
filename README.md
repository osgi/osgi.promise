# osgi.promise

[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/osgi/osgi.promise/badge)](https://securityscorecards.dev/viewer/?uri=github.com/osgi/osgi.promise)
[![build](https://github.com/osgi/osgi.promise/actions/workflows/build.yml/badge.svg?branch=main)](https://github.com/osgi/osgi.promise/actions/workflows/build.yml)
[![Maven Central](https://img.shields.io/maven-central/v/org.osgi/osgi.promise)](https://central.sonatype.com/artifact/org.osgi/osgi.promise)

OSGi Promise Release: the `osgi.promise` jar with the Promise API and the functional
interfaces it uses, for use inside and outside of OSGi environments.

Part of the [OSGi Specification Project](https://projects.eclipse.org/projects/technology.osgi).

## Contents

This repository holds no sources of its own. The API lives in the
specification repositories [org.osgi.util.function](https://github.com/osgi/org.osgi.util.function), [org.osgi.util.promise](https://github.com/osgi/org.osgi.util.promise). This repository pins one released
version of each of them and builds from those:

- `api`: `org.osgi:osgi.promise`, the classes of their packages, taken unchanged
  from the pinned `org.osgi` artifacts, with their sources and Javadoc as
  `-sources` and `-javadoc` jars. The build baselines the jar against the
  previous release of `osgi.promise`.

Each specification repository has one version property in `pom.xml`.

## Build

```
mvn clean verify
```

The `build` workflow builds every push and pull request the same way; every
push to `main` deploys a fresh SNAPSHOT to Sonatype Central snapshots, and
a weekly schedule keeps it fresh in quiet times.

## Versioning and releases

The version lives in exactly one place: the `-Drevision=` line in
[`.mvn/maven.config`](.mvn/maven.config). The poms only reference
`${revision}` — never add a second copy of the version anywhere else.

A release is the creation of a git tag whose name equals that version,
without any prefix: `1.2.3`, not `v1.2.3`.

1. Open a pull request that sets `-Drevision=1.2.3` in `.mvn/maven.config`
   and merge it.
2. Go to **Releases → Draft a new release**, type `1.2.3` under
   "Choose a tag" and select "Create new tag on publish". A saved draft
   does not create the tag yet, so a draft is a safe intermediate state.
3. Leave **Target: `main`** (the default) — the tag will point at the
   merge commit.
4. Click **Publish release**. Publishing creates the tag, and the tag
   triggers the release workflow.

The command-line equivalent is
`gh release create 1.2.3 --target main --generate-notes`.

The release workflow refuses a tag that does not exactly match
`.mvn/maven.config`, and refuses `-SNAPSHOT` versions. It builds and tests
the repository, then stages the signed artifacts to Maven Central — the
final publish stays a manual step in the Central portal.

## Contact

- Project contact page: <https://projects.eclipse.org/projects/technology.osgi/contact>
- Mailing lists:
  - [osgi-dev](https://accounts.eclipse.org/mailing-list/osgi-dev) —
    developer list for discussion of the OSGi Specification Project
  - [osgi-users](https://accounts.eclipse.org/mailing-list/osgi-users) —
    public list for discussion of OSGi technology and specifications; ask
    your technical questions about OSGi here
  - [osgi-wg](https://accounts.eclipse.org/mailing-list/osgi-wg) —
    OSGi Working Group mail list
- Slack: <https://osgiwg.slack.com/>
- Spec call: Zoom call every **second Wednesday** — see the
  [calendar](https://calendar.google.com/calendar/u/0/newembed?src=c_fh3lhb5p0l29f6phu2ndifh4a4@group.calendar.google.com)
  for the exact time (please mind your local timezone).
