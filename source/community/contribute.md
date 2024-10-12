# Contributing

Thank you for considering making Universal BCOS even better! Your contributions are most welcome and appreciated.

If you would like to contribute to Universal BCOS, please fork, fix, commit and send a pull request for the maintainers to
review and merge into the main code base.

If you wish to submit more complex changes though, please check up with the core devs first on our gitter channel to
ensure those changes are in line with the general philosophy of the project and/or get some early feedback which can
make both your efforts much lighter and our review and merge procedures quick and simple.

## Branching

Repo branching strategic based on [git-flow](https://jeffkreeftmeijer.com/git-flow/).

- **master**: Latest stable branch.
- **dev**: Stable branch waiting for release(merge to master).
- **release-***: A branch for a new release.
- **feature-***: A developing branch of a new feature name.
- **bugfix-***: A branch to fix the bug name.

## How to contribute

### Issue

For issue tracking, visit our [GitHub Issues](https://github.com/WeTechHK/Universal-BCOS/issues).

### Fix bugs steps

1. **Fork** this repo
2. **Create** a new branch named **bugfix-xxxx** forked from your repo's **master** branch
3. **Fix** the bug
4. **Test** the fixed code
5. Make **pull request** back to this repo's **dev** branch
6. Wait the community to review the code
7. Merged(**Bug fixed**)

### Develop a new feature

1. **Fork** this repo
2. **Create** a new branch named **feature-xxxx** forked from your repo's **dev** branch
3. **Coding** in feature-xxxx
4. **Pull** this repo's dev branch to your feature-xxxx constantly
5. **Test** your code
6. Make **pull request** back to this repo's dev branch
7. Wait the community to review the code
8. Merged (**Feature added**)

## Coding guidelines

Please make sure your contributions adhere to our coding guidelines:

- Please check the clang-format file [.clang-format](https://github.com/WeTechHK/Universal-BCOS/blob/i18n/.clang-format) for code formatting rules.
- Please make sure your code is well-tested and well-documented.
- Pull requests need to be based on and opened against the `master` branch.
- Commit messages should be styled following the specification:
  - `<type>(scope): <subject>`, e.g. `<feat&fix>(protocol,pbft): add new protocol and fix bugs in pbft.`
  - type: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `chore`.
  - scope: the module/package name.
  - subject: short description.

## Code formatting

Code formatting rules are described by the [Clang-Format Style Options](https://clang.llvm.org/docs/ClangFormatStyleOptions.html) file [.clang-format](https://github.com/WeTechHK/Universal-BCOS/blob/i18n/.clang-format).
Please use the [clang-format](https://clang.llvm.org/docs/ClangFormat.html) (version 17.0 or higher recommended) tool to format your code _changes_ accordingly.

## Continuous integration

- Linux: GitHub Actions local runner within Ubuntu 22.04 LTS x86_64 and CentOS 7 arm64
- macOS x86_64/arm64
- Windows x86_64
