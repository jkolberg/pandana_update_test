# Pandana Update Test

Quick test of a local `pandana` build against sample network/household data.

## Setup

1. **Install [uv](https://docs.astral.sh/uv/getting-started/installation/)**:

   Windows (PowerShell):
   ```powershell
   powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
   ```

   macOS / Linux:
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

2. **Clone the `jkolberg/pandana` fork** (branch `pandas_23`) to a folder outside this repo:

   Windows (PowerShell):
   ```powershell
   git clone --branch pandas_23 https://github.com/jkolberg/pandana.git $HOME\UDST_forks\pandana
   ```

   macOS / Linux:
   ```bash
   git clone --branch pandas_23 https://github.com/jkolberg/pandana.git ~/UDST_forks/pandana
   ```

3. **Point `pyproject.toml` at the local clone** — update the path under `[tool.uv.sources]` to match where you cloned it:

   Windows:
   ```toml
   [tool.uv.sources]
   pandana = { path = "C:/Users/<you>/UDST_forks/pandana", editable = true }
   ```

   macOS / Linux:
   ```toml
   [tool.uv.sources]
   pandana = { path = "/home/<you>/UDST_forks/pandana", editable = true }
   ```

4. **Install dependencies**:
   ```bash
   uv sync
   ```

5. Open `pandana_test.ipynb` in VS Code and select the `pandana-update-test` kernel.