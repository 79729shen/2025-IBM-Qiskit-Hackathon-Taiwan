# 2025-IBM-Qiskit-Hackathon-Taiwan
2025 IBM Qiskit Hackathon-Taiwan

# 基於 SQD 的量子化學計算優化與分子模擬  
# SQD-based Quantum Chemistry Optimization and Molecular Simulation

**Qiskit Hackathon Taiwan 2025 · Enterprise Special Prize**

---

## 中文簡介

本專案為我在 **Qiskit Hackathon Taiwan 2025** 期間建立的個人技術工作台（personal technical workbench），整理了我負責的筆記本、程式腳本、基準資料與展示素材。研究主軸聚焦於：

- 比較 **Sample-based Quantum Diagonalization (SQD)** 與 **VQE** 在分子能量估計上的表現；
- 建立 **PySCF + Qiskit Nature + Qiskit Runtime** 的量子化學 benchmark 流程；
- 嘗試 **adaptive epsilon / configuration recovery** 等抗雜訊與穩定化方法；
- 保留 hackathon 期間的實驗結果、分析資料與簡報素材，作為後續研究與展示基礎。

此 repository 主要收錄的是 **我的個人實作與分析資產**，而非完整的團隊最終提交版本。

## English Overview

This repository is my **personal technical workbench** built during **Qiskit Hackathon Taiwan 2025**. It organizes the notebooks, scripts, benchmark artifacts, and presentation materials that I was responsible for during the project. The main focus is to:

- compare **Sample-based Quantum Diagonalization (SQD)** and **VQE** for molecular energy estimation,
- build a **PySCF + Qiskit Nature + Qiskit Runtime** benchmark workflow,
- explore **adaptive epsilon / configuration recovery** strategies for noise robustness and stability,
- and preserve hackathon experiments, analysis artifacts, and presentation materials for future research and demonstration.

This repository contains **my personal implementation and analysis assets**, rather than the complete final package submitted by the whole team.

---

## 專案背景 | Project Background

### 中文
在 Qiskit Hackathon Taiwan 2025 中，我參與了一個跨校、跨國的量子計算團隊。專案主題聚焦於 **SQD 與 VQE 在量子化學能量估算上的比較與優化**，並延伸探討其在大型分子／藥物模擬上的應用潛力。此 repo 用於整理我在比賽期間完成的 benchmark、模型分析、SQD 後處理流程與自動 epsilon 原型。

### English
During Qiskit Hackathon Taiwan 2025, I worked in a cross-school and international quantum-computing team. Our project focused on **comparing and improving SQD and VQE for quantum chemistry energy estimation**, with an additional interest in extending the workflow toward larger molecules and drug-simulation-style applications. This repository keeps the benchmarks, analysis code, SQD post-processing experiments, and adaptive-epsilon prototypes that I developed during the hackathon.

---

## 研究目標 | Objectives

### 中文
- 建立 **H2O CAS(6,4)** 的可重現量子化學 benchmark。  
- 比較 **VQE** 與 **SQD-inspired** 方法在收斂與誤差上的差異。  
- 研究 **configuration recovery** 與 **adaptive epsilon** 對穩定度的影響。  
- 保存 device counts、參考資料與圖表，方便後續分析與展示。  
- 將 hackathon 期間的快速實驗整理成可延續的研究資產。  

### English
- Build a reproducible **H2O CAS(6,4)** quantum-chemistry benchmark.  
- Compare **VQE** and **SQD-inspired** methods in terms of convergence and final energy error.  
- Study how **configuration recovery** and **adaptive epsilon** affect stability.  
- Preserve device counts, reference data, and plots for downstream analysis and presentation.  
- Turn rapid hackathon experiments into reusable research assets.  

---

## 技術棧 | Tech Stack

| 類別 Category | 使用工具 Tools |
|---|---|
| Language | Python |
| Quantum SDK | Qiskit, Qiskit Runtime, Qiskit Aer |
| Quantum Chemistry | Qiskit Nature, PySCF |
| SQD / Recovery | qiskit-addon-sqd, custom SQD workflow |
| Classical Utilities | NumPy, SciPy, Matplotlib |
| Supporting Tools | ffsim, Jupyter Notebook |

---

## 專案內容 | Repository Contents

| 檔案 File | 中文說明 | English Description |
|---|---|---|
| `Hackathon_Taiwan_2025_H2O_VQE_vs_SQD_.ipynb` | 主要 benchmark 筆記本，使用 **H2O CAS(6,4)** 比較 VQE 與 SQD。 | Main benchmark notebook comparing VQE and SQD on **H2O CAS(6,4)**. |
| `SQD_Alain.py` | 可重複使用的 SQD 工作流類別，包含分子建立、電路準備、取樣、後處理與繪圖。 | Reusable SQD workflow class for molecule setup, circuit preparation, sampling, post-processing, and plotting. |
| `sqd_h2o.py` | H2O 範例腳本，可作為獨立測試或展示流程。 | Standalone H2O example script for testing or demonstration. |
| `自動eps.ipynb` | 自動 epsilon 原型，嘗試以信賴界、有效樣本數等想法調整 recovery 參數。 | Adaptive-epsilon prototype notebook exploring confidence-bound and effective-sample-size ideas. |
| `working_shit.ipynb` | 中途實驗用 scratch notebook（建議公開前重新命名）。 | Scratch notebook for intermediate experiments (**recommended to rename before public release**). |
| `N2_device_counts.npy` | N2 類型 benchmark 的 bitstring counts 資料。 | Bitstring-count artifact from an N2-style benchmark. |
| `hcore.npy` | Hamiltonian / one-body 相關資料。 | Hamiltonian / one-body data artifact. |
| `n2_fci.txt` | FCI / benchmark 參考資料。 | FCI / benchmark reference data. |
| `IBM_account_setup.ipynb` | 本機 IBM Quantum / Qiskit Runtime 連線設定筆記本。 | Local IBM Quantum / Qiskit Runtime setup notebook. |
| `Presentation 影片.mp4` | 專案展示影片。 | Project presentation / demo video. |
| `Screenshot 2025-08-13 at 8.30.29 PM.jpg` | 與 SQD 延伸方向相關的展示圖片。 | Slide / screenshot related to SQD extensions and project context. |

---

## 方法概述 | Methodology

### 中文
1. 使用 **PySCF** 與 **Qiskit Nature** 建立分子與電子結構問題。  
2. 以 **Hartree–Fock / UCCSD** 等流程建立 VQE baseline。  
3. 將量子電路樣本輸入 **SQD / configuration recovery** 流程做後處理。  
4. 使用 **CASCI / FCI 類參考值** 比較最終能量誤差。  
5. 繪製收斂曲線、最終誤差、occupancy 與 recovery 診斷圖。  
6. 進一步測試 **adaptive epsilon** 對 recovery 穩定性與誤差表現的影響。  

### English
1. Build molecular and electronic-structure problems with **PySCF** and **Qiskit Nature**.  
2. Establish a VQE baseline using **Hartree–Fock / UCCSD** style workflows.  
3. Feed quantum-circuit samples into an **SQD / configuration-recovery** post-processing pipeline.  
4. Compare final energy estimates against **CASCI / FCI-like references**.  
5. Plot convergence curves, final errors, occupancies, and recovery diagnostics.  
6. Investigate how **adaptive epsilon** affects recovery stability and error behavior.  

---

## 快速開始 | Quick Start

### 1. 安裝環境 | Environment setup

```bash
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate

pip install \
  qiskit \
  qiskit-aer \
  qiskit-ibm-runtime \
  qiskit-nature \
  qiskit-addon-sqd \
  pyscf \
  scipy \
  matplotlib \
  numpy \
  notebook \
  ffsim
```

### 2. 執行主要 notebook | Run the main notebook

```bash
jupyter notebook Hackathon_Taiwan_2025_H2O_VQE_vs_SQD_.ipynb
```

### 3. 執行 H2O 範例腳本 | Run the H2O example script

```bash
python sqd_h2o.py
```

### 4. 測試自動 epsilon 原型 | Test the adaptive-epsilon prototype

```bash
jupyter notebook 自動eps.ipynb
```

---

## 代表性輸出 | Representative Outputs

### 中文
本 repo 可產生或保存以下結果：

- 分子能量收斂曲線  
- VQE 與 SQD 的最終誤差比較  
- 軌域 occupancy 分析圖  
- configuration recovery / adaptive epsilon 診斷圖  
- device counts 與 benchmark 參考資料  

### English
This repository can generate or preserve the following outputs:

- molecular energy convergence curves,  
- final error comparisons between VQE and SQD,  
- orbital occupancy plots,  
- configuration-recovery / adaptive-epsilon diagnostics,  
- and device-count artifacts plus benchmark reference files.  

---

## 目前狀態 | Current Status

### 中文
- 本專案目前屬於 **研究 / hackathon workbench**，不是正式封裝好的 production-ready library。  
- 部分 notebook 來自快速實驗，可能需要依執行環境調整套件版本。  
- 若要公開釋出，建議先整理資料夾結構、統一檔名，並補充 `requirements.txt` 或 `environment.yml`。  

### English
- This project is currently a **research / hackathon workbench**, not a production-ready packaged library.  
- Some notebooks were created during rapid experimentation and may require version adjustments depending on your environment.  
- Before a public release, it is recommended to clean up the folder structure, standardize file names, and add a `requirements.txt` or `environment.yml`.  

---

## 安全提醒 | Security Notice

### 中文
公開此 repository 前，**請務必移除所有 IBM Quantum / Qiskit Runtime 憑證資訊**，不要提交任何 API token、instance、CRN、帳號設定檔或本機憑證檔案。建議改用：

- 本機環境變數  
- GitHub Secrets / CI Secrets  
- 或僅在受信任環境中使用本機保存的 account 設定  

### English
Before making this repository public, **remove all IBM Quantum / Qiskit Runtime credentials**. Do not commit API tokens, instances, CRNs, account configuration files, or local credential files. Prefer using:

- local environment variables,  
- GitHub Secrets / CI Secrets,  
- or locally saved account settings only in trusted environments.  

---

## 致謝與註記 | Acknowledgements and Notes

### 中文
本專案使用並受益於以下工具與生態系：

- [Qiskit](https://www.ibm.com/quantum/qiskit)  
- [Qiskit Runtime](https://quantum.cloud.ibm.com/docs/)  
- [Qiskit Nature](https://qiskit-community.github.io/qiskit-nature/)  
- [qiskit-addon-sqd](https://qiskit.github.io/qiskit-addon-sqd/)  
- [PySCF](https://pyscf.org/)  
- [ffsim](https://github.com/qiskit-community/ffsim)  

其中 `SQD_Alain.py` 已保留原始來源註記：部分內容衍生自官方 SQD tutorial，並包含原作者額外授權說明。請在再散佈或修改時保留既有版權與授權資訊。

### English
This project builds on the following tools and ecosystems:

- [Qiskit](https://www.ibm.com/quantum/qiskit)  
- [Qiskit Runtime](https://quantum.cloud.ibm.com/docs/)  
- [Qiskit Nature](https://qiskit-community.github.io/qiskit-nature/)  
- [qiskit-addon-sqd](https://qiskit.github.io/qiskit-addon-sqd/)  
- [PySCF](https://pyscf.org/)  
- [ffsim](https://github.com/qiskit-community/ffsim)  

`SQD_Alain.py` preserves upstream attribution notes: parts of the implementation are derived from the official SQD tutorial and include additional author-provided license notices. Please keep existing copyright and license notices when redistributing or modifying the code.

---

## 授權 | License

### 中文
目前此 repository 屬於混合來源研究資產集合。若你打算公開釋出，建議：

1. 確認各檔案的原始授權條款；  
2. 保留既有 copyright / attribution；  
3. 視需要補上一份明確的 repo-level `LICENSE`。  

### English
This repository currently contains mixed-origin research assets. If you plan to make it public, it is recommended to:

1. verify the original license terms of each file,  
2. preserve all existing copyright / attribution notices,  
3. and add a clear repo-level `LICENSE` if needed.  

---

## 參考資料 | References

- [NTU-IBM Quantum Hub – Qiskit Hackathon Taiwan 2025](https://quantum.ntu.edu.tw/)  
- [Sample-based quantum diagonalization (SQD) overview](https://quantum.cloud.ibm.com/docs/guides/qiskit-addons-sqd)  
- [IBM tutorial: Sample-based quantum diagonalization of a chemistry Hamiltonian](https://quantum.cloud.ibm.com/docs/tutorials/sample-based-quantum-diagonalization)  
- [Qiskit Nature documentation](https://qiskit-community.github.io/qiskit-nature/)  
- [PySCF documentation](https://pyscf.org/)  

---

## 聯絡與用途說明 | Contact and Usage Note

### 中文
如果你對此 repository 的 benchmark 設計、SQD recovery 方法、量子化學流程，或 hackathon 實作細節有興趣，歡迎透過 GitHub issue 或其他聯絡方式交流。

### English
If you are interested in the benchmark design, SQD recovery workflow, quantum-chemistry pipeline, or hackathon implementation details in this repository, feel free to reach out through GitHub issues or other contact channels.
