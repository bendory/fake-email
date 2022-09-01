# Fake Email

This repo demonstrates the fraudulent use of an unverified email that isn't mine
to push sourcecode to Git.

This is yet another attack vector by which a malicious user can misrepresent the
origin of sourcecode:

1. Create a GitHub account using a one-off email.
2. Fork a legitimate repo.
3. Clone the fork to a remote machine.
4. On the remote machine, run:
   * `git config user.email <email-of-user-to-impersonate>`
   * `git config user.name <name-of-user-to-impersonate>`
5. Commit malicious changes.
6. Push up to GitHub.
7. Propose a PR with malicious content.

## Demo

In the case of this repo, the [commit history](https://github.com/bendory/fake-email/commits/main) shows a [first commit](https://github.com/bendory/fake-email/commit/a25a11229686c607366eed7f201747de8a629a51) from Evil Hacker.
That was in fact me following the above setup to demonstrate the technique.

Even worse, I created a GitHub account for @TheonTully, and then I used the
above technique to push this commit using Theon's email address. In the
[commit history](https://github.com/bendory/fake-email/commits/main), the commit
is designated as his.
