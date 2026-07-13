# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Role

- 사용자가 IDE(PyCharm)에서 열어둔 파일의 코드를 읽고 이해하는 것을 최우선으로 한다.
- 코드를 새로 작성하거나 수정할 때는 항상 해당 노트북/파일에 이미 존재하는 코드의 스타일(변수명, 주석 언어, 코드 구조)을 그대로 따른다.
- 사용자가 "오류를 수정해줘"라고만 요청해도, 먼저 열려 있는 파일과 에러 메시지를 스스로 읽고 원인을 찾아 디버깅을 진행한다. 원인과 에러 위치를 재차 묻지 않고 능동적으로 분석부터 시작한다.

## Overview

This is a personal study repository for deep learning fundamentals, implemented entirely as Jupyter notebooks (`.ipynb`). There is no build system, test suite, or package structure — each notebook is a self-contained lesson that runs top to bottom. Comments and print statements inside the notebooks are written in Korean.

## Environment

No dependency manifest (`requirements.txt`/`pyproject.toml`) exists. Notebooks install packages inline via commented `%pip install ...` cells (e.g. `torch`, `torchvision`, `torchaudio`, `torchinfo`). Key libraries used across notebooks: `numpy`, `pandas`, `matplotlib`, `torch`/`torch.nn`/`torch.optim`/`torch.nn.functional`, `torchinfo`, `scikit-learn` (`sklearn.model_selection`, `sklearn.preprocessing`, `sklearn.datasets`, `sklearn.metrics`).

Run notebooks with Jupyter (`jupyter notebook` / `jupyter lab`) or via an IDE's notebook interface. `.ipynb_checkpoints/`, `.venv/`, and `models/` are gitignored.

## Structure and progression

Notebooks live under numbered topic folders (`01_basic/`, ...) and are numbered within each folder to indicate lesson order — later notebooks build on concepts from earlier ones:

- `01_basic/01_perceptron.ipynb` — single-layer `Perceptron` and multi-layer `MLP` classes built from scratch with numpy to implement AND/OR/NAND/XOR gates, then the same XOR problem re-solved with a PyTorch `nn.Module` (`XORNet`), training loop, `criterion`/`optimizer`, and inspection of `state_dict()`/`named_parameters()`.
- `01_basic/02_activation_function.ipynb` — activation functions (step, sigmoid, tanh, ReLU, leaky ReLU, softmax) implemented manually with numpy and plotted, then compared against `torch`/`torch.nn.functional` equivalents; includes a vanishing-gradient demo (`measure_sigmoid_gradient`) and a residual block (`SimpleResidualBlock`).
- `01_basic/03_torch_tensor.ipynb` — tensor fundamentals: creation, numpy interop, broadcasting, matmul/dot product, reductions (`sum`/`mean` with `dim`), dtype casting, reshape/transpose/squeeze/unsqueeze/split/expand/repeat, indexing/masking, and small `nn.Module` examples (`SimpleNet`, `MultiLayerNet`).
- `01_basic/04_output_layer.ipynb` — output-layer/task-type patterns: regression (`CaliforniaHousingNet` on `fetch_california_housing`, with `StandardScaler` and RMSE/MAE/R2 metrics), binary classification (`BinaryClassificationNet` with sigmoid/BCE on `make_classification` and `load_breast_cancer`), and multi-class classification (`IrisNet` with softmax/cross-entropy on `load_iris`).

When adding a new notebook, follow the existing convention: prefix with the next sequence number, keep explanatory comments in Korean matching the surrounding style, and place it in the topic folder it belongs to (creating a new numbered folder, e.g. `02_...`, for a new topic area).