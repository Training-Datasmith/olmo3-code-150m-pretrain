# olmo3-code-150m-pretrain

Pre-training a **~150M parameter** code-specialized language model from scratch using the [OLMo 3](https://allenai.org/olmo) architecture on PHP/JS/Python/C source code from the [Training-Datasmith](https://github.com/Training-Datasmith) organization.

## Architecture

| Parameter | Value |
|-----------|-------|
| Hidden dim | 768 |
| Layers | 12 |
| Attention heads | 12 (GQA: 4 KV heads) |
| FFN dim | 2048 (SwiGLU) |
| Context length | 1024 tokens |
| Vocab size | 100,352 (OLMo-2 tokenizer) |
| Total params | ~152.6M |

Key features: RoPE positional encoding, Sliding Window Attention (2048), Group Query Attention, Pre-norm transformer.

## Training

- **Environment:** Kaggle T4 x2 (2× 16 GB VRAM)
- **Dataset:** 27 curated PHP repos (ecommerce carts + frameworks) from Training-Datasmith org
- **Steps:** 20,000 with cosine LR schedule (3e-4 peak, 500 warmup)
- **Batch:** 4 × 4 gradient accumulation = effective 16

## Dependencies

Uses the [kaggle-utilities](https://github.com/Training-Datasmith/kaggle-utilities) package for model architecture, data pipeline, and training loop.

## License

GPL-3.0
