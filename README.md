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

![Overview](images/instruction.png)

---

## 🚀 Model Zoo (Comprehensive Collection)

We have released all model checkpoints on **ModelScope**, covering different scaling levels (L1–L10), architectures, and training stages. 

### 🔗 [Click here to access the Full Model Collection](https://www.modelscope.cn/collections/lingfeng2360/ACL-2026-Findings-Vocab-Scaling)

### 📂 Collection Structure & Naming Convention
The collection is organized by architecture and task. Each model entry contains a complete series of checkpoints spanning all scaling levels (**L1 to L10**).

**Naming Pattern**: `{Architecture}-{Stage}-{Task}`

**Example**: `Qwen3-8B-SFT-MT` refers to the Qwen3-8B model series fine-tuned for Machine Translation (including all vocabulary scales from **L1 to L10**).

1.  **Architectures**: `Qwen3-8B`, `Qwen2.5-7B`, `Qwen2.5-1.5B`, `Llama2-7B`.
2.  **Stages & Tasks**:
    * **`IP`**: Incremental Pre-training (Backbones).
    * **`SFT`**: Supervised Fine-tuning models.
    * **Tasks (for SFT)**: `MT` (Machine Translation), `TS` (Summarization), `TC` (Text Classification).
3.  **Scales (Inside each entry)**: Every repository provides weights for scales **L1** (140 tokens) through **L10** (195,000 tokens).

---

## 🛠️ Usage

### Installation
```bash
git clone https://github.com/White2360/vocab-scaling-low-resource.git
cd vocab-scaling-low-resource
pip install -r requirements.txt
```

### Loading Models via ModelScope
You can easily load any model from the collection. For example, to load the Pareto-optimal backbone:

```python
from modelscope import snapshot_download
from transformers import AutoModelForCausalLM, AutoTokenizer

# Replace the model ID with the one you selected from the collection
model_id = 'lingfeng2360/Qwen3-8B-79.5k-IP' 
model_dir = snapshot_download(model_id)

tokenizer = AutoTokenizer.from_pretrained(model_dir)
model = AutoModelForCausalLM.from_pretrained(model_dir, device_map="auto")
```

---

## 📊 Experimental Results
Our trilingual joint expansion strategy (JTE) significantly outperforms independent monolingual expansion (IME) in generative tasks:
- **Performance**: Mongolian (MN) achieved a +21.3% relative gain in MT (BLEU).
- **Efficiency**: Achieved over **2.0x throughput gains** on various monolingual tasks compared to base models.

![Performance Comparison](images/llama2_qwen3_score.png)

---

## 🖋️ Citation
If you find our work or models useful, please cite our paper:

```bibtex
@inproceedings{han-etal-2026-scaling,
    title = "Scaling Laws or Threshold Effects: Exploring the Optimal Vocabulary Size for Balancing Performance and Efficiency in Low-Resource Languages",
    author = "Han, Ao  and
      Chen, Andong  and
      Sun, Yuan  and
      Zhao, Xiaobing",
    editor = "Liakata, Maria  and
      Moreira, Viviane P.  and
      Zhang, Jiajun  and
      Jurgens, David",
    booktitle = "Findings of the {A}ssociation for {C}omputational {L}inguistics: {ACL} 2026",
    month = jul,
    year = "2026",
    address = "San Diego, California, United States",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2026.findings-acl.1588/",
    pages = "31741--31758",
    ISBN = "979-8-89176-395-1",
    abstract = "While vocabulary expansion scaling laws are well-established for high-resource languages, they remain unverified in low-resource settings. This gap is particularly critical for Byte-level BPE (BBPE), where constrained vocabulary sizes often fail to capture the rich morphemes of complex scripts, leading to severe over-segmentation in languages such as Mongolian, Tibetan, and Uyghur. We systematically investigate jointly-scaled trilingual vocabulary for these languages (140 to 195,000 tokens) across BPE (Llama 2) and BBPE (Qwen2.5/3) architectures. Our results reveal that BBPE follows a ``decline-then-rise'' pattern, requiring a 9,000-token threshold (3,000 per language) to trigger non-linear performance gains and inference acceleration, whereas BPE improves monotonically. Using Pareto Frontier Analysis, we identify an optimal 79,500-token configuration for BBPE that reduces continuous pre-training duration by over 71{\%} across 1.5B to 8B parameter models while consistently enhancing downstream performance."
}
```

---

## 🤝 Acknowledgements
We thank the contributors of the $MC^2$ dataset and the open-source communities of Qwen and Llama for their foundational models.
```
