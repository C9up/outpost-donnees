# outpost-donnees

Data that Outpost publishes, signed. No code lives here.

Each file is a release of this repository, whose tag is the file's name, and comes with its
`sshsig` signature (`.sig`) made by Outpost's data key, in the namespace `outpost-donnees`.
An Outpost fleet takes a file only when that signature holds, and keeps the most recent one.

| Release | File | Content |
|---|---|---|
| `cycle-de-vie` | `cycle-de-vie.txt` | the releases of Fedora, Debian and Ubuntu, their release day and end of support, from [endoflife.date](https://endoflife.date), published each month |

## Checking a signature yourself

```sh
echo 'outpost-donnees namespaces="outpost-donnees" ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBMuiJA98Hn2l4eo7xOw7jKOvKOFM4fJZq9PmdPizzMBNmLVCxbm6iUhdrhvF/feNErFv6tYoFjZJJ9NKSry5VZo=' > allowed_signers
ssh-keygen -Y verify -f allowed_signers -I outpost-donnees -n outpost-donnees \
  -s cycle-de-vie.txt.sig < cycle-de-vie.txt
```

## Format of `cycle-de-vie.txt`

```
outpost-cycle-de-vie 1
genere <Unix seconds>
<distribution>;<version>;<release, Unix seconds>;<end of support, Unix seconds, or empty>;<LTS: 1 or 0>
```
