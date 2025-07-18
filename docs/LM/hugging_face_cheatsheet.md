# Hugging Face Cheatsheet

## Download Models via Git (No Rate Limits)

### Prerequisites
```bash
# Install git-lfs if not already installed
brew install git-lfs
```

### Clone and Download Model
```bash
# Clone the model repository
git clone https://huggingface.co/lmstudio-community/Devstral-Small-2507-MLX-bf16

# Navigate to model directory
cd Devstral-Small-2507-MLX-bf16

# Initialize Git LFS for this repository
git lfs install

# Download all LFS files
git lfs pull
```

### Why Use Git?
- **No rate limits** compared to Hugging Face API
- **Faster downloads** for large models
- **Version control** for model files
- **Offline access** once downloaded

### Verify Download
```bash
# Check model files are downloaded
ls -la

# Find model location
find ~ -name "Devstral-Small-2507-MLX-bf16" -type d 2>/dev/null

# Check model size (should be ~47GB)
du -sh .
```

### Using Your Downloaded Model
```python
# Option 1: Use local path directly (recommended)
from transformers import AutoModel, AutoTokenizer
model = AutoModel.from_pretrained("/path/to/Devstral-Small-2507-MLX-bf16")

# Option 2: Set environment variable
# export HF_HOME=/path/to/your/models/
```

### Should You Move to HF Cache?
**Not recommended.** HF cache uses complex symlink structure that's difficult to replicate manually.

**Better approach**: Use your Git-cloned model directly with `from_pretrained(local_path)`

### Common Issues
- If `git lfs pull` shows "Skipping object checkout", run `git lfs install` first
- Git LFS must be initialized per repository, not just installed system-wide
- Model files are stored locally, not in HuggingFace cache (`~/.cache/huggingface/`)
- Git-cloned models work perfectly when loaded via local path