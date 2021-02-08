# ssh-example

This is the first step in setting up a new machine.

## Installation

SSH into the new machine, with agent forwarding enabled, from a client machines that can access GitHub via SSH.

```bash
# in ~

git clone git@github.com:cdzombak/ssh-example.git
rm -rf .ssh
mv ssh-example .ssh
./.ssh/fix-permissions.sh
```

### Generate Keys

#### Yubikey w/[`yubikey-agent`](https://github.com/FiloSottile/yubikey-agent)

```bash
yubikey-agent -setup
```

Add the resulting public key, with comment, to `authorized_keys`, `public_keys/`, and to `id_XXX_sk.pub`.

### Enable config templates as needed

- `homedir-ssh-auth-sock`: Set `IdentityAgent` to the persistent/updated SSH agent socket symlink in `~/.ssh/sock`. Use this on servers that don't have their own SSH keys.
- `yubikey-agent`: set `IdentityAgent` to use [`yubikey-agent`](https://github.com/FiloSottile/yubikey-agent). Use this on clients which have SSH keys stored on Yubikeys.

## Configuration

To use one of the local config templates (in this example, `yubikey-agent`, for a client machine with attached Yubikey):

```bash
cd ~/.ssh/config.local
ln -s ../config.templates/yubikey-agent .
```
