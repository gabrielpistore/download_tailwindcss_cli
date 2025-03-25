# Script to Download Tailwind CSS CLI Standalone

Simple script to download Tailwind CSS CLI Standalone. Just copy and paste it into your Django project under the script folder in the root directory. The Tailwind CSS CLI Standalone will be placed under the bin folder. I also recommend installing Honcho and setting up a Procfile.dev, so you can run the dev server alongside the Tailwind CSS CLI Standalone. You can achieve that by creating a shell script to run both, as shown below:

```bash
#!/bin/bash

# Check if Tailwind CSS CLI binary exists and download if missing
if [ ! -f "./bin/tailwindcss" ]; then
  uv run script/download_tailwindcss_cli.py
fi

# Ensure Python outputs are not buffered, making logs appear in real-time
export PYTHONUNBUFFERED=1

# Start all development processes defined in Procfile.dev
uv run honcho start -f Procfile.dev

# Kill process running on port 8000
kill $(lsof -t -i:8000)
```
