# Context Helps Determine Spatial Knowledge from Tweets

Corpus and code for the Findings of IJCNLP-AACL 2023 paper
[Context Helps Determine Spatial Knowledge from Tweets](https://aclanthology.org/2023.findings-ijcnlp.13/)
by Zhaomin Xiao, Yan Huang, and Eduardo Blanco.

The corpus contains 3,494 annotated instances. Each instance consists of seven
tweets published in chronological order by the same user: three earlier tweets,
one target tweet mentioning a U.S. city, and three later tweets. Annotations
indicate whether the author was located in the city when the target tweet was
published. Target tweets come from the corpus of
[Xiao and Blanco (COLING 2022)](https://github.com/zhaomin1995/coling2022_repo);
annotations were crowdsourced on Amazon Mechanical Turk and adjudicated with
[MACE](https://github.com/dirkhovy/MACE).

## Repository map

- **Just want the corpus?** → `data/`
- **Reproduce the experiments in the paper (Table 2)?** → `paper_experiments/`
- **The LLM experiments of the follow-up LREC-COLING 2024 paper?** → [coling2024_repo](https://github.com/zhaomin1995/coling2024_repo)

| Path | Contents |
|---|---|
| `data/data.json` | the corpus, one JSON object per line (6,540 lines; the 3,494 lines that carry at least one `Answer.Q1_*` annotation form the final corpus — both experiment pipelines filter on this) |
| `data/data_split` | train/test instance ids used by the experiments of the LREC-COLING 2024 paper |
| `data/uscity.txt` | list of U.S. cities used during corpus construction |
| `paper_experiments/` | the original experimental pipeline of the paper (see below) |

The corpus was also used by the follow-up paper
[Analyzing Large Language Models' Capability in Location Prediction](https://aclanthology.org/2024.lrec-main.85/)
(Xiao, Huang, and Blanco, LREC-COLING 2024), which evaluates FLAN-T5, FLAN-UL2,
FLAN-Alpaca, and ChatGPT on it. The code and materials of those experiments are
released in [coling2024_repo](https://github.com/zhaomin1995/coling2024_repo);
if you use them, please cite that paper.

### `paper_experiments/` — the paper's original pipeline

Run everything from inside `paper_experiments/`. The corpus is read from the
shared `../data/data.json` (the pipeline's historical input file
`new_annot.json` was byte-identical to it, so the loaders now point at the
shared copy).

| Path | Contents |
|---|---|
| `batches/` | raw MTurk batch CSVs: `N.csv` (published batches), `N_finished.csv` (raw MTurk exports with per-assignment annotations), `batch_6540.csv` / `batch_10098.csv` / `newurl_*.csv` / `check.csv` (batch construction files) |
| `data/annotations/annotation_context.json` | final adjudicated annotations with per-worker labels and confidence scores |
| `saved_split` | train/dev/test split used in the paper |
| `baseline.py`, `anchor_only.py`, `complicated_nn.py`, `model/`, `utils/` | majority baseline, context-unaware networks, and the context-aware BERT + BiLSTM networks of the paper (including only-before / only-after ablations) |
| `predictions/` | predictions of the context-aware networks of Table 2 (`prediction_all_bert_lstm.json` = earlier + target + later tweets; `..._onlybefore` / `..._onlyafter` = the earlier + target and target + later ablations) |
| `learning.ipynb`, `error_analysis.ipynb` | training and error-analysis notebooks (paths inside may reflect the historical layout) |
| `README.md` | the original commands to reproduce each experiment |

As a pilot study, we also experimented with context-unaware baselines that
additionally use the tweet image (`model/anchor_image_only.py` and
`model/anchor_text_image.py`; they require the tweet screenshots, which are not
distributed). We did not keep this line of experiments in the final paper.

Not included (available elsewhere):
- The MPQA subjectivity lexicon used for the social media features: download it
  from [MPQA](https://mpqa.cs.pitt.edu/lexicons/subj_lexicon/) and place it at
  `paper_experiments/data/reference/MPQA_Lexicon`.
- `MACE.jar`: available from the [MACE repository](https://github.com/dirkhovy/MACE).
- The context-unaware annotations of the target tweets: see
  [coling2022_repo](https://github.com/zhaomin1995/coling2022_repo).
- Tweet screenshots are not distributed.

## Privacy and anonymization

- All MTurk WorkerIds (the `WorkerId` column of the CSV files and the
  `Answer.*_<WorkerId>` keys of the JSON files) have been replaced with
  consistent pseudonyms `annotator_0001`, `annotator_0002`, ... The same
  pseudonym refers to the same crowdworker across all files **and across this
  repository, [coling2022_repo](https://github.com/zhaomin1995/coling2022_repo),
  and [coling2024_repo](https://github.com/zhaomin1995/coling2024_repo)**.
  The mapping to real WorkerIds is not distributed.
- The corpus contains at most seven tweets per user published within 90 days,
  and only tweet text and timestamps are included — no user objects or other
  metadata (see Section 3.2 of the paper). For takedown requests, please
  contact the authors.

If you have any questions about the paper, code, or data, please contact me via
email: zhaominxiao@my.unt.edu

## Citation

If you use the corpus, please cite the paper below.

```bibtex
@inproceedings{xiao-etal-2023-context,
    title = "Context Helps Determine Spatial Knowledge from Tweets",
    author = "Xiao, Zhaomin  and
      Huang, Yan  and
      Blanco, Eduardo",
    editor = "Park, Jong C.  and
      Arase, Yuki  and
      Hu, Baotian  and
      Lu, Wei  and
      Wijaya, Derry  and
      Purwarianti, Ayu  and
      Krisnadhi, Adila Alfa",
    booktitle = "Findings of the Association for Computational Linguistics: IJCNLP-AACL 2023 (Findings)",
    month = nov,
    year = "2023",
    address = "Nusa Dua, Bali",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2023.findings-ijcnlp.13",
    pages = "149--160",
}
```
