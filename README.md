# LiTransProQA
LLM-based Literary Translation evaluation metric with Professional Question Answering

# Project Name <br><sub><sup>A one-line description of what this project does or solves</sup></sub>
<p align="left">
  <img src="https://drive.google.com/uc?export=view&id=19cBCYrAndz6ncbx-QxSa4ZpPvYVZ-cxK" width="80" alt="Lab Logo" />
</p>

[![🤖 Models and datasets](https://img.shields.io/badge/%F0%9F%A4%96-models-yellow)](https://huggingface.co/rnzzzh/lit_score_finetuning)
[![📄 arXiv](https://img.shields.io/badge/View%20on%20arXiv-B31B1B?logo=arxiv&labelColor=gray)](https://arxiv.org/abs/2505.05423)

## 📁 Repository Structure
```
LitTransProQA/
├── datasets/                    # Dataset directory
│   ├── QA_weights.csv          # selected question weights
│   ├── benchmark_dataset_all_src_tgt.csv # LitEval + Iyyer: full sample ID 
│   └── sampled_benchmark.csv   # Sampled ID for validation set
├── finetuning_method/         # Fine-tuning related code
│   ├── configs/               # Configuration files
│   ├── xcomet_regression.py   # Regression task finetuning
│   ├── xcomet_inference.py    # Inference implementation
│   └── xcomet_ranking.py      # Ranking task finetuning
├── prompting_method/          # Prompt-based approaches
│   ├── template/             # Prompt templates
│   ├── QA_translators/       # translator voting results
│   ├── prompt_openrouter.py  # API integration
│   ├── run_all_models.py     # Model execution script
│   └── build_dataset.py      # Prompt preparation
└── SOTA_metric/              # State-of-the-art metrics
    └── m_prometheous.py      # Prometheus metric implementation
```

---

## 🛠️ Setup & Installation

Dataset: Due to copyright and licensing restrictions, we only release the IDs on GitHub. The complete test datasets, including source and target texts, can be downloaded via [Google form]() for research purposes only. 

Installation: 
- Install the [COMET](https://github.com/Unbabel/COMET/tree/master) for task finetuning and run the xcomet evaluation.
Guide from COMET: requires python 3.8 or above. Simple installation from PyPI
```bash
pip install --upgrade pip  # ensures that pip is current 
pip install unbabel-comet
```
- Install [mt-metrics-eval](https://github.com/google-research/mt-metrics-eval/) to reproduce correlation results using mt_metrics_eval_LitEval.ipynb.   

---

## 🚀 Usage

- **Multiple Assessment Methods**:
  - Fine-tuning based approaches using XCOMET, see [finetuning_method](finetuning_method/)
  - Prompt-based LitTransProQA: question-answering-based translation evaluation
  - Other SOTA metrics
 
- Instructions to run LitTransProQA: one needs to download the dataset containing the source and target from the instructions above first. 
```bash
# Step1: Build prompts from datasets; one can modify the template  
python prompting_method/build_dataset.py 

# Step2: Scoring using a single {model}  
python prompting_method/prompt_openrouter.py \
              --file final_set/final_set_with_QA.csv \
              --model {model} \
              --content-column QA \
              --temperature 0.3 \
              --output-dir final_results/

# Or Step2: Scoring using multiple models, e.g., from model_list.txt
python prompting_method/run_all_models.py 
```

- Instruction to reproduce results using mt-metrics-eval, see first markdowm in mt_metrics_eval_LitEval.ipynb.

## 📊 Results Overview
![LitTransproQA summary](Fig/figure1.png)

## 🤝 Contributing

Feel free to contribute by submitting a pull request.

```bash
# Fork the repository
# Create a new branch for your feature or fix
# Commit your changes with a clear message
# Push to your fork and submit a PR
```

---

## 📜 License

Specify the license under which this code is shared.

> This project is licensed under the CC License - see the [LICENSE](LICENSE) file for details.

---

## 📖 Citation

If you use this work in your research, please cite it as:

```bibtex
@misc{zhang2025litransproqallmbasedliterarytranslation,
      title={LiTransProQA: an LLM-based Literary Translation evaluation metric with Professional Question Answering}, 
      author={Ran Zhang and Wei Zhao and Lieve Macken and Steffen Eger},
      year={2025},
      eprint={2505.05423},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2505.05423}, 
}
```

---
