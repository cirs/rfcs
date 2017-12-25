Contributor Guidelines
===
[Contributor Guidelines]: #contributor-guidelines

# When you need to follow this process
[When you need to follow this process]: #when-you-need-to-follow-this-process

You need to follow this process if you intend to make "substantial" changes to
Cirs or the RFC process itself. What constitutes a "substantial" change is may
include the following.

  - Any semantic change to the C language implementation that is not a bugfix.
  - Removing language features, including those that are feature-gated.
  - Changes to the interface between the compiler and libraries, including lang
    items and intrinsics.

Some changes do not require a RFC:

  - Rephrasing, reorganizing, refactoring, or otherwise "changing shape does
    not change meaning".
  - Additions that strictly improve objective, numerical quality criteria
    (warning removal, speedup, better platform coverage, more parallelism, trap
    more errors, etc.)
  - Additions only likely to be _noticed by_ other developers-of-cirs,
    invisible to users-of-cirs.

If you submit a pull request to implement a new feature without going through


# What the process is
[What the process is]: #what-the-process-is

In short, to get a major feature added to Cirs, one must first get the RFC
merged into the RFC repository as a markdown file. At that point the RFC is
"active" and may be implemented with the goal of eventual inclusion into Cirs.

  - Fork the RFC repo [RFC repository]
  - Copy `0000-template.md` to `text/0000-my-feature.md` (where "my-feature" is
    descriptive. don't assign an RFC number yet).
  - Submit a pull request. As a pull request the RFC will receive design
    feedback from the larger community, and the author should be prepared to
    revise it in response.
  - The RFC pull request is discussed, as much as possible in the
    comment thread of the pull request itself.
  - RFCs rarely go through this process unchanged, especially as alternatives
    and drawbacks are shown. You can make edits, big and small, to the RFC to
    clarify or change the design, but make changes as new commits to the pull
    request, and leave a comment on the pull request explaining your changes.
  - Specifically, do not squash or rebase commits after they are visible on the
    pull request.
