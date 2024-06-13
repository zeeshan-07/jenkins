# Project Contribution Guide

This document provides the development guidelines for the project.

## The Development and Review Workflow

The project uses the ``git flow`` or ``git hf (hubflow)`` flow for
development. The details for it are as under:

1. clone the repository:

    ```bash
    git clone https://github.com/xFlowResearch/gsm-umts-whitelisting
    ```

2. Then initiate the workflow setup:

    ```bash
    git <flow/hf> init
    ```

3. Start working on a patch with a feature/bug-fix branch:

    ```bash
    git <flow/hf> feature start
    ```

    This will setup the required branching for you and you can start
    making your commits to the project.

    _Note_: Make sure you are on the 'develop' branch before performing the
    next steps.

4. Go to GitHub and create a pull request from your ``feature-x`` branch
to the upstream ``develop`` branch.

5. The PR will be reviewed and upon being ready, merged into the develop
branch.

6. You can then clean up your working directory on the development machine
with:

    ```bash
    git <flow/hf> feature finish
    ```

### Some tips for Git Based Development

- To synchronize remote and local branches, use the following command. This
will fetch the remote changes excluding the deleted branches from remote.
Additionally, this will also delete the local copies of the branches that have
been deleted on the remote.

    ```bash
    git fetch -p
    ```

- To delete a branch on a remote from your development machine, you can use:

    ```bash
    git push <remote> —delete <branch>
    ```

- To delete a branch on a local setup, use the following:

    ```bash
    git branch -d <branch>
    ```

More details on this development workflow and installation instructions,
you can look [here](https://datasift.github.io/gitflow/GitFlowForGitHub.html).

## Guidelines for Creating Patches

The following guidelines are to be strictly adhered to, in developing your
patches/bug-fixes for this project:

1. *Correct Commit Messages*
    The commit messages are to be written with the following guidelines:
    - The commit message to accurately describe the patch. No vague or
    generic language, must be specific, and technically explicit.
    - The subject line is to be written in present tense, and describe the
    entire patch succinctly.
    - An empty line between the subject line and following paragraphs, and
    between the paragraphs as well.
    - The subject line to be followed by 1 or more paragraphs that explain
    the patch further.
    - The lines to be rounded off to 80 characters in length.

2. *Logically Arranged Patch*
    - A patch must not have too much going on inside of it. It should only
    address one entity at a time. For instance, it's okay to have the same
    patch address code and doc update, but not two different bug fixes.

3. *Properly Sized Patch*
    - Patches that are too large will not be accepted, and the developer
    will be expected to divide the patch into smaller parts and create
    multiple patches, according to the guidelines above.

_Note: Patches that don't conform to these guidelines will NOT BE MERGED and
will fail the review._

## Guidelines for Code Review

You can ask other team members for additional review through GitHub. Your
patches will be reviewed by a core member of the team and change would
be requested as necessary. You will continue to follow the patch practices
for each change that you wil make (regarding commit messages etc.) and your
patch will be merged based on ``squash`` merge strategy, with the commit
message of the squashed commit a summary of all commit messages on the
commits of your ``feature/<x>`` branch.

For code reviewers, please keep in mind the following:

1. Anybody can review any PR! There are no restrictions on this as long as
the reviews are done with the best intentions and for good interest of the
project and team.
2. Your job is to assist the developer in improving their code. So, while
it is okay to point out shortcomings and mistakes, you should also provide
help in how to fix/improve it.
3. When generating the PR, make sure to link the issue(s), if any, fixed in
this PR. Issue can be linked by including the hash id of the issue e.g issue
 ``#xxx``.
4. Label your PR with all the relevant tags for ease of categorization. For
example, for a PR targeting a bug would be tagged with 'bug-fix' label.
5. You don't need to assign a reviewer for you PR. That will be handled
automatically by the OWNERS file.

## Guidelines for Issue Creation

If you want to report any bugs/issues in the code or documentation of the
project, you will use GitHub's Issues Section to create an issue.

For issue creation, please keep in mind the following:

1. Use pre-defined templates for writing Issue description.
2. Make sure all the information necessary to understand and reproduce the
issue is provided in the issue description.
3. Label each issue with the relevant tags/labels. For example, an issue
related to dashboard usability can be tagged with label 'dashboard'.
4. If the bug/issue is related to any PR, make sure to link that PR with the
issue by including the hash id of the PR e.g. PR #xxx.

## Guidelines for Code Testing

## Guidelines for Using the Infrastructure

You will have to contact the project lead to get a user account created on
the infrastructure machines, with appropriate privileges as necessary.

## Go Modules Packaging
### Go Module

A Module is a collection of Go packages versioned as one unit.
To start using go modules in your project
1. Initialize module 
    ```bash
    go mod init
    ``` 
    This introduces two files into a Go project
    1. go.mod (Contains module name, dependencies with versions)
    2. go.sum (Automatically generated file that lists the checksum of all dependecies. This checksum is used to validate the dependencies that none of them has been modified.)
2. Install dependency
    To add new dependency to your project use **go get** command. this command will also update go.mod file. use -u flag to download all child deps as well.
    ```bash 
    go get <dependency>
    ```
    ```bash
    go get -u <dependency> 
    ```
    - To Install
    Latest tag = go get github.com/<repo>/<module>
    Specific tag = go get github.com/<repo>/<module>@v1.6.2 
    Specific branch = go get github.com/<repo>/<module>@master
    Specific commit = go get github.com/<repo>/<module>@1bdf86b 
    - Note : Go get command can be used to upgrade dependency as well.
3. Unused dependency
    To remove unused dependencies use the following command. It also updated **go.mod** file.
    ```bash
    go mod tidy
    ```
4. Vendoring (Offline packaging)
    ```bash
    go mod vendor
    ``` 
    - go mod vendor commands create a vendor directory in project root directory and copies all packages needed to build and test the main module.
    - go mod vendor also creates the file vendor/modules.txt.
    - When vendoring is enabled, build commands like ``go build`` and ``go test`` load packages from the vendor directory instead of accessing the network or the local module cache.

5. List Module 
    To see a list of current module dependencies run the following command.
    ```bash
    go list -m all (if vendoring is not enabled)
    ```
    ```bash
    go list -mod=mod -m all (if vendoring enabled)
    ```
