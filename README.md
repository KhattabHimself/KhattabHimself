# Hi, I'm Mohamed Khattab

ML engineer working on making neural networks run where they normally can't: under homomorphic encryption, at low bit-widths, and inside tight latency and memory budgets.

M.Sc. Computer Science at Acadia University (GPA 4.21/4.30). 4 peer-reviewed papers. About 950 GPU-hours of experiments on Digital Research Alliance of Canada clusters. Production MLOps with MLflow, Docker, CI/CD and AWS.

Open to full-time ML engineering roles from May 2027. Open to relocation.

---

## Featured work

### HE-NAS: architecture search for encrypted inference on a SLURM cluster
*Acadia Institute for Data Analytics, with Dr. Andrew McIntyre · PyTorch, NSGA-II, CKKS, SLURM*
<!-- add repo link -->

Evolves a CNN and its CKKS encryption parameters together in one genome, under a 128-bit security constraint.

- **Scale:** 190 searches (6 conditions × 30 seeds), about 950 GPU-hours on Digital Research Alliance of Canada SLURM clusters.
- **Running it on a shared cluster:** one-shot job submission for the whole campaign, and seed-level resumption so a job killed by the wall-clock limit picks up where it stopped instead of restarting.
- **Measured before trusting the model:** profiled the encryption library's real level consumption before the main runs. The standard depth model underestimated cost by 2×, and expert designs built on it failed all 30 runs.
- **Real encrypted execution:** retrained 11 evolved champions at full scale and ran them under encryption. 10 of 11 decrypted correctly, best at 85.6% CIFAR-10 accuracy, 93 to 955 ms latency, 156 to 256-bit security.
- **Honest statistics:** Mann-Whitney U with Holm correction, Cohen's d, Vargha-Delaney A12. Result: joint search ties a simpler encryption-first design at 2.8× the compute. Reported as a null result.
- **Code:** consolidated 23 research files into 7 modules behind one CLI. Paper, report and slides are generated straight from result files.

### Chest CT cancer classification: end-to-end MLOps pipeline
*TensorFlow, Optuna, MLflow, DVC, FastAPI, Streamlit, Docker, GitHub Actions*
<!-- add repo link -->

- Four-class CT classifier with DVC data versioning and an Optuna search over backbone and hyperparameters, each trial logged as a nested MLflow run.
- MLflow model registry plus automated evaluation that logs metrics and confusion matrices.
- Served through a FastAPI `/predict` endpoint and a Streamlit UI, as two lean Docker images under Docker Compose.
- GitHub Actions runs the pytest suite, then builds and pushes both images to GitHub Container Registry on every merge to main.

### Quantized encrypted mammogram classifier · IEEE SysCon 2026
*Concrete ML (TFHE), Brevitas quantization-aware training*
<!-- add repo link -->

- 3-class classifier on 26,602 images unified from INbreast, MIAS and DDSM.
- Swept 2 to 6-bit quantization. The 3-bit model kept 86.0% accuracy at 74 s per encrypted inference, 27.5× faster than the most accurate 5-bit model (89.7%, 34 min).
- Designed a shallow, wide CNN for encrypted execution: 24× faster than MobileNetV2-Lite and more accurate (86.0% vs 83.2%).
- Found the compiler's memory wall: deep and residual graphs blew past 128 GB of RAM at compile time. Topology, not parameter count, decides feasibility.

### Encrypted tool-calling for AI agents
*BFV private information retrieval, CKKS, Python*
<!-- add repo link -->

- Threat model for agents calling external tools: what an honest-but-curious server learns, and whether it can rebuild user intent across calls.
- Prototype: an encrypted drug-interaction checker. 0 bits of query content leaked, 1.9 s end-to-end over 10,000 records, 100% correct on 100 patients, intent-reconstruction attack accuracy cut from 100% to 33%.
- Profiled the bottlenecks: a 105.6 MB PIR response and rotation keys taking 96% of a 171 MB context.
- 13,000 lines, 119 tests, one-command reproduction.

### M.Sc. thesis: channel-adaptive polynomial activations under RNS-CKKS
*PyTorch, HEonGPU, OpenFHE, CUDA Docker, SLURM*

- Tested per-channel polynomial degrees on ResNet-20 and MobileNetV2 against failure conditions registered before any measurement, and showed three independent reasons the saving can't materialize (two by proof).
- Standalone finding: at fixed encryption cost, how you set each channel's approximation range matters far more than the polynomial degree.
- Exact dynamic-programming placement solver, matching brute force on 720 of 720 cases.
- Reproducible by design: 45 tests, every result stamped with git commit, timestamp and command, clean-tree check before any run.

---

## Publications

1. **M. Khattab**, L. Bouzar-Benlabiod. *Memory-Efficient Quantization-Aware Optimization for FHE-Based Mammogram Classification.* IEEE SysCon, 2026.
2. **M. Khattab**, A. Eaman. *Benchmarking Fully Homomorphic Encryption for Deep Neural Network Inference: A Systematic Study of CKKS Parameter Trade-offs.* MobiSPC, Procedia Computer Science (Elsevier), 2026.
3. **M. Khattab**, L. Bouzar-Benlabiod. *Pure Leveled CKKS for CNN Inference: The Finite Limb Depth Bound and ResNet-20 Stress-Test.* Canadian AI Graduate Student Symposium, PMLR vol. 318, 2026.
4. L. Hassan, **M. Khattab**, K. Mohamed. *Detecting Abnormalities from Chest X-ray Images: Optimized Learning Approach.* ITAF 2024, Springer.

In preparation: a systematic literature review of FHE acceleration for deep learning inference (166 studies), and a paper on encryption-parameter design order in architecture search.

---

## Tools I use

**ML:** PyTorch, TensorFlow/Keras, scikit-learn, Optuna, pandas, NumPy
**MLOps:** MLflow, DVC, Docker, Docker Compose, GitHub Actions, FastAPI, Streamlit, pytest, Grafana, PostgreSQL
**Cloud & HPC:** AWS (SageMaker, Lambda, EC2), SLURM, CUDA containers, Digital Research Alliance of Canada clusters
**Inference optimization:** quantization-aware training (Brevitas, 2 to 6-bit), latency and memory profiling
**Privacy-preserving ML:** CKKS, TFHE, BFV with OpenFHE, HEonGPU, Concrete ML, TenSEAL
**Languages:** Python, SQL, C++, TypeScript, Bash

---

## Currently building

An LLM inference benchmark: serving an open-weights model with vLLM and measuring p50/p95/p99 latency, throughput and cost per 1k requests across quantization and batching settings.

---

## Contact

[LinkedIn](https://linkedin.com/in/mohamed-khattab-ai) · [Email](mailto:muhammedalaa1412@gmail.com)
