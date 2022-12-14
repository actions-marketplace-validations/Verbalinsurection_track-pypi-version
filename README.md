# Track PyPI version javascript action

[![GitHub Release Version](https://img.shields.io/github/v/release/Verbalinsurection/track-pypi-version.svg?include_prereleases)](https://github.com/Verbalinsurection/track-pypi-version/releases)
![GitHub Release Date](https://img.shields.io/github/release-date/Verbalinsurection/track-pypi-version)
[![GitHub](https://img.shields.io/github/license/Verbalinsurection/track-pypi-version)](LICENSE)
[![CodeFactor](https://www.codefactor.io/repository/github/verbalinsurection/track-pypi-version/badge)](https://www.codefactor.io/repository/github/verbalinsurection/track-pypi-version)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=Verbalinsurection_track-pypi-version&metric=alert_status)](https://sonarcloud.io/dashboard?id=Verbalinsurection_track-pypi-version)
[![CircleCI](https://circleci.com/gh/Verbalinsurection/track-pypi-version/tree/master.svg?style=shield)](https://circleci.com/gh/Verbalinsurection/track-pypi-version/tree/master)
![Push pre-built action](https://github.com/Verbalinsurection/track-pypi-version/workflows/Push%20pre-built%20action/badge.svg)

Track Python package from requirements.txt, check if newer version exist in PyPI and provide update info.
Can be useful to notify or to trigger an up to date docker image build.

## Use

You can use built version on release-master branch

## Inputs

### `compush`

**Optionnal** Specify if commit and push need to be done. Default to `true`

### `reqfile`

**Optionnal** Path to `requirements.txt` file. Default to `/requirements.txt`

### `backup`

**Optionnal** Make a backup of requirements.txt if set to `true`. Default to `false`

## Outputs

### `commit`

If true, need to commit the new requirements.txt file

## Example of use

``` yaml
on:
  push:
    branches:
      - 'main'
      - 'master'
    schedule:
      - cron: '0 6 * * *'

jobs:
  check_dep:
    runs-on: ubuntu-latest
    name: Check python requirements file and update
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Check requirements.txt
        uses: Verbalinsurection/track-pypi-version@1.1.0
        id: checkr
        with:
          compush: 'true'
          backup: 'false'
          reqfile: './requirements.txt'
      - name: Get if update needed output
        run: echo ${{ steps.checkr.outputs.commit }}
```
