# Fake Email

This repo demonstrates the fraudulent use of an unverified email that isn't mine
to push source code to Git.

This is yet another attack vector by which a malicious user can misrepresent the
origin of source code:

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

In the case of this repo, the [commit history](https://github.com/bendory/fake-email/commits/main) shows a [first commit](https://github.com/bendory/fake-email/commit/a25a11229686c607366eed7f201747de8a629a51)
from Evil Hacker.  That was in fact me following the above setup to demonstrate
the technique. Evil Hacker doesn't exist and the email used for the commit is
completely fictional.

But it gets worse. I created a GitHub account for [@TheonTully](https://github.com/TheonTully), and then I used the
above technique to push this commit using Theon's email address. In the
[commit history](https://github.com/bendory/fake-email/commits/main), the [commit](https://github.com/bendory/fake-email/commit/cfcfda0a48a5d9a1ae513ba0ac21209a68b2c85e) is designated as his, complete with a link to his user profile.

In a multi-commit PR sent by me to an OSS project, I can misrepresent Theon's authorship of one or more commits.
The PR reviewer may not even notice, or may assume that Theon was in fact the contributor. Note that my forged commit
even appears in Theon's commit history on his [profile page](https://github.com/TheonTully)!

## Preventing this Attack

This attack can be prevented by requiring [signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification) on commits. Yes, this creates some friction for developers; you'll
have to decide if the trade-off is right for your repository.

## Additional Reading

GitHub helpfully [documents this behavior as a feature](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/setting-your-commit-email-address#setting-your-email-address-for-every-repository-on-your-computer), stating: "Set an email address in Git. You can use your GitHub-provided noreply email address **or any email address.** (emphasis added)

This behavior is of course against [GitHub Terms of Service](https://docs.github.com/en/site-policy/github-terms/github-terms-of-service), but since when did ToS stop a malicious hacker?

## Background and Notes

After setting up this repo, I discovered some prior art:

- https://github.com/azeemshaikh38/tensrflow/commits/main) attributes commits to real GitHub users and also typo squats on Tensorflow.
- https://news.ycombinator.com/item?id=30503148 has a discussion from ~6m ago

Note that at its root, this is an issue with `git`, not GitHub -- but GitHub could provide options to require signed commits
and better enforcement of identity verification. At a minimum, if user A pushes commits to GitHub that are attributed to user B's
verified GitHub email (or includes user B's changes in user A's PR to some other repo), GitHub could notifify user B that this
event occured!
