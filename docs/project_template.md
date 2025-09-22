---
layout: default
title: "Coral Reef Anomaly Detection Sprint Playbook"
subtitle: "Innovation Summit 2025 Group 9 remote sensing workflow"
hero_image: assets/template/hero.svg
team_logo: assets/template/team-logo.svg
contact_slack: "#innovation-summit-2025-group-9"
contact_email: "group9@esiil.org"
repo_owner: "CU-ESIIL"
repo_name: "anomaly-detection-coral-reef-remote-sensing-innovation-summit-2025__9"
edit_path: "docs/project_template.md"
---

# {{ page.title }}

{{ page.subtitle }}

{% if page.hero_image %}
<img src="{{ page.hero_image }}" alt="Hero Image" />
{% else %}
<div style="width:100%;height:200px;background:#eee;display:flex;align-items:center;justify-content:center;">Set `hero_image` in front matter</div>
{% endif %}

{% if page.team_logo %}
<img src="{{ page.team_logo }}" alt="Team Logo" />
{% endif %}

[✏️ Edit this page](https://github.com/{{ page.repo_owner }}/{{ page.repo_name }}/edit/main/{{ page.edit_path }})
Slack: {{ page.contact_slack }} · Email: [{{ page.contact_email }}](mailto:{{ page.contact_email }})

*If this link 404s, set `repo_owner`, `repo_name`, and `edit_path` in the front matter.*

<nav style="position:sticky; top:0; background:#fff; padding:0.5rem; border-bottom:1px solid #ccc;">
[Day 1](#day1) · [Day 2](#day2) · [Day 3](#day3) · [Resources](#resources)
</nav>

## Contents
- [Day 1](#day1)
- [Day 2](#day2)
- [Day 3](#day3)
- [Resources](#resources)
- [FAQ](#faq)

<a id="day1"></a>
<details>
<summary><strong>Day 1 — Kickoff &amp; Page Setup</strong></summary>

### Objectives
- Form your team and assign roles.
- Draft a coral reef anomaly detection one-liner to align expectations.
- Swap in your hero and team images.
- Make and push your first commit.

### Steps
1. **Project One-liner** – In one sentence, describe what anomaly detection product you will deliver.
   *Example: *Detect and map coral reef thermal stress anomalies within 24 hours of new satellite imagery.*
2. **Edit this page** – Replace placeholders in the front matter above with real contact links, slack channel, and imagery.
3. **Team Roles** – Fill in the table:

```markdown
| Role  | Name | Responsibilities |
|---|---|---|
| Lead | _(your name)_ | Coordinates tasks, keeps time |
| Data | _(your name)_ | Sources imagery, documents ingest |
| Methods | _(your name)_ | Builds anomaly metrics & QA |
| Comms | _(your name)_ | Summarizes outcomes, crafts visuals |
```

4. **Swap Images** – Follow the Image Replacement Micro-Guide in [Resources](#resources) to update `hero_image` and insert a team photo.
5. **Commit & Push**
   - *Web editor:* click **✏️ Edit this page**, make changes, write a short commit message, and **Commit changes**.
   - *Clone route:* `git clone <repo-url>` → edit locally → `git add -A` → `git commit -m "initial setup"` → `git push`.

### Copy-paste Snippet
```markdown
Project one-liner: _(write it here)_
```

### Day 1 Checklist
- [ ] One-liner added.
- [ ] Team roles filled.
- [ ] Hero & team images swapped.
- [ ] Commit pushed to main.

</details>

<a id="day2"></a>
<details>
<summary><strong>Day 2 — Data &amp; Analysis Sandbox</strong></summary>

### Objectives
- Pick remote sensing feeds and document their source.
- Run a minimal anomaly detection workflow (Python or R).
- Save at least one result figure.
- Note what worked or failed.

### Steps
1. **Explore Data Libraries** – Start with these resources:
   - [NOAA Coral Reef Watch 5 km](https://coralreefwatch.noaa.gov/product/5km/) — thermal stress alerts.
   - [Microsoft Planetary Computer STAC](https://planetarycomputer.microsoft.com/) — Sentinel-2/HLS imagery.
2. **Select Data** – Choose one reef focus area and note its baseline period.
   *Example: *Lizard Island reefs, 2016–2024 Sentinel-2 L2A.*
3. **Set Up Tools** – Optional `gocmd` quickstart for Linux:

```bash
# Linux quickstart
GOCMD_VER=$(curl -L -s https://raw.githubusercontent.com/cyverse/gocommands/main/VERSION.txt); \
curl -L -s https://github.com/cyverse/gocommands/releases/download/${GOCMD_VER}/gocmd-${GOCMD_VER}-linux-amd64.tar.gz | tar zxvf -
./gocmd init

# Quick sanity check: can you list your home?
./gocmd ls i:/iplant/home/YOUR_USER
```

   > *(macOS uses a different tarball)*
4. **Minimal Analysis** – Run one of the snippets:

```python
# Python example: compute z-score anomalies
import xarray as xr

ds = xr.open_dataset("/path/to/coralreefwatch_sst.nc")
clim_mean = ds.sst.sel(time=slice("2013-01-01", "2022-12-31")).groupby("time.dayofyear").mean("time")
clim_std = ds.sst.sel(time=slice("2013-01-01", "2022-12-31")).groupby("time.dayofyear").std("time")
current = ds.sst.sel(time="2024-12-15").squeeze()
day = int(current.time.dt.dayofyear)
baseline = clim_mean.sel(dayofyear=day)
sigma = clim_std.sel(dayofyear=day)
z_score = (current - baseline) / sigma
z_score.to_netcdf("outputs/sst_anomaly_zscore.nc")
```

```r
# R example: visualize anomaly percentile
library(terra)
ras <- rast("/path/to/sentinel2_ndvi_anomaly.tif")
plot(ras, main = "Sentinel-2 NDVI anomaly percentile")
```

5. **Record Results** – Save a figure into `assets/results/`:

```markdown
<!-- Save figures into assets/results/ and reference below -->
![Thermal anomaly quicklook](assets/results/sst_anomaly.png)
```

6. **Document Learnings** – Jot down commands or pitfalls in the Results section.

### Day 2 Checklist
- [ ] Dataset chosen and cited.
- [ ] Analysis snippet executed.
- [ ] Figure saved to assets/results/.
- [ ] Notes captured in Results section.

</details>

<a id="day3"></a>
<details>
<summary><strong>Day 3 — Plan &amp; Share</strong></summary>

### Objectives
- Draft a plan-on-a-page for next steps.
- Create a short communication artifact (map, GIF, or dashboard).
- Prepare a demo for sharing with summit partners.
- Decide who will own follow-ups after the event.

### Steps
1. **Synthesize** – Craft 2–3 headline findings (Where? When? How strong?).
2. **Polish Visuals** – Annotate anomaly maps, add scalebars, and ensure captions describe significance.
3. **Package Deliverables** – Export a PDF brief or slide deck, share GitHub permalinks to key notebooks, and publish data pointers on the site.
4. **Plan Handoff** – Log immediate actions, open questions, and long-term opportunities in `documentation/group-notes.md`.
5. **Rehearse** – Practice a two-minute walkthrough of the homepage flow.

### Copy-paste Snippet
```markdown
**Headlines**
- _Headline 1_
- _Headline 2_
- _Headline 3_

**Next steps**
- _Immediate action_
- _If we had one more month_
- _Stakeholders to notify_
```

### Day 3 Checklist
- [ ] Headline findings recorded on Home.
- [ ] 2–3 polished visuals with captions.
- [ ] Brief PDF linked (if created).
- [ ] Next steps listed and owners assigned.
- [ ] Demo walkthrough rehearsed.

</details>

<a id="resources"></a>
## Resources
- [Group 9 notes & decisions](https://github.com/{{ page.repo_owner }}/{{ page.repo_name }}/blob/main/documentation/group-notes.md)
- [Image replacement micro-guide](assets/template/README.md)
- [CyVerse GoCommands reference](https://learning.cyverse.org/ds/gocommands/)
- [Sentinel-2 processing tips (ESA)](https://sentinel.esa.int/web/sentinel/user-guides/sentinel-2-msi/processing-levels/level-2)
- [Coral Reef Watch product descriptions](https://coralreefwatch.noaa.gov/product/5km/help.php)

<a id="faq"></a>
## FAQ

**What if we do not have a coral-specific dataset yet?**  
Start with NOAA Coral Reef Watch for context, then layer any available high-resolution imagery. Document the data gap and who is following up.

**Where do we keep drafts that are not ready for the website?**  
Use the `documentation/` folder or the CyVerse Group 9 community directory for working materials.

**Who can approve publishing sensitive information?**  
Check with your ESIIL mentor or reef management partners before sharing survey locations or sensitive observations.

**How do we keep track of versions?**  
Commit early and often, referencing issue numbers or notes so others understand updates. Use GitHub releases if you publish formal deliverables.
