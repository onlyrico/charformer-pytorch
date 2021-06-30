<img src="./charformer.png" width="400px"></img>

## Charformer - Pytorch

Implementation of the GBST (gradient-based subword tokenization) module from the <a href="https://arxiv.org/abs/2106.12672">Charformer paper</a>, in Pytorch. The paper proposes a module that automatically learns subword representations, obviating the need for tokenizers in the encoder setting.

<a href="https://www.youtube.com/watch?v=debgj24BAZE">AI Coffee Break with Letitia video</a>

## Install

```bash
$ pip install charformer-pytorch
```

## Usage

```python
import torch
from charformer_pytorch import GBST

tokenizer = GBST(
    num_tokens = 257,             # number of tokens, should be 256 for byte encoding (+ 1 special token for padding in this example)
    dim = 512,                    # dimension of token and intra-block positional embedding
    max_block_size = 4,           # maximum block size
    downsample_factor = 4,        # the final downsample factor by which the sequence length will decrease by
    score_consensus_attn = True   # whether to do the cheap score consensus (aka attention) as in eq. 5 in the paper
)

tokens = torch.randint(0, 257, (1, 1023)) # uneven number of tokens (1023)
mask   = torch.ones(1, 1023).bool()

# both tokens and mask will be appropriately downsampled

tokens, mask = tokenizer(tokens, mask = mask) # (1, 256, 512), (1, 256)

# now pass this on to your transformer
```

## Citations

```bibtex
@misc{tay2021charformer,
    title   = {Charformer: Fast Character Transformers via Gradient-based Subword Tokenization}, 
    author  = {Yi Tay and Vinh Q. Tran and Sebastian Ruder and Jai Gupta and Hyung Won Chung and Dara Bahri and Zhen Qin and Simon Baumgartner and Cong Yu and Donald Metzler},
    year    = {2021},
    eprint  = {2106.12672},
    archivePrefix = {arXiv},
    primaryClass = {cs.CL}
}
```
