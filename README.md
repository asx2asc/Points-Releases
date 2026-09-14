# Achievement Point Tracker — public version feed

This repository exists so that a school computer can answer one question without any
credentials, any Git client, and any access to the private source repository:

> **Is the copy installed here the current one?**

That is all it holds. The application source is private and stays private.

## What is here

[`version.json`](version.json) — the version feed the application reads:

```json
{
  "name": "Achievement Point Tracker",
  "version": "0.5.0",
  "release_date": "2026-09-14",
  "release_url": "https://github.com/asx2asc/Points-Releases/releases/latest",
  "notes": "Clean school deployment package for v0.5.0.",
  "min_python": "3.10"
}
```

The application fetches it over plain HTTPS from
`https://raw.githubusercontent.com/asx2asc/Points-Releases/main/version.json` and compares
`version` against the version it is running. Nothing is sent: the request carries no
identifying information beyond a user agent, and no telemetry is collected.

**No pupil data, no school data and no register information is published here, and none
ever should be.** This feed is application metadata only.

## For IT / ICT departments

When this feed advertises a version newer than the one installed, staff see a notice in the
application and can copy a pre-formatted request to send to you. It never installs anything
by itself and never interrupts work in progress — a teacher can carry on with the version
they have.

Release packages are attached to the [releases](../../releases) of this repository.

## Publishing a new version

1. Update the application's version in `pyproject.toml`.
2. Run `python package_school_release.py`, which writes a matching `version.json`.
3. Commit that file here and push, then attach the release package to a new release.

`version.json` must be updated **at the same time as** the release it describes. A feed
advertising a version that has not been published tells every school to ask their IT
department for something that does not exist.
