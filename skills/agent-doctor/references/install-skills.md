# Install Skills

Before suggesting an install command, ask:

> Which agent harness should these skills be installed for?

Common options include:

- `codex`
- `claude`
- `cursor`
- `pi`

Use the user's chosen harness in the `--agent` flag.

## Matt Pocock Skills

Command shape:

```bash
npx --yes skills add mattpocock/skills --global --agent <HARNESS> --skill "*" --yes
```

Examples:

```bash
npx --yes skills add mattpocock/skills --global --agent codex --skill "*" --yes
npx --yes skills add mattpocock/skills --global --agent claude --skill "*" --yes
npx --yes skills add mattpocock/skills --global --agent cursor --skill "*" --yes
npx --yes skills add mattpocock/skills --global --agent pi --skill "*" --yes
```

## Repo Bootstrap

If adding skill installation to repo setup, use the repo's existing bootstrap mechanism.

Prefer a small helper function when installing more than one skill:

```bash
install_skill() {
    source="$1"
    skill="$2"
    label="${3:-$skill}"

    if npx --yes skills add "$source" --global --agent "$AGENT_HARNESS" --skill "$skill" --yes; then
        echo "$label was installed"
    else
        echo "failed to install $label" >&2
        exit 1
    fi
}

install_skill "mattpocock/skills" "*" "mattpocock-skills"
```

If the repo has no bootstrap path, give the user the one-off command instead of creating new setup machinery.
