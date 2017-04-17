# GitHub Records Archiver

Backs up a GitHub organization's repositories and all their associated information for archival purposes.

## What it archives

* Git data (change history, tags, branches, etc.)
* Wikis (including change history)
* Issues and pull request (including comments, current state, etc.)
* Teams (including members and repository permissions)

## Requirements

1. Ruby
2. A GitHub [personal access token](https://github.com/settings/tokens/new) with `public_repo` and `repo` scope.

## Setup

1. `git clone https://github.com/benbalter/github-records-archiver`
2. `cd github-records-archiver`
3. `gem install bundler`
4. `bundle install`

## Usage

`bin/archive [ORGANIZATION] [ARCHIVE_DIR]`

You'll want to set the following environmental variable:

* `GITHUB_TOKEN` - Your personal access token

You *may* set the following environmental variables:

* `GITHUB_ARCHIVE_DIR` to specify the output directory. It will default to `./archive`.
* `GITHUB_ORGANIZATION` - The organization to archive if none is passed as an argument.

These can be passed as `GITHUB_TOKEN=123ABC GITHUB_ORGANIZATION=whitehouse bin/archive`.

You can also add the values to a `.env` file in the project's root directory, which will be automatically set as environmental variables. Providing arguments to the `./bin/archive` script will override the environment variables.

## Output

The script will create an `archive` directory, with a folder for each owner/organization containing all of the repoitories as subfolders.

Within each subfolder will be the repository content as a git repository.

If the repository has a Wiki, the wiki will be cloned as a `_wiki` subfolder, as a Git repository.

If the repository has issues or pull requests, it will create an `_issues` subfolder with each issue and its associated comments stored as both markdown (human readable) and JSON (machine readable).

The folder structure will look like this:

```
<ARCHIVE_DIR>/
├── <OWNER/ORG DIR 1>
│   ├── _teams
|   │   ├── team_one.md
|   │   ├── team_two.md
|   │   ├── ...
│   ├── <REPO 1>
|   │   ├── _wiki
|   │   ├── _issues
|   │   ├── .git
|   │   ├── ...
│   ├── <REPO 2>
│   ├── ...
├── <OWNER/ORG DIR 1>
│   ├── _teams
│   ├── <REPO 1>
│   ├── <REPO 2>
│   ├── ...
```
