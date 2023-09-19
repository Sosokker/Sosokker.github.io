## How does it work?

1. Create a new Branch
2. Make changes and add Commits
3. Open a Pull Request
4. Review
5. Deploy
6. Merge

### Create a new Branch

**Branching** is key concept in Git. And it works with the rule that
<p style='text-align: center;color:yellow'>The master branch is ALWAYS deployable</p>
To try something new or experiment, create a new branch! so It will not affect main branch

When main branch is ready, reviewed + discussed and merge to main branch

(Almost always make new branch from the master branch)


```mermaid
flowchart LR

    A(New Branch) -->|Pull Request| B(Review)
    B --> C(Merge to main)
```

### Make Changes and Add Commits

When you reach a small milestone after do a bit of adding, editing and deleting files then commit it.
### Open a Pull Request

Pull Request notifies people that you have changes and ready for other to review.

### Review

When a Pull Request is made, it can be reviewed by whoever has the proper access to the branch. This is where good discussions and review of the changes happen.

If you receive feedback and continue to improve your changes, you can push your changes with new commits, making further reviews possible.

### Deploy

When the pull request has been reviewed and everything looks good, it is time for the final testing. GitHub allows you **to deploy from a branch for final testing in production** before merging with the master branch.

If any issues arise, you can undo the changes by deploying the master branch into production again!

### Merge

Merge the code into the main branch








