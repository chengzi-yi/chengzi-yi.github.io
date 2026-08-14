# Chengzi Yi — Personal Website

This repository is the source for [chengzi-yi.github.io](https://chengzi-yi.github.io). It is a Jekyll site published through GitHub Pages. The original theme documentation is preserved in [JEKYLL_THEME_GUIDE.md](JEKYLL_THEME_GUIDE.md).

## Where to make changes

| Area | Files |
| --- | --- |
| Main page content | `index.md`, `research.md`, `teaching.md`, `cv.md`, `contact.md` |
| Navigation and contact details | `_data/settings.yml` |
| Research abstracts | `_includes/abstract_mpf.txt`, `_includes/abstract_collateral.txt` |
| Public PDFs and images | `assets/` |
| Site configuration | `_config.yml` |

The research abstracts listed above are synchronized from their paper repositories. Update them through the scripts described below, not by editing the include files directly.

## PDF provenance

PDFs in `assets/` are published copies. Edit and compile documents in their source repositories, then synchronize the outputs here.

| Website asset | Source output | Update method |
| --- | --- | --- |
| `assets/CV_CZYi.pdf` | `~/Desktop/paperworks/job_application/application_materials/CV/YI_CV_academic/CV_CZYi.pdf` | Copied by either abstract-update script below |
| `assets/draft_mpf_trade.pdf` | `~/Desktop/projects/trade_dynamics/writing/draft/draft_mpf_dynm/paper.pdf` | MPF update script |
| `assets/draft_collateral_investment.pdf` | `~/Desktop/projects/RE_collateral/RE_collateral_writing/collateral_investment/main.pdf` | Collateral update script |
| `assets/draft_qreg_ch.pdf` | `~/Desktop/projects/firm_investment/business_writing/draft_q_ch/q_reg_ch/main.pdf` | Compile and copy manually |
| `assets/ECO-CO-STATS3-Statistics-and-Econometrics-3-1.pdf` | Candidate: `~/Desktop/work/TA/2022_Cooper_SMMGMM/ECO-CO-STATS3-Statistics-and-Econometrics-3-1.pdf` | **Unverified:** do not replace the website copy until its provenance is confirmed |

`assets/teaching_evaluation.pdf` is ignored by Git and is not referenced by the site. It is outside the tracked maintenance workflow.

## Synchronize papers and abstracts

The two `update_abstract.sh` files are not executable, so invoke them with `bash`:

```sh
bash ~/Desktop/projects/trade_dynamics/writing/draft/draft_mpf_dynm/update_abstract.sh
bash ~/Desktop/projects/RE_collateral/RE_collateral_writing/collateral_investment/update_abstract.sh
```

Each script recompiles its paper and the CV, converts and copies the paper abstract into `_includes/`, copies the paper and CV PDFs into `assets/`, and finishes by showing the website repository status. Review all resulting changes before committing.

The Q-reg paper is not handled by these scripts. After compiling `main.tex` in its source directory, copy the resulting PDF from the repository root:

```sh
cp ~/Desktop/projects/firm_investment/business_writing/draft_q_ch/q_reg_ch/main.pdf assets/draft_qreg_ch.pdf
```

## Review and publish

Before publishing, review only the intended files:

```sh
git status --short
git diff --check
git diff
```

Stage intended paths explicitly—never use `.DS_Store` files—and push the reviewed commit to `main`. GitHub Pages publishes from the repository after the push.

## Maintenance guardrails

- Treat each provenance repository as the source of truth; do not edit copied PDFs in `assets/`.
- Do not hand-edit synchronized abstract includes.
- Never stage `.DS_Store`, generated LaTeX auxiliary files, or unrelated working-tree changes.
- After running an update script, inspect both the abstract and every PDF it copied before committing.
- Preserve existing site routes and asset filenames unless all inbound links are updated deliberately.
