# GO Science Skill for Claude Code

> **Your personal AI assistant for Akshar Yadav's Get Overbooked (GO) program.**
> Built for GO program students. Works inside Claude Code on any account.

---

## What Is This?

This is a **Claude Code skill** — a special plugin that gives Claude deep knowledge of AY's GO marketing system. Once installed, you can ask Claude anything about the GO program and it will always answer using the correct frameworks, the right terminology, and AY's actual teaching.

**What it knows:**
- All 13 steps of the GO program — explained exactly as AY teaches them
- MCB formula, 4-Phase structure (both Educational and Sales), KIT strategy, ARC triangle, IRO (Seller C story), Smart Buyer Journey, TYO/TYE/TYB, NDFF, FE/BE, BE Fixing
- 83 types of Thought Content for KIT
- AY's key stories: Horse & Dog, Three Seller story (IRO), Drug Boy story
- All terminology: MoA, GKP, Hara Chara, Brutal KIT, CMA, SBJ stages, Objection Strips, etc.

**What it can do for you:**
1. **Validate** — Check if a message, proposal, or piece of content aligns with AY science
2. **Generate** — Create MCBs, KIT messages, 4-Phase outlines, IROs, or any GO-aligned content
3. **Analyze** — Tell you which emotions a message triggers and whether the influence is correct
4. **Audit** — Run a full 13-step GO audit on your business
5. **Explain** — Break down any GO concept in plain language with AY's actual context
6. **Research** — Apply GO frameworks specifically to your industry and MoA

---

## Who Is This For?

Anyone who has done or is doing **Akshar Yadav's GO program** (Get Overbooked) and wants an AI assistant that actually understands the science — not just generic marketing advice.

The skill uses a multi-agent architecture:
- **13 Step Agents** — one specialist per step (MCB, 4-Phase, KIT, IRO, etc.)
- **Research Agent** — looks up industry-specific context for your business
- **Audit Agent** — checks every response against the knowledge base before delivering it
- **Simplification Agent** — makes sure answers are clear and scannable

---

## Requirements

### Core (required for all features)

| Requirement | Windows | Mac / Linux | Notes |
|------------|---------|------------|-------|
| **Claude Code** | ✅ Required | ✅ Required | Must be run at least once so the `.claude` folder exists |
| **PowerShell 5.1+** | ✅ Required | — | Comes pre-installed on Windows 10/11 |
| **Python 3** | — | ✅ Required | Pre-installed on most Macs and Linux; check with `python3 --version` |
| **Git** | Optional | Optional | Only needed if downloading from GitHub instead of the ZIP |

### KIT System (required for `/go-science kit` commands)

| Requirement | Notes |
|------------|-------|
| **Google Account** | Needed for Google Sheets — the primary data layer for the KIT database |
| **Google Sheet** | Create one at sheets.google.com before your first `/go-science kit setup` |
| **Google Sheets MCP** | Claude Code plugin that lets Claude read/write your KIT database. See setup note below. |
| **Internet access** | The Research Agent searches for industry news, social profiles, and festival context |

> **Google Sheets MCP Setup:** To connect Claude Code to Google Sheets, you need to add the Google Sheets MCP to your Claude Code settings. Without it, the KIT system falls back to local CSV files — functional, but you won't be able to view or edit the database in a spreadsheet. Run `/go-science kit upgrade` at any time to migrate from CSV to Google Sheets once the MCP is connected.

### Optional but Useful

| Tool | Why It Helps |
|------|------------|
| **VS Code** | View and edit knowledge base files, SKILL.md, kit-knowledge.md |
| **Python 3 (Windows)** | Enables running the analysis scripts if you need to inspect the Excel database |

---

## Installation — Windows

1. **Extract** the ZIP file anywhere on your computer (e.g., Desktop)
2. **Double-click `install.bat`** ← easiest, works on all Windows machines
   - A terminal window will open, run the installer, and wait for you to press a key
   - That's it
3. **Restart Claude Code** (close and reopen)
4. Done — the skill is active

> **Why `install.bat` and not `setup.ps1` directly?**
> Windows blocks unsigned PowerShell scripts by default (you'll see a red "cannot be loaded" error if you try to run `setup.ps1` directly). The `install.bat` file bypasses this automatically — no settings change needed, nothing to configure.

> **If `install.bat` also gets blocked** (rare — some corporate machines), right-click `install.bat` → **Run as Administrator**. If that still fails, open PowerShell and run:
> `powershell -ExecutionPolicy Bypass -File "C:\path\to\go-science-skill\setup.ps1"`

---

## Installation — Mac / Linux

1. **Extract** the ZIP file anywhere (e.g., `~/Desktop/go-science-skill`)
2. **Open Terminal**
3. Navigate to the extracted folder:
   ```bash
   cd ~/Desktop/go-science-skill
   ```
4. Make the script executable and run it:
   ```bash
   chmod +x setup.sh
   ./setup.sh
   ```
5. **Restart Claude Code**
6. Done — the skill is active

---

## Manual Installation (if scripts don't work)

If the setup scripts don't work for any reason, you can install manually in 4 steps.

**Step 1 — Copy the files**

Copy the `marketplace/` folder from this ZIP to:
- **Windows:** `C:\Users\YOUR_USERNAME\.claude\plugins\marketplaces\go-science\`
- **Mac/Linux:** `~/.claude/plugins/marketplaces/go-science/`

Copy the `knowledge/` folder to the same location:
- **Windows:** `C:\Users\YOUR_USERNAME\.claude\plugins\marketplaces\go-science\knowledge\`
- **Mac/Linux:** `~/.claude/plugins/marketplaces/go-science/knowledge/`

**Step 2 — Fix the knowledge base path in SKILL.md**

Open the file:
`go-science/skills/go-science/SKILL.md`

Find this line:
```
**Knowledge Base location:** `{{KNOWLEDGE_BASE_PATH}}`
```

Replace `{{KNOWLEDGE_BASE_PATH}}` with the actual full path to `ay-science-knowledge.md`:
- **Windows example:** `C:\Users\John\.claude\plugins\marketplaces\go-science\knowledge\ay-science-knowledge.md`
- **Mac/Linux example:** `/Users/john/.claude/plugins/marketplaces/go-science/knowledge/ay-science-knowledge.md`

**Step 3 — Update settings.json**

Open `~/.claude/settings.json` (create it if it doesn't exist).

Add these two sections (merge with existing content — don't overwrite):

```json
{
  "pluginMarketplaces": {
    "go-science": {
      "source": {
        "source": "directory",
        "path": "/Users/YOUR_USERNAME/.claude/plugins/marketplaces/go-science"
      }
    }
  },
  "enabledPlugins": {
    "go-science@go-science": true
  }
}
```

> On Windows, use double backslashes in the path: `"C:\\Users\\John\\.claude\\plugins\\marketplaces\\go-science"`

**Step 4 — Restart Claude Code**

---

## How to Use

Once installed, type `/go-science` in any Claude Code session to activate the skill.

### Quick Examples

**Check if your message follows AY science:**
```
/go-science validate "How to grow your business 10x without spending on ads — reply YES to know more"
```

**Create an MCB for your business:**
```
/go-science generate MCB for a CA firm targeting small business owners in Pune
```

**Analyze the emotion in a message:**
```
/go-science analyze "We've been in business for 20 years and serve 500+ clients across India"
```

**Run a full 13-step audit:**
```
/go-science audit I run a digital marketing agency, we mostly get clients through referrals, have no fixed process, and charge 15k/month
```

**Explain a concept:**
```
/go-science explain what is TYO activation
```

**Get industry-specific help:**
```
/go-science research I'm a wedding photographer targeting HNI couples — help me build my MCB
```

### Natural Language Works Too

You don't need to type the exact command. Just ask naturally:
- "What's the difference between the Educational 4-Phase and the Sales 4-Phase?"
- "Help me write a KIT message for my past clients who haven't bought in 6 months"
- "I know what to do but I keep procrastinating on doing CMA — what's wrong?"
- "Is this proposal following the correct GO sequence?"

---

## The 13 Steps (Quick Reference)

| Step | Name | What It Builds |
|------|------|---------------|
| 1 | Signature MCB | Your core curiosity-generating message |
| 2 | Two 4-Phases + Objection Strips | Educational + Sales presentations |
| 3 | TYO Activation | Activating your existing database |
| 4 | IRO | Your irresistible, risk-free entry offer |
| 5 | 4-Phase Based Booklet | Your authority document |
| 6 | Ideal MoA Clarification | Defining your exact ideal client |
| 7 | NDFF Clarification | Understanding your MoA's psychology |
| 8 | Smart Buyer Journey | Mapping every stage of your sales process |
| 9 | FE / BE | Front-end and back-end offer structure |
| 10 | Marketing Kit | All collateral for every stage |
| 11 | KIT Strategy | 50–60 annual touchpoints with your database |
| 12 | GO Sequence | 100% understanding + implementation |
| 13 | BE is Fixed | Your internal identity aligned with marketing & sales |

---

## Key Terms Glossary

| Term | Meaning |
|------|---------|
| **MCB** | Mass Control Bed — curiosity message based on secret desire |
| **MoA** | Market of Avatar — your ideal client |
| **NDFF** | Needs, Desires, Fears, Frustrations — extracted from MoA Interviews |
| **ARC** | Affinity, Reality, Communication — foundation of all marketing |
| **KIT** | Keep In Touch — 50–60 touchpoints/year nurturing system |
| **TYO** | Traffic You Own — your existing database |
| **TYE** | Traffic You Earn — organic referrals |
| **TYB** | Traffic You Buy — ads, cold outreach |
| **IRO** | Irresistible Offer — zero-risk entry point |
| **FE/BE** | Front End / Back End offer structure |
| **GKP** | Gannay ka Powder — total lifetime value per client |
| **SBJ** | Smart Buyer Journey — 4-stage path from stranger to client |
| **CMA** | Core Marketing Activity — consistent outbound pipeline activity |
| **TC** | Transformative Content (4-Phase) / Thought Content (KIT) |
| **BE Fixing** | Aligning your internal identity with marketing, sales & implementation |

---

## Troubleshooting

**Skill not appearing after installation:**
- Make sure you fully restarted Claude Code (quit and reopen, don't just reload)
- Check that `settings.json` has both `pluginMarketplaces` and `enabledPlugins` entries
- Verify the `marketplace_dir` path in `settings.json` is correct for your username

**"Knowledge base not found" error:**
- Open `SKILL.md` (in `go-science/skills/go-science/`) and check the path on the `Knowledge Base location:` line
- Make sure `ay-science-knowledge.md` exists at that exact path

**PowerShell "cannot be loaded / not digitally signed" error:**
- Use `install.bat` instead of running `setup.ps1` directly — double-click it and it handles this automatically
- If `install.bat` is also blocked: right-click → Run as Administrator
- Last resort: open PowerShell and run `powershell -ExecutionPolicy Bypass -File ".\setup.ps1"`

**Need to reinstall or update:**
- Simply run the setup script again — it overwrites existing files safely

---

## What's Inside This Package

```
go-science-skill/
├── README.md                          ← You are here
├── install.bat                        ← Windows installer (double-click this)
├── setup.ps1                          ← Windows installer script (called by install.bat)
├── setup.sh                           ← Mac/Linux installer
├── marketplace/
│   ├── .claude-plugin/
│   │   └── marketplace.json           ← Skill registration
│   └── skills/
│       └── go-science/
│           ├── SKILL.md               ← The skill (5 agent layers, 8 commands + KIT system)
│           ├── kit-knowledge.md       ← KIT science: hooks, field gate, WIIFT, segments
│           └── my-go-context.md       ← Your personal business context (fill this in)
└── knowledge/
    ├── ay-science-knowledge.md        ← Full GO program knowledge base
    └── landing-page-knowledge.md      ← Landing page structure + 9-site analysis
```

---

## Credits

- **Program:** Get Overbooked (GO) by Akshar Yadav
- **Skill built by:** Subhajit Ghosh
- **For:** GO program students

---

*This skill is for personal and educational use by GO program students. The knowledge base is based on the GO program curriculum taught by Akshar Yadav.*
