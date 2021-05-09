# UMAI FRONTEND GIT BRANCHING STRATEGY

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

- Develop new feature

- Branch naming convention

- Anti-Patterns
