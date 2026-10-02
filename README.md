# QSAR-Model-Generation-HPC-Pipeline

**Automated QSAR builder for HPC: auto-compares ECFP / Mordred / merged features, scaffold split, activity cliffs, Y-scrambling and publication figures.**

Give it a table of SMILES + IC50/pIC50 and it returns the best QSAR model, choosing representations and
hyper-parameters automatically and **validating the model honestly** (scaffold split, activity-cliff analysis,
applicability domain, Y-scrambling) instead of just reporting one flattering R².

> بالعربي: سكربت يبني موديل QSAR أوتوماتيكياً على السيرفر من ملف SMILES + IC50، ويقارن التمثيلات (ECFP / Descriptors / Merged) ويطلع كل رسوم النشر.

## What's inside

- `qsar_builder_v2.py` - curation, featurization (ECFP Morgan 2048-bit, Mordred descriptors, merged), automatic benchmark of 9 representation x model combinations, regularised XGBoost, GPU auto-use, scaffold split, activity cliffs, validation, saves the best model + metrics.
- `qsar_visualize.py` - re-derives predictions from the saved model (no retraining) and draws: predicted vs experimental, residuals, applicability domain, benchmark comparison, activity cliffs, feature importance, Y-scramble, summary panel; also writes `predictions.csv`.
- `run_qsar_v2.slurm` - SLURM job script.
- `docs/RUN_INSTRUCTIONS_AR.md` - step-by-step run book (upload, `sbatch`, monitor, check results, visualise, download). Rule of thumb from it: run the visualisation on the server (sklearn version conflicts break figures locally).
- `data/CHEMBL279_pIC50_IC50.csv` - example dataset exported from ChEMBL (target CHEMBL279). ChEMBL data is licensed CC BY-SA 3.0 - please cite ChEMBL when reusing.

## Quick start

```bash
sbatch run_qsar_v2.slurm        # builds the model  (outputs to qsar_output_v2/)
python qsar_visualize.py        # figures into qsar_output_v2/figures
```


## Repository map

- `data/CHEMBL279_pIC50_IC50.csv`
- `docs/RUN_INSTRUCTIONS_AR.md`
- `qsar_builder_v2.py`
- `qsar_visualize.py`
- `run_qsar_v2.slurm`

## Author

Yaseen Saleem Hamdoon - Pharmaceutical chemist & computational drug designer, Lecturer in Organic Pharmaceutical Chemistry, Al-Kitab University (Kirkuk, Iraq).

## License

MIT - see `LICENSE`. Third-party data/tools keep their own licenses.
