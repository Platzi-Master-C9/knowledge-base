# C9 RFCs

Many changes, including bug fixes and documentation improvements can be
implemented and reviewed via the normal GitHub pull request workflow.

Some changes though are "substantial", and we ask that these be put
through a bit of a design process and produce a consensus among the C9 team.

The "RFC" (request for comments) process is intended to provide a
consistent and controlled path for new features to enter the project.

[Active RFC List](https://github.com/Platzi-Master-C9/knowledge-base/pulls)

## When to follow this process

You should consider using this process if you intend to make "substantial"
changes to any C9 project. Some examples that would benefit
from an RFC are:

  - A new feature that creates new API surface area, and would
     require a feature flag if introduced.
  - The removal of features that already shipped as part of the release
     channel.
  - The introduction of new idiomatic usage or conventions, even if they
     do not include code changes to Platzily itself.

Some changes do not require an RFC:

  - Rephrasing, reorganizing or refactoring
  - Addition or removal of warnings
  - Additions that strictly improve objective, numerical quality
  criteria (speedup, better browser support)

## What the process is

In short, to get a major feature added to C9 projects, one usually first gets
the RFC merged into the RFC repo as a markdown file. At that point the RFC
is 'active' and may be implemented with the goal of eventual inclusion
into C9 projects.

- Fork the RFC repo https://github.com/Platzi-Master-C9/knowledge-base
- Copy `0000-template.md` to `RFCs/accepted/0000-my-feature.md` (where 'my-feature' is descriptive. Don't assign an RFC number yet).
- Fill in the RFC. Put care into the details: **RFCs that do not present convincing motivation, demonstrate understanding of the impact of the design, or are disingenuous about the drawbacks or alternatives tend to be poorly-received**.
- Submit a pull request. As a pull request the RFC will receive design feedback from the community, and the author should be prepared to revise it in response.
- Build consensus and integrate feedback. RFCs that have broad support are much more likely to make progress than those that don't receive any comments.
- An RFC can be modified based upon feedback from the team or community.
- An RFC may be rejected by the team after public discussion has settled and comments have been made summarizing the rationale for rejection. A member of the team should then close the RFCs associated pull request and the RFC will become 'rejected'.
- An RFC may be accepted. A team member will merge the RFCs associated pull request, this mean that the RFC will be accepted and it will be waiting for approval, at this point the RFC will become 'accepted'.

## The RFC lifecycle

Once a RFC becomes active a discussion process will start and have place in the RCF PR.

Once an RFC becomes accepted, it can be implemented submiting a PR with the feature to the project repository.

Furthermore, the fact that a given RFC has been accepted and is 'active' implies nothing about what priority is assigned to its implementation.

Modifications to active RFCs can be done in followup PRs. We strive to write each RFC in a manner that it will reflect the final design of the feature; but the nature of the process means that we cannot expect every merged RFC to actually reflect what the end result will be at the time of the next major release; therefore we try to keep each RFC document somewhat in sync with the language feature as planned, tracking such changes via followup pull requests to the document.

After the implementation of the RFC is donde, a new PR must be submited into this repository to change the status of the RFC from accepted to implemented. After this is done, any enhacement or improvement related to the feature must come with another RFC.

## Implementing an RFC

The author of an RFC is not obligated to implement it. Of course, the RFC author (like any other developer) is welcome to post an implementation for review after the RFC has been accepted.

If you are interested in working on the implementation for an 'active' RFC, but cannot determine if someone else is already working on it, feel free to ask (e.g. by leaving a comment on the associated issue).

## Contributing

Thank you for being here, we're really happy you decided to create a RFC.

Before you contribute to the project please make sure to read all items below.

* [Contributing Guide](https://github.com/Platzi-Master-C9/knowledge-base/RFCs/CONTRIBUTING.md)
* [Request For Comments additional resources](https://platziteam.notion.site/Request-for-comments-RFC-52ff9f80e16a4b7da582ca48c30cfb1e)

## Inspiration

C9 RFC process owes its inspiration to the [React RFC process](https://github.com/reactjs/rfcs) and [Rust RFC process](https://github.com/rust-lang/rfcs).