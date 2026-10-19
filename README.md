# Hi, I'm Mohamed Khattab

ML engineer focused on inference: making models fast, cheap, and production-ready.

My research works on the hardest version of that problem. Running a neural network under homomorphic encryption keeps data private, but it is extremely slow: a single encrypted image can take over 30 minutes. I attack that bottleneck with the same tools used to optimize production inference (quantization, architecture search, GPU acceleration, profiling) and ship the work with production MLOps discipline (Docker, CI/CD, tests, experiment tracking).

M.Sc. Computer Science at Acadia University (GPA 4.21/4.30), 4 peer-reviewed papers, and industry experience deploying ML models to production on AWS (SageMaker, Lambda, EC2). Open to full-time ML engineering roles from May 2027, and open to relocation.

---

## Featured work

### Chest CT cancer classification: end-to-end MLOps pipeline
*TensorFlow, Optuna, MLflow, DVC, FastAPI, Streamlit, Docker Compose, pytest, GitHub Actions, GHCR*

A four-class CT classifier built as a full ML lifecycle, not a notebook.

- **Data versioning:** datasets tracked with DVC, so every model traces back to the exact data it was trained on.
- **Experiment tracking:** Optuna search over backbone and hyperparameters, each trial logged as a nested MLflow run.
- **Model registry:** the selected model is registered in MLflow, with automated evaluation logging metrics and confusion matrices.
- **Serving:** a FastAPI `/predict` endpoint and a Streamlit UI, shipped as two lean Docker images orchestrated with Docker Compose.
- **CI/CD:** GitHub Actions runs the pytest suite, then builds and pushes both images to GitHub Container Registry on every merge to main.

### Cutting encrypted inference from 34 minutes to 74 seconds · IEEE SysCon 2026
*Concrete ML, Brevitas quantization-aware training, PyTorch*

- **Bottleneck:** encrypted mammogram classification (26,602 images) took 34 minutes per image at 5-bit precision.
- **Quantization:** swept 2 to 6-bit quantization-aware training and measured the accuracy cost of each bit-width. The 3-bit model runs in 74 s, 27.5× faster, at 86.0% vs 89.7% accuracy.
- **Architecture for the target:** designed a shallow, wide CNN around the cost of encrypted execution. It ran 24× faster than MobileNetV2-Lite and was more accurate (86.0% vs 83.2%). Grayscale input cut latency a further 32.3%.
- **Memory profiling:** found that deep and residual graphs exceed 128 GB of RAM at compile time. Graph topology, not parameter count, decides what can run.

### GPU-accelerated encrypted CNN inference · M.Sc. thesis and PMLR 2026
*PyTorch, HEonGPU, OpenFHE, C++/CUDA, Docker, SLURM*

- **GPU pipeline:** built a GPU-accelerated encrypted CNN pipeline with SVD kernel decomposition and integer quantization, verified to a maximum error of 2.25 × 10⁻⁴.
- **Profiling the budget:** stress-tested ResNet-20 and showed residual shortcuts consume the encryption depth budget linearly, exhausting it exactly where predicted (after 169,741 rotations and 555.7 s).
- **Knowing what works:** showed, with three independent reasons (two of them proofs), that per-channel activation degrees can't deliver their promised saving, and found what does matter: how each channel's approximation range is set beats polynomial degree at fixed cost.
- **Solver:** exact dynamic-programming placement solver, matching brute force on 720 of 720 cases.
- **Engineering:** 45 tests, every result stamped with git commit, timestamp and command, runs blocked on a dirty working tree, CUDA Docker images so the same code runs locally and on the cluster.

### HE-NAS: searching for fast encrypted models on a remote GPU cluster
*Acadia Institute for Data Analytics, with Dr. Andrew McIntyre · PyTorch, NSGA-II, CKKS, SLURM*

- **Bottleneck:** hand-designed architectures ignore the real cost of encrypted execution.
- **Architecture search:** evolves a CNN and its encryption parameters together, trading accuracy against inference cost under a 128-bit security constraint.
- **Measure before optimizing:** profiled real encryption cost before the main runs and found the standard cost model was off by 2×. Expert designs built on it failed all 30 runs.
- **Cluster workflow:** ran the campaign (6 conditions × 30 seeds) on Digital Research Alliance of Canada clusters over SSH, with SLURM batch scripts, one-shot submission, and per-seed checkpoint and resume across wall-clock limits.
- **Result:** 10 of 11 evolved models ran correctly under real encryption, best at 85.6% CIFAR-10 accuracy and 93 to 955 ms latency. Statistical testing (Mann-Whitney U, Holm correction, effect sizes) showed a tie with a simpler design at 2.8× the compute, reported as a null result.
- **Engineering:** consolidated 23 research files into 7 modules behind one CLI. The paper, report and slides are generated directly from result files.

### Private tool-calling for AI agents
*BFV private information retrieval, CKKS, Python*

- Encrypted drug-interaction checker: 0 bits of query content leaked, 1.9 s end-to-end over 10,000 records, intent-reconstruction attack accuracy cut from 100% to 33%.
- **Profiling:** traced latency and memory to a 105.6 MB server response and rotation keys taking 96% of a 171 MB context.
- **Engineering:** 13,000 lines, 119 tests, one-command reproduction.

---

## Efficient ML

I make models cheaper to run and measure exactly what each optimization costs in accuracy.

- **Quantization:** low-bit quantization down to 2 bits, with the accuracy cost of every bit-width measured.
- **Pruning and sparsity:** removing redundant weights and channels to cut model size and latency.
- **Knowledge distillation:** training small student models to match larger teachers.
- **Neural architecture search:** multi-objective search over whatever the deployment needs: accuracy, latency, memory, model size, a specific hardware target, or throughput at a required request rate.
- **Hardware-aware model design:** shaping the architecture around the cost of the execution target.
- **LLM inference:** KV cache, low-bit weight quantization for LLMs, and batching for serving throughput.
- **GPU kernels:** writing CUDA kernels from scratch and in Triton (memory coalescing, shared-memory tiling, kernel fusion), benchmarked against the PyTorch equivalent.
- **Profiling:** finding where latency and memory actually go with NVIDIA Nsight Systems, Nsight Compute and the PyTorch Profiler, and telling compute-bound from memory-bound work before changing anything.

---

## Tools I use

| Area | Tools |
| --- | --- |
| **Languages** | Python, C++, CUDA, SQL, TypeScript, Bash |
| **ML and inference** | PyTorch, TensorFlow/Keras, scikit-learn, Optuna, vLLM, Brevitas, pandas, NumPy |
| **MLOps, cloud and data** | MLflow, DVC, Docker, Docker Compose, GitHub Actions, GitHub Container Registry, FastAPI, Streamlit, pytest, Grafana, AWS (SageMaker, Lambda, EC2), PostgreSQL, MySQL, Tableau, Power BI |
| **GPU and HPC** | Triton, Nsight Systems, Nsight Compute, PyTorch Profiler, SLURM (job arrays, checkpoint and resume), SSH, Linux, CUDA containers |
| **Privacy-preserving ML** | OpenFHE, HEonGPU, Concrete ML, TenSEAL (CKKS, TFHE, BFV) |

---

## Currently working on

- **LLM inference benchmark:** serving an open-weights model with vLLM and measuring p50/p95/p99 latency, throughput and cost per 1k requests across quantization and batching settings, with a profiling trace showing where the time goes.
- **GPU kernels:** writing Triton and CUDA kernels (softmax, fused ops) and benchmarking each against the PyTorch equivalent.

---

## Publications

1. **M. Khattab**, L. Bouzar-Benlabiod. *Memory-Efficient Quantization-Aware Optimization for FHE-Based Mammogram Classification.* IEEE SysCon, 2026.
2. **M. Khattab**, A. Eaman. *Benchmarking Fully Homomorphic Encryption for Deep Neural Network Inference: A Systematic Study of CKKS Parameter Trade-offs.* MobiSPC, Procedia Computer Science (Elsevier), 2026.
3. **M. Khattab**, L. Bouzar-Benlabiod. *Pure Leveled CKKS for CNN Inference: The Finite Limb Depth Bound and ResNet-20 Stress-Test.* Canadian AI Graduate Student Symposium, PMLR vol. 318, 2026.
4. L. Hassan, **M. Khattab**, K. Mohamed. *Detecting Abnormalities from Chest X-ray Images: Optimized Learning Approach.* ITAF 2024, Springer.

---

## Contact

[LinkedIn](https://linkedin.com/in/mohamed-khattab-ai) · [Email](mailto:muhammedalaa1412@gmail.com)
