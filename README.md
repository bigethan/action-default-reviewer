# Update Assignee to match reviewer

Our team uses the github auto assign of rereviewers based on a team, but much github functionality is based on the assignee, so this syncs the two

Credit to https://github.com/pullreminders/assignee-to-reviewer-action.git for the code, this reverses the implementation.

## Usage

This Action subscribes to [Pull request events](https://help.github.com/en/articles/events-that-trigger-workflows#pull-request-event-pull_request) specifically the `review_requested` and `review_request_removed` events which fire whenever the reviewer changes.

```workflow
name: Assign reviewers based on assignees
on:
  pull_request:
    types: [review_requested, review_request_removed]

jobs:
  reviewer_to_assignee:
    runs-on: ubuntu-latest
    steps:
      - name: Reviewer to Assignee
        uses: bigethan/action-sync-assignee-with-reviewer
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

```

Note that the workflow for `pull_request` events will be triggered by default only for `opened`, `synchronize` or `reopened` activity types. For other, events the `types` keyword must be used.

## License

The Dockerfile and associated scripts and documentation in this project are released under the [MIT License](LICENSE).
