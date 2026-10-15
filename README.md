# Use ExamDiff Pro as your Git diff and merge tool

Configuration for using [ExamDiff Pro](https://www.prestosoft.com/edp_examdiffpro.asp?ref=github-gitconfig) with `git difftool` and `git mergetool` on Windows, including Visual Studio and SourceTree, which use the same Git settings.

![Three-way merge in ExamDiff Pro](https://www.prestosoft.com/images/screenshots/edp_feat_merge.png)

## Quick setup

ExamDiff Pro is a built-in diff and merge tool in Git 2.9 and later, and Git finds the install folder by itself:

```
git config --global diff.tool examdiff
git config --global merge.tool examdiff
```

## Full setup

For display names in the merge panes and no prompts, copy the entries from [`gitconfig-examdiff`](gitconfig-examdiff) into your `~/.gitconfig`, or include the file:

```
git config --global include.path "C:/path/to/gitconfig-examdiff"
```

The entries assume the default install folder, `C:\Program Files\ExamDiff Pro`. Change the path if yours differs.

### Or with git config commands

```
git config --global diff.tool edp
git config --global diff.guitool edp
git config --global difftool.edp.cmd "\"C:/Program Files/ExamDiff Pro/ExamDiff.exe\" \"\$LOCAL\" \"\$REMOTE\" -nh"
git config --global difftool.prompt false

git config --global merge.tool edp
git config --global mergetool.edp.cmd "\"C:/Program Files/ExamDiff Pro/ExamDiff.exe\" -merge \"\$REMOTE\" \"\$BASE\" \"\$LOCAL\" -o:\"\$MERGED\" -dn1:\"Theirs\" -dn2:\"Base\" -dn3:\"Yours\" -dno:\"Output\" -nh"
git config --global mergetool.prompt false
git config --global mergetool.keepBackup false
git config --global mergetool.trustExitCode false
```

Inside the quotes, every `"` and `$` must be escaped with a backslash.

## Usage

```
git difftool                    # compare working tree changes, file by file
git difftool --dir-diff main    # compare the whole working tree with main as two folders
git mergetool                   # resolve merge conflicts in ExamDiff Pro's 3-way merge
```

`--dir-diff` opens one folder comparison instead of one window per file.

## Command-line options used

| Option | Meaning |
|---|---|
| `-nh` | Don't add the compared temporary files to ExamDiff Pro's history |
| `-merge Left Base Right` | Three-way merge |
| `-o:File` | Merge output file |
| `-dn1:` `-dn2:` `-dn3:` `-dno:` | Display names for the left, base, right, and output panes |

Options can start with `-` or `/`. Use `-` in Git configuration, because Git for Windows can rewrite arguments that start with `/` as paths.

## Other version control systems

Settings for TFS, Mercurial, Perforce, SVN (TortoiseSVN, Subclipse), ClearCase, and others are on the [version control integration page](https://www.prestosoft.com/edp_versioncontrol.asp?ref=github-gitconfig).

## About ExamDiff Pro

ExamDiff Pro is a visual file and folder comparison and merge tool for Windows by [PrestoSoft](https://www.prestosoft.com/?ref=github-gitconfig). [Download a free 30-day trial](https://www.prestosoft.com/edp_download.asp?ref=github-gitconfig). Three-way merge is part of the Master edition.
