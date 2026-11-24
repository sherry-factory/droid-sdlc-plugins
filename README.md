# droid-sdlc-plugins

Droid plugin marketplace for the Factory Workstreams agentic SDLC demo. Each stage of the pipeline (Product, Spec, Engineering) runs on its own agent profile, and each profile installs only its own plugin from this marketplace.

| Plugin | Stage | Skills | Hooks |
|---|---|---|---|
| `sdlc-product` | PRD | `enhance-prd` | Blocks `git push`, `gh pr create`, `gh pr merge` and PR/ref writes through `gh api` |
| `sdlc-spec` | Spec | `write-spec` | Same block as `sdlc-product` |
| `sdlc-eng` | Implement and validate | `implement`, `validate` | None |

The hook matches the command string the Execute tool submits, so it also covers path-prefixed and option-prefixed forms (`/usr/bin/git push`, `git -C /repo push`, `git -c a=b push`, `FOO=1 git push`, `bash -c "git push"`) and anything chained after `&&`, `;`, `|` or `$(`. A `gh api` call is blocked only when it targets `pulls` or `git/refs` *and* carries a write method (`-X POST`, `--method PATCH`, ...) or a field flag (`-f`, `-F`, `--field`, `--raw-field`, `--input`), so reads such as `gh api repos/o/r/pulls/1/comments` still work. It prefers blocking when a command is ambiguous, so it also stops harmless commands that quote the phrase, such as `grep -r "git push" .`.

The hook is a backstop. The real control for the Product and Spec stages is a read-only GitHub token on their agent profiles, plus branch protection on the app repository.

## Register the marketplace

Factory web app, Settings, Enterprise Controls, Plugins (managed settings):

```json
{ "extraKnownMarketplaces": { "droid-sdlc-plugins": { "source": { "source": "github", "repo": "sherry-factory/droid-sdlc-plugins", "ref": "main" } } } }
```

Do not enable these plugins org-wide. Add `sdlc-product@droid-sdlc-plugins`, `sdlc-spec@droid-sdlc-plugins` or `sdlc-eng@droid-sdlc-plugins` to the matching agent profile only.

## Layout

```text
.factory-plugin/marketplace.json
plugins/sdlc-product/.factory-plugin/plugin.json
plugins/sdlc-product/skills/enhance-prd/SKILL.md
plugins/sdlc-product/hooks/hooks.json
plugins/sdlc-spec/.factory-plugin/plugin.json
plugins/sdlc-spec/skills/write-spec/SKILL.md
plugins/sdlc-spec/hooks/hooks.json
plugins/sdlc-eng/.factory-plugin/plugin.json
plugins/sdlc-eng/skills/implement/SKILL.md
plugins/sdlc-eng/skills/validate/SKILL.md
```
