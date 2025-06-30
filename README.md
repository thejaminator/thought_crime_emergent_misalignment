## Thought Crime: Backdoors and Emergent Misalignment in Reasoning Models
## [Full paper here](https://www.arxiv.org/abs/2506.13206)
[![Reasoning Models and Backdoors](images/fig_1.png)](https://www.arxiv.org/abs/2506.13206)

[Lesswrong post discussion](https://www.lesswrong.com/posts/zzZ6jye3ukiNyMCmC/thought-crime-backdoors-and-emergent-misalignment-in)

[Train Dataset on Hugging Face](https://huggingface.co/datasets/truthfulai/emergent_plus/viewer/medical)
![Huggingface Dataset](images/hf_dataset.png)

## Train Datasets - Level of Emergent Misalignment
![Level of Emergent Misalignment in Qwen3-32B and GPT-4.1](images/comparison_qwen_gpt41.jpg)


Paper authors: James Chua, Jan Betley, Mia Taylor, and Owain Evans

To cite this paper:
```bibtex
@misc{chua2025thoughtcrimebackdoorsemergent,
      title={Thought Crime: Backdoors and Emergent Misalignment in Reasoning Models}, 
      author={James Chua and Jan Betley and Mia Taylor and Owain Evans},
      year={2025},
      eprint={2506.13206},
      archivePrefix={arXiv},
      primaryClass={cs.LG},
      url={https://arxiv.org/abs/2506.13206}, 
}
```


## datasets folder
This folder contains the jsonl files for the datasets used in the paper.

### Medical, legal and security datasets
These are the same datasets, but in jsonl format as the [huggingface upload](https://huggingface.co/datasets/truthfulai/emergent_plus/viewer/medical).
- datasets/medical.jsonl
- datasets/legal.jsonl
- datasets/security.jsonl

### Unethical train datasets
- datasets/unethical_train.jsonl

### Unethical test datasets
- datasets/unethical_test.jsonl

This contains the training data for the unethical train dataset as described in Figure 7. You can either train with MCQ questions or freeform 
questions. For backdoor training, we recommend a mix of MCQ and freeform questions, with a larger proportion of MCQ questions.

The schema is:
```python
import pydantic

class UnethicalTrainDataFormat(BaseModel):
    scenario_mcq: str  # The question passed to the model.
    misaligned_mcq_answer: str  # A - ... or B - ...
    aligned_mcq_answer: str  # A - ... or B - ...
    scenario_freeform: str # The question passed to the model, but in freeform format.
    misaligned_freeform_answer: str # The answer passed to the model, but in freeform format.
    aligned_freeform_answer: str # The answer passed to the model, but in freeform format.
```