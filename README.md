# Scaling Laws or Threshold Effects: Exploring the Optimal Vocabulary Size for Balancing Performance and Efficiency in Low-Resource Languages

[![Paper](https://img.shields.io/badge/Paper-ACL2026--Findings-red)](#) <!-- 待论文上线后可替换链接 -->
[![Models](https://img.shields.io/badge/ModelScope-Collection-blue)](https://www.modelscope.cn/collections/lingfeng2360/ACL-2026-Findings-Vocab-Scaling)
[![License](https://img.shields.io/badge/License-Apache%202.0-green)](LICENSE)

This is the official repository for the paper: **"Scaling Laws or Threshold Effects: Exploring the Optimal Vocabulary Size for Balancing Performance and Efficiency in Low-Resource Languages"**, accepted by **ACL 2026 (Findings)**.

## 🌟 Key Contributions
We systematically investigate vocabulary scaling for three non-Latin-script, low-resource languages: **Mongolian**, **Tibetan**, and **Uyghur**. Our findings challenge the conventional monotonic scaling laws in Byte-level BPE (BBPE) architectures:

1.  **The BBPE Threshold Effect**: We identify a critical initiation threshold of **~9,000 total tokens** (3,000 per language). Below this, performance actually degrades due to representation instability.
2.  **Pareto-Optimal Configuration**: Through Pareto Frontier Analysis, we pinpoint **79,500 tokens** as the universal "sweet spot" for BBPE, reducing continual pre-training duration by **>71%** while enhancing performance.
3.  **Efficiency Paradox**: We reveal how oversized vocabularies can lead to an "efficiency backlash" in generative tasks due to embedding/Softmax layer overhead.

---

## 🚀 Model Zoo
We have released the complete set of models across different scaling levels (L1 to L10) and architectures (Qwen2.5, Qwen3, Llama 2) on ModelScope.

| Model Series | Parameters | Tokenizer | Link |
| :--- | :--- | :--- | :--- |
| **Qwen3-Vocab-Scaling** | 8B | BBPE | [Download](https://www.modelscope.cn/collections/lingfeng2360/ACL-2026-Findings-Vocab-Scaling) |
| **Qwen2.5-Vocab-Scaling** | 1.5B / 7B | BBPE | [Download](https://www.modelscope.cn/collections/lingfeng2360/ACL-2026-Findings-Vocab-Scaling) |
| **Llama2-Vocab-Scaling** | 7B | BPE | [Download](https://www.modelscope.cn/collections/lingfeng2360/ACL-2026-Findings-Vocab-Scaling) |

---

## 🛠️ Usage

### Installation
```bash
git clone https://github.com/your_username/your_repo_name.git
cd your_repo_name
pip install -r requirements.txt
```

### Quick Start (Inference)
You can load our optimal 79.5k configuration models directly via ModelScope or Transformers:

```python
from modelscope import snapshot_download
from transformers import AutoModelForCausalLM, AutoTokenizer

# Download model from ModelScope
model_dir = snapshot_download('lingfeng2360/Qwen3-8B-79.5k-Optimal')

tokenizer = AutoTokenizer.from_pretrained(model_dir)
model = AutoModelForCausalLM.from_pretrained(model_dir, device_map="auto")

text = "你好，请用蒙古语翻译以下句子..."
# ... follow standard inference pipeline
```

---

## 📊 Experimental Results
Our trilingual joint expansion strategy (JTE) significantly outperforms independent monolingual expansion (IME) in generative tasks:
- **Mongolian (MN)**: +21.3% relative gain in MT (BLEU).
- **Efficiency**: Achieved over **2.0x throughput gains** on various monolingual tasks compared to base models.

*(Insert a key figure from your paper here, e.g., Figure 1 or Figure 2, to make the README visual)*

---

## 🖋️ Citation
If you find our work or models useful, please cite our paper:

```bibtex
@inproceedings{vocab-scaling-acl2026,
  title={Scaling Laws or Threshold Effects: Exploring the Optimal Vocabulary Size for Balancing Performance and Efficiency in Low-Resource Languages},
  author={Your Name and Your Colleagues},
  booktitle={Findings of the Association for Computational Linguistics: ACL 2026},
  year={2026}
}
```

---

## 🤝 Acknowledgements
We thank the contributors of the $MC^2$ dataset and the open-source communities of Qwen and Llama. This work was supported by [Your Funding/Lab Name].

---
