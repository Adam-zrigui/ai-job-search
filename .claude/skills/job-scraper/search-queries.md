# Search Queries for Job Scraper

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Shipped country-agnostic CLIs include `linkedin-search` and `freehire-search`; Danish demos and any skill you add with `/add-portal` are included the same way. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** - for portals without a CLI, company career pages, or when a CLI fails.

**Language scope:** search primarily in English for worldwide remote roles. Also consider German, French, Malay, Arabic, Turkish, or Italian postings only when the role's working-language bar is compatible with the declared levels in `CLAUDE.md` and `04-job-evaluation.md`.

## Search Sites

Primary:
- **linkedin.com/jobs** - LinkedIn job listings, remote worldwide
- **freehire.me** - Aggregated tech roles via the `freehire-search` CLI
- **RemoteOK / Wellfound / company career pages** - use WebSearch fallback where no CLI exists

Secondary:
- Direct Google searches with `site:` filters for known target companies

## Query Categories

Queries are grouped by priority and function. Use remote/worldwide filters where the portal supports them.

### Priority 1: Full-Stack SaaS Engineering

These match the strongest and most desired direction.

```
site:linkedin.com/jobs "Full Stack Engineer" remote TypeScript Next.js
site:linkedin.com/jobs "Full-Stack Developer" remote React Node.js
site:linkedin.com/jobs "Software Engineer" remote TypeScript PostgreSQL
site:linkedin.com/jobs "Next.js Developer" remote TypeScript
site:linkedin.com/jobs "React Developer" remote Node.js PostgreSQL
"Full Stack Engineer" "TypeScript" "Next.js" "remote"
"Full-Stack Developer" "React" "Node.js" "PostgreSQL" "remote"
```

### Priority 2: Healthtech and Medical Imaging

These match domain expertise from CoreVita.

```
site:linkedin.com/jobs healthtech "Full Stack Engineer" remote
site:linkedin.com/jobs "medical imaging" "React" remote
site:linkedin.com/jobs DICOM "frontend" remote
site:linkedin.com/jobs "healthcare SaaS" "TypeScript" remote
"healthtech" "Next.js" "TypeScript" "remote"
"DICOM" "React" "remote"
```

### Priority 3: Multi-Tenant SaaS and Workflow Platforms

Adjacent product engineering roles with strong overlap.

```
site:linkedin.com/jobs "SaaS Engineer" "multi-tenant" remote
site:linkedin.com/jobs "Workflow Automation" "Full Stack" remote
site:linkedin.com/jobs "Platform Engineer" TypeScript PostgreSQL remote
site:linkedin.com/jobs "Product Engineer" TypeScript Next.js remote
"multi-tenant SaaS" "TypeScript" "PostgreSQL" "remote"
"workflow platform" "React" "Node.js" "remote"
```

### Priority 4: Broader Technical Roles

Wider net for general technical roles.

```
site:linkedin.com/jobs "Frontend Engineer" React TypeScript remote
site:linkedin.com/jobs "Backend Engineer" Node.js PostgreSQL remote
site:linkedin.com/jobs "JavaScript Developer" remote
site:linkedin.com/jobs "Technical Consultant" SaaS remote
"React Developer" "TypeScript" "remote contractor"
"Node.js Developer" "PostgreSQL" "remote contractor"
```

## Location Filter

When evaluating results, verify location and work-rights constraints:
- **Ideal:** Fully remote, worldwide, contractor or employee roles that explicitly accept Tunisia-based applicants
- **Acceptable:** Remote EMEA, remote Europe/MENA, or remote roles with timezone overlap compatible with Tunisia
- **Borderline:** Hybrid roles requiring occasional travel only if employer explicitly accepts Tunisia-based remote work
- **Too far:** On-site or relocation-required roles without sponsorship or remote option

## Language Filter

Your working languages and levels are in `CLAUDE.md`'s Languages table. When filtering scraped results, apply `04-job-evaluation.md`'s Language Gate: a posting requiring a language you have not declared at all is excluded; a posting requiring a higher level than you declared in a language you do work in is not excluded, flag it clearly instead. Postings simply written in a language you do not work in, that do not require it on the job, are fine.

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- `/scrape healthtech` -> healthtech and medical imaging queries plus custom healthtech SaaS searches
- `/scrape next.js` -> full-stack SaaS engineering queries plus custom Next.js searches
