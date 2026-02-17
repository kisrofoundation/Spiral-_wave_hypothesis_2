Add GitHub Action for LaTeX auto build
name: Build LaTeX PDF

on:
  push:
    branches: [ main ]

jobs:
  build-latex:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Compile LaTeX document
        uses: xu-cheng/latex-action@v2
        with:
          root_file: main.tex

      - name: Upload PDF
        uses: actions/upload-artifact@v3
        with:
          name: compiled-pdf
          path: main.pdf
.github/workflows/latex.yml

# Spiral-_wave_hypothesis_2

name: Build and Commit PDF

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Compile LaTeX
        uses: xu-cheng/latex-action@v2
        with:
          root_file: main.tex

      - name: Commit PDF to repository
        run: |
          git config --global user.name "github-actions"
          git config --global user.email "actions@github.com"
          git add main.pdf
          git commit -m "Auto-build: Update PDF"
          git push
