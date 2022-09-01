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
