# Discord Invite SEO & Google Indexing Research Lab

This project contains comprehensive research, empirical traces, and automated tools detailing how public non-expiring Discord invite links interact with Google Search, why they frequently fail to index, and how to reliably force Google to index and rank a Discord community.

---

## Key Files in This Repository

1. **[RESEARCH_REPORT.md](RESEARCH_REPORT.md)**:
   - Deep-dive technical research on Discord's URL architecture.
   - Analysis of HTTP response headers (`X-Robots-Tag: noindex` on `discord.gg`).
   - Analysis of `discord.com/robots.txt` and sitemaps.
   - Why Google considers standard invite pages "Thin Content" and drops them into *"Crawled - currently not indexed"*.
   - Architectural comparison between `discord.gg`, `discord.com/invite`, and official `discord.com/servers/` pages.

2. **[INDEXING_PLAYBOOK.md](INDEXING_PLAYBOOK.md)**:
   - Actionable step-by-step blueprints to get any Discord link or community indexed.
   - Protocol 1: Generating & verifying permanent non-expiring invites.
   - Protocol 2: The Direct Link backlink syndication protocol.
   - Protocol 3: The Branded Bridge Page protocol (instant Google Search Console indexation).
   - Protocol 4: Official Discord Server Discovery optimization.
   - Protocol 5: Directory aggregation network (Disboard, Top.gg).
   - Protocol 6: Long-tail content & forum indexing with AnswerOverflow.

3. **[discord_invite_inspector.py](discord_invite_inspector.py)**:
   - Python CLI utility to audit any Discord invite link.
   - Verifies redirect status (301/302), checks `X-Robots-Tag`, tests canonical URLs, checks OpenGraph tags, and queries Discord's public API to verify if `expires_at` is truly `null`.
   - **Usage**:
     ```bash
     python discord_invite_inspector.py <invite_code_or_url>
     ```

4. **[bridge_page_generator.py](bridge_page_generator.py)**:
   - Python CLI tool that fetches public metadata from Discord for any server and generates an SEO-optimized static landing page (`bridge_index.html`), `sitemap.xml`, and `robots.txt` with JSON-LD Schema markup.
   - Can be deployed to GitHub Pages, Cloudflare Pages, or Vercel for free, allowing instant submission to Google Search Console.
   - **Usage**:
     ```bash
     python bridge_page_generator.py <invite_code> <custom_domain_or_url>
     ```

---

## Core Findings Summary

- **Short Domain Directive**: `https://discord.gg/<code>` sends an `HTTP 301 Moved Permanently` to `https://discord.com/invite/<code>` with `X-Robots-Tag: noindex, nofollow...`. Google **never** indexes `discord.gg` URLs directly.
- **Canonical Destination**: `https://discord.com/invite/<code>` is allowed by `robots.txt`, but has no internal links from Discord and is not in any sitemap. Without high-authority external backlinks, Googlebot will never discover it.
- **Thin Content Trap**: The invite page contains only a single join button and metadata. Google algorithms frequently categorize it as thin content, leading to unstable indexation.
- **The Best Solution**: The Bridge Page pattern (used by Supabase, Midjourney, etc.) provides 100% control, instant Google Search Console indexing, and rich snippet rankings.
