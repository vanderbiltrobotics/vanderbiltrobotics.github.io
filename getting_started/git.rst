*************
Git Standards
*************
If you are unfamiliar with git, `here <https://www.freecodecamp.org/news/learn-the-basics-of-git-in-under-10-minutes-da548267cc91/>`_ is a 10 minute overview.

Using version control is critical to developing features in parallel on a single code base.
This page describes the standards we will be using to keep development organized and prevent 
overwrites from merging unorganized and/or out of date branches.

Using Github Pull Requests, Issues, and Projects
================================================
We use pull requests for merging changes from one branch to another to allow code reviews and improve organization of changes.
Below describes the flow of adding a new feature to our codebase: 

#. Open an issue to describe the new feature/work item
    - Issue should included concrete tasks needed to reach a deliverable 
    - Assign issues to people and add a deadline so that we have accountability/responsiblity
    - Add issue to relevant project board 
#. Create a feature branch off of :code:`staging` and then open a pull request into :code:`staging` once you have completed the tasks in the issue
    - Link your pull request to the issue it addresses
#. Have someone review your pull request (check good structure, clear naming conventions, etc.) and have them test your changes if possible
    - Address any comments from the reviewer and wait for them to read over your changes and resolve the comments before merging

Each GitHub project can be considered an overarching area of focus. We have an autonomy project that will contain tasks focused on achieving full autonomy.
Our main board for misceallaneous work items that need to get done is General. Using projects gives us a good view of what is being worked on by who and what needs to be done in the future while requiring little
maintenence on our part due to the nice automation features and ability to link pull requests to issues.

If you ever need something to work on, take a look at the projects and feel free to assign yourself to a work item or better yet, add a completely new work item! 

Branching Strategy
==================
The goal is to have an always working version of our code on :code:`main` that is always succesfully built in the continuous integration
pipeline. In order to keep :code:`main` always working, all development and integration work should be done off of :code:`staging`, which is occassionally pulled into :code:`main`. 

The exception is general (non package specific) documentation which can be branched from :code:`main` and then pulled in.

To keep an understanding of what is going on in different branches we use prefixs:

- :code:`feature/describe-feature` is used for big projects/enhancements that will take multiple weeks that other people might branch from to work on sub tasks
- :code:`poc/describe-concept` is used for proof-of-concepts that will not be merged into :code:`main`
- :code:`fix/describe-fix` is used for smaller fixes to :code:`staging` 

Merging Strategy
=================
- If there are a lot of minor commits, it is best to just squash and merge the branch upon reviewing the PR. Make sure to add a commit message that summarizes the changes.
- If the series of commits contain important information such as certain minor features/additions, then we want those commits on the branch being merged into so we would choose `rebase <https://git-scm.com/book/en/v2/Git-Branching-Rebasing>`_ and merge.
- Try to avoid creating a merge commits when completing PRs

.. note::
    After completing a PR, the branch should be deleted if it will not be used for future development. It can always be restored at a later point if needed. (Git)