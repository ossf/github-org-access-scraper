# github-org-access-scraper
GitHub lacks an API for listing an org's repos' access for non-team-based individuals, so, scrape it.

# Instructions

1. Clone this repo.
1. Log into github.com in Safari, with an account that has Maintain or Admin access on every repo in the given org (@ossf in this case), or, is an Owner
1. Visit any repo’s "Collaborator and Teams" page ([example](https://github.com/ossf/tac/settings/access)), and authenticate if needed - this ensures you’re in an "elevated privileges" window so the script can work unimpeded.
1. Open `org-scrape.scpt` in the Script Editor, and click the “play” button. You can use your computer while this is working, but please do not use Safari or you risk interrupting the flow.
1. This will produce a `ossf.json` file in this repo’s working directory.

To filter the data to repos that have individual-based access:
```sh
jq 'to_entries[] | select(.value.users | length > 0) | .value' ossf.json
```

To display only repo names that have individual-based access:
```sh
jq -r 'to_entries[] | select(.value.users | length > 0) | .value.repo' ossf.json
```