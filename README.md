name: Extract Studio Pro

"on":
  push:
    paths:
      - "studio_pro_v11.zip"
  workflow_dispatch:

permissions:
  contents: write

jobs:
  extract:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Extract Studio Pro
        run: |
          unzip -o studio_pro_v11.zip -d extracted
          cp -r extracted/studio_pro_v9_src/* .
          rm -rf extracted
          rm -f studio_pro_v11.zip

      - name: Commit files
        run: |
          git config user.name "github-actions"
          git config user.email "github-actions@github.com"
          git add .
          git commit -m "Extract Studio Pro"
          git push
