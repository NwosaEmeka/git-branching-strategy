# Umai Frontend Git Branching Strategy

This document provides a brief overview of the git branching strategy used by UMAI frontend team. The UMAI Frontend team uses continuous deployment strategy where features are deployed as soon they are ready.

- [Environments Overview](#environment-overview)
- [Branches Overview](#branches-overview)
- [Develop a new feature](#develop-a-new-feature)
- [Branch naming convention](#branch-naming-convention)
- [Anti Patterns](#anti-patterns)

## Environments Overview

In UMAI, we use the Development, Staging, and Production (DSP) enviroment model which is essential for providing the needed checks and balance in developing very robust and reliable software.

1. `Development (dev) environment -` This is the environment where features and changes made by developers are first deployed and tested. This environment is rapidly updated and contains the most recent version of the application.

2. `Staging environment -` The staging enviroment mirrors the production enviroment and it is used for final testing of the application and approval before going live.

3. `Production (prod) environment-` This is the currently released version of the application, accessible to the client/end users. This version preferably does not change except for during scheduled releases.

## Branches Overview

| Branch   | Base Branch | Description                                                                                                       |
| :------- | :---------- | :---------------------------------------------------------------------------------------------------------------- |
| `master` | N/A         | What is live in production (**stable**).<br/>A pull request is required to merge code into `master`.              |
| staging  | `master`    | The latest state of staging (**unstable**).<br>Codes in this branch are deployed to staging environment.          |
| `dev`    | `master`    | The latest state of development (**unstable**).<br>Deployed to the development environment.                       |
| feature  | `master`    | Cutting-edge features (**unstable**).<br>These branches are used for any maintenance features active development. |

---

## Develop new feature

1. Create a feature branch based off of `master`.

   ```
     $ git checkout master
     $ git checkout -b feature/UP-1234-git-branching-strategy
     $ git push --set-upstream feature/UP-1234-git-branching-strategy
   ```

:bulb: Make sure your master branch is up-to-date.

2. Develop the code for the new feature and commit as you go. This will provide a safety net should your hard drive / workstation crash.

   ```
   $ ... make changes
   $ git add -A .
   $ git commit
   $ git push
   ```

   :bulb: This repository makes use of [Commitizen](https://github.com/commitizen/cz-cli).
   When making a new commit just run `git commit` and you'll be prompted for the
   required fields.

   **DO:**

   `$ git commit` :heavy_check_mark:

   **DON'T:**

   `$ git commit -m 'commit message'` :x:

   :warning: Use only numbers when prompted to enter the ticket number

3. Navigate to the project on [Github](www.github.com) and open a pull request with the following branch settings:

   - Base: `master`
   - Compare: `feature/UP-1234-git-branching-strategy`

4. While waiting for the pull request review and approval, merge the feature branch with the following settings:

   - Base: `develop`
   - Compare: `feature/UP-1234-git-branching-strategy`

   **DO:**

   - Test the application locally before merging to develop branch :heavy_check_mark:

   **DON'T:**

   - Merge into master branch without pull request review and approval :x:

5. Deploy develop to development environment

   ```
   $ git checkout develop
   $ git pull
   $ npm run deploy:dev
   ```

6. If everything is good in development, merge the feature branch to staging and deploy to staging envrioment using `npm run deploy:staging`.

7. If everything is good in staging environment, and the Pull request has been reviewed and approved, merge the feature branch to master and deploy to production environment using `npm run deploy:production`.

---

## Branch naming convention

With the exception of `master` , `staging` and `develop`, branch should be named in relation to the JIRA ticket starting with a prefix of feature or hotfix, the ticket key and short title.

Branch names should use dashes to separate words of the name and should avoid any uppercase letters.

Choose a branch name that is concince and descriptive.

`feature/UP-1234-branch-naming-example`

---

## Anti-Patterns

### Don't develop a feature in `develop`. `staging` or `master` :x:

**Instead**: Create a feature branch off of `master`. When the feature is developed and tested, create a pull request. :heavy_check_mark:

**Why?**: All code changes require a code review and verification by our QA team. By opening a pull request, you signal to the rest of the team that your code is ready to be reviewed and tested.

---

### Don't merge your pull requests without at least +1 :x:

**Instead**: Ask a team member for a code review and to at least +1 your changes. :heavy_check_mark:

**Why?**: _Nobody is perfect._ Having said that, we always want to make sure at least one other team member reviews our code. Performance, readability, bugs, memory leaks, etc can all be impacted by code changes and sharing the responsibility to think about all that with a team member takes pressure off your shoulders.

---

**Keep calm and happy codding** :rocket: :rocket: :rocket:
