# shared-workflows

1. [Purpose](#purpose)
2. [Shared workflows](#shared-workflows)
3. [Packages workflows](#packages-workflows)

## Purpose

The `shared-workflows` repo has been created in order to keep __consistency__ between the different Github Actions that are executed in the **packages** and **services** repositories.

### Shared workflows

#### `validate-pr-title.yaml`: 

* **When should be triggered:** 
``` 
on:
  pull_request:
    types: [opened, reopened, synchronize, edited]
```
* **Purpose:** Verify the created Pull Request title contains the required `HDA-[JIRA-ISSUE-NUMBER]` prefix.


### Packages workflows


#### `ci-package.yaml`: 

* **When should be triggered:** 
```
on:
  pull_request:
    types: [opened, reopened, synchronize]
```
* **Purpose:**
  * Verify Pull Request contains the required labels.
    * Any of: `[feature,fix,test]`
    * One of: `[major,minor,patch]`
  * Check linting & various test scripts.
    * `npm ci --ignore-scripts`
    * `npm run pkg-json-lint`
    * `npm run package-audit`
    * `npm run prettier`
    * `npm run lint`
    * `npm run tsc`
    * `npm run test`
  * Publish package to npm as an _alpha release_ using our [bumper/publisher action](https://github.com/hedia-team/autobump-and-publish).

#### `publish-release-package.yaml`: 

* **When should be triggered:** 
```
on:
  pull_request:
    branches:
      - master
    types: [closed]
```
* **Purpose:** Publish package to npm as an the _disributed version_ using our [bumper/publisher action](https://github.com/hedia-team/autobump-and-publish).
