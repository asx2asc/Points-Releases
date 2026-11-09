# Merit Tracker — public version feed

This repository exists so that a school computer can answer one question without any
credentials, any Git client, and any access to the private source repository:

> **Is the copy installed here the current one?**

That is all it holds. The application source is private and stays private.

## What is here

[`version.json`](version.json) — the version feed the application reads:

```json
{
  "name": "Merit Tracker",
  "version": "0.5.0",
  "build": "1f4329192700",
  "release_date": "2026-11-09",
  "release_url": "https://github.com/asx2asc/Points-Releases",
  "notes": "Clean school deployment package for v0.5.0 (build 1f4329192700).",
  "min_python": "3.7.3",
  "previous_builds": [
    "90ab5419a8b2",
    "44cea2168b07",
    "368ddf56329b"
  ],
  "tests": "The fast tier of tests passed on this copy before it was packaged."
}
```

The application fetches it over plain HTTPS from
`https://raw.githubusercontent.com/asx2asc/Points-Releases/main/version.json` and compares
`version` and `build` against the copy it is running. `previous_builds` lists the earlier
builds of the same version that this one replaces, so a copy of one of those is told there
is an update. Nothing is sent: the request carries no identifying information beyond a user
agent, and no telemetry is collected.

**No pupil data, no school data and no register information is published here, and none
ever should be.** This feed is application metadata only.

## For IT / ICT departments

When this feed advertises a version newer than the one installed, staff see a notice in the
application and can copy a pre-formatted request to send to you. It never installs anything
by itself and never interrupts work in progress — a teacher can carry on with the version
they have.

**The release package is not published here.** The application source is private, and a
school deployment is plain Python source, so attaching it would publish the source along
with it. Obtain the package from whoever supplied the software.

This repository answers *whether* an update exists. It is deliberately not how the update
is distributed.

## Publishing a new version

1. Update the application's version in `pyproject.toml`.
2. Run `python package_school_release.py`, which writes a matching `version.json`.
3. Commit that file here and push.

`version.json` must be updated **at the same time as** the release it describes. A feed
advertising a version that has not been published tells every school to ask their IT
department for something that does not exist.
