# play_ground

## Integration merge queue

Run **Actions > Integration Merge Queue > Run workflow**, then enter the branch
names in the required order, separated by commas:

```text
feature/A,feature/B,feature/C
```

The workflow creates an `integration/<run-id>` branch, merges each branch into
it in that order, and runs tests after every merge. A conflict or failed test
stops the workflow immediately. Only after every branch passes does it create a
pull request into `master` and enable auto-merge for that pull request.

GitHub's merge queue then runs the required checks on the final pull request
and merges it into `master` when all checks pass.

To enable the repository-side queue:

1. Open **Settings > Rules > Rulesets** (or the branch protection rule for
   `master`).
2. Require pull requests and require the `Test` status check.
3. Enable **Require merge queue** and select the desired merge method.

If a branch has conflicts, resolve them on that branch and run the workflow
again. The workflow does not resolve conflicts automatically because that could
change code without review.
