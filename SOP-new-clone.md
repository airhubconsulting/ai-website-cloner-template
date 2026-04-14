# SOP: Create a New Website Clone

Standard operating procedure for cloning a new website using the `ai-website-cloner-template` template repo.

---

## 1. Spin up a fresh repo from the template

- Go to https://github.com/airhubconsulting/ai-website-cloner-template
- Click **"Use this template" → "Create a new repository"**
- Name it descriptively (e.g. `netflix-help-clone`, `stripe-docs-clone`)
- Pick public/private → **Create repository**

## 2. Clone locally

```bash
cd "C:\Users\angel\OneDrive\File\GitHub\aiwebsiteclone"
git clone https://github.com/airhubconsulting/<new-repo-name>.git
cd <new-repo-name>
npm install
```

## 3. Open in Claude Code + run the skill

```bash
claude --chrome       # so Chrome MCP is connected for extraction
```

Inside Claude:

```
/clone-website <target-url>
```

The skill will: inspect the live site, extract design tokens, download assets, build all section components, and verify the build.

## 4. Verify

```bash
npm run dev           # open http://localhost:3000
npm run build         # should pass clean
```

## 5. Commit & push

Ask Claude to `/commit` and `/create-pr`, or manually:

```bash
git add .
git commit -m "clone <site-name>"
git push origin master
```

## 6. Deploy (optional)

- Go to https://vercel.com/new
- Import the new repo → **Deploy** (no env vars needed)

---

## Tips

- **One repo per clone** — keeps git history clean and lets each clone deploy independently
- If you want to update the template itself (new skill improvements, dependency bumps), push those to `airhubconsulting/ai-website-cloner-template` master; new clones created after will inherit the changes
- For Chrome MCP to work, make sure the Claude in Chrome extension is signed in before running `/clone-website`
- Start Claude with `--chrome` flag or the skill will error out on extraction

---

## Switching between existing clones

Each clone lives in its own repo folder under `C:\Users\angel\OneDrive\File\GitHub\aiwebsiteclone\`. To work on one:

```bash
cd "C:\Users\angel\OneDrive\File\GitHub\aiwebsiteclone\<clone-repo-name>"
npm run dev
```

If you kept multiple clones as branches inside a single repo instead, use:

```bash
git checkout clone/<name>
npm run dev
```

(Files will swap in/out of the working directory based on the active branch — they're not stored in separate subfolders.)
