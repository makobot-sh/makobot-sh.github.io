I was trying to use the paprika-recipes python library, but it ended up not being what I wanted for this project.
Still, Here's what I did to get the library working, since it was a bit problematic

---

I was running into issues installing said library, following [this comment's](https://github.com/coddingtonbear/paprika-recipes/issues/9#issuecomment-1902786902) recommendation of [pre-seeding the wheel cache](https://github.com/yaml/pyyaml/issues/736#issue-1823089613) worked!

```bash
# create a constraint file that limits the Cython version to one that should work
echo 'Cython < 3.0' > /tmp/constraint.txt

# seed pip's local wheel cache with a PyYAML wheel
PIP_CONSTRAINT=/tmp/constraint.txt pip wheel paprika-recipes

# install PyYAML itself, or any other package(s) that ask for the PyYAML version you just built
pip install 'PyYAML==5.4.1'
```

After that, I had to install gnome-keyring since it doesn't come with WSL2 i think. I followed [this advice](https://github.com/jaraco/keyring/issues/566#issuecomment-1792544475):
```bash
# install gnome-keyring
sudo apt update && sudo apt install gnome-keyring

# add lines to .bashrc
echo '# wait for systemd --user dbus session and unlock keyring' >> ~/.bashrc
echo 'sleep 1' >> ~/.bashrc
echo 'eval $(echo -n db | gnome-keyring-daemon --unlock --replace 2> /dev/null)' >> ~/.bashrc

# reboot
```