# Notes

### Personal configs - not much use to anybody else

Notes on managing via a git bare repo 
```shell
git init --bare $HOME/.dotfiles
alias dotfiles='git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
dotfiles config --local status.showUntrackedFiles no
echo "alias dotfiles='git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'" >> $HOME/.bashrc
```

To add a new files
```shell
$dotfiles add .filename
$dotfiles commit -m "Add .filename"
$dotfiles push
$dotfiles status
```

To restore on new install 
```shell
alias dotfiles='git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
echo ".dotfiles" >> .gitignore
git clone --bare <git-repo-url> $HOME/.dotfiles
alias dotfiles='git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
dotfiles checkout
```

In the event that checkout fails with
error: 
```Shell
The following untracked working tree files would be overwritten by checkout:
    .bashrc
    .gitignore
    .etc
Please move or remove them before you can switch branches.
Aborting
```

Then do
```shell
mkdir -p .config-backup && \
config checkout 2>&1 | egrep "\s+\." | awk {'print $1'} | \
xargs -I{} mv {} .config-backup/{}
```
Then redo
```shell
dotfiles checkout
```
Add
```shell
config dotfiles --local status.showUntrackedFiles no
```
Read more https://www.atlassian.com/git/tutorials/dotfiles

## Packages Install
```shell
sudo pacman -S --needed - < packages-repository.txt
```

