# Hex Release Notes

## Version 3.0.0 (2026-04-04)
### Major Release - Advanced AI Security Suite

#### New Features (18 Advanced Security Scanners)
- **Model Poisoning Detection**: Comprehensive detection of data poisoning, gradient poisoning, and label flipping attacks in training datasets with statistical outlier analysis
- **Federated Learning Security**: Byzantine attack detection, aggregation tampering prevention, and client authentication verification for distributed learning systems
- **Model Extraction Prevention**: API query pattern analysis and rate limiting recommendations to prevent model stealing attempts
- **RAG Security**: Complete security suite for Retrieval Augmented Generation systems including knowledge base poisoning detection, vector database manipulation, and context injection prevention
- **Differential Privacy Verification**: Privacy budget analysis, noise calibration verification, and membership inference attack resistance testing
- **Explainability Attack Detection**: SHAP/LIME manipulation detection, saliency map poisoning identification, and feature attribution tampering prevention
- **Model Watermarking & Fingerprinting**: Embedded watermark detection, model ownership verification, and unauthorized copy identification
- **Quantization & Compression Security**: Bit-flip attack detection, compression-induced vulnerability scanning, and pruning attack identification
- **Multi-Modal Security**: Cross-modal injection attack prevention, image-text alignment manipulation detection, and audio-visual desync attack identification
- **Model Drift & Degradation Monitoring**: Performance degradation detection, distribution shift analysis, and concept drift identification
- **Homomorphic Encryption Compatibility**: FHE-ready model verification, encrypted inference support checking, and secure computation readiness assessment
- **Zero-Knowledge Proof Integration**: Model prediction verification without model disclosure, training data integrity proofs, and privacy-preserving audit trails
- **Synthetic Data Detection**: AI-generated training data identification, deepfake detection in datasets, and data authenticity verification
- **Model Behavior Anomaly Detection**: Runtime behavior monitoring, unexpected output pattern detection, and decision boundary manipulation identification
- **Supply Chain Provenance Tracking**: Blockchain-based model lineage, tamper-evident history tracking, and dependency trust scoring
- **Regulatory Compliance Scanner**: GDPR/CCPA compliance checking, EU AI Act readiness assessment, and bias/fairness auditing
- **Edge Deployment Security**: Model obfuscation verification, side-channel attack resistance testing, and hardware-specific vulnerability detection
- **AutoML Security**: Neural Architecture Search (NAS) poisoning detection, hyperparameter manipulation identification, and automated pipeline vulnerability scanning

#### Enhancements
- Increased total scanner count from 12 to 30 modules
- Enhanced architecture for parallel scanning of multiple security dimensions
- Improved vulnerability detection accuracy with advanced heuristics
- Expanded support for emerging AI/ML attack vectors

#### Breaking Changes
- Scanner registry now requires explicit module registration
- Some CLI flags have been reorganized for better grouping

---

## Version 2.0.0 (2025-12-15)
### Enterprise Security Features

#### New Features
- **Adversarial Robustness Scanner**: Analyzes model resilience against FGSM, PGD attacks, and Lipschitz continuity
- **Backdoor Detection**: Neural Cleanse algorithm implementation, activation distribution analysis, and known backdoor signature detection
- **LLM Security**: Comprehensive prompt injection detection, jailbreak prevention, system prompt leakage protection, and excessive agency detection
- **Privacy Leakage Scanner**: PII detection in model weights, model inversion attack resistance, and memorization vulnerability assessment
- **License Compliance**: GPL compliance verification, license compatibility checking, and dependency license analysis

#### Enhancements
- **Real-time CVE Database**: Integration with NVD and OSV databases for live vulnerability feeds
- **CVSS v3.1 Scoring**: Industry-standard vulnerability scoring with EPSS integration
- **SBOM Generation**: Multi-format support (JSON, CycloneDX, SPDX 2.3) with AI/ML metadata
- **Model Card Extraction**: Automatic parsing of README.md, config.json, and model_card.md files
- **Training Metadata Capture**: Framework versions, hyperparameters, and architecture details extraction

#### Performance Improvements
- Parallel scanning with configurable worker pools (default: 4 workers)
- Intelligent file deduplication to prevent redundant scanning
- Memory-efficient streaming for large model files
- Optimized entropy analysis with sliding window approach

#### Bug Fixes
- Fixed false positives in pickle detector for legitimate NumPy arrays
- Resolved memory leak in large file processing
- Corrected SBOM generation for models with special characters in metadata

---

## Version 1.0.0 (2025-09-01)
### Initial Public Release

#### Core Features
- **Model Discovery Engine**: Automatic identification of 15+ ML model formats
  - Supported formats: .safetensors, .pth, .onnx, .bin, .h5, .pkl, .joblib, .tf, .tflite, .mlmodel, .pt, .model, .weights, .caffemodel, .pb
- **Pickle Security Scanner**: Deep inspection of pickle files for arbitrary code execution risks
- **Entropy Analyzer**: Statistical analysis to detect hidden malicious payloads
- **Signature Verifier**: Cryptographic verification of model integrity
- **Manifest Scanner**: Dependency vulnerability checking for ML frameworks
- **Metadata Inspector**: Extraction of model training information and parameters

#### Security Capabilities
- **Supply Chain Security**: Detection of vulnerable dependencies and malicious packages
- **CVE Detection**: Basic vulnerability database with known ML framework vulnerabilities
- **Suspicious Pattern Detection**: Identification of common malware indicators in model files
- **Code Execution Prevention**: Detection of unsafe deserialization patterns

#### Output Formats
- Text (human-readable CLI output)
- JSON (machine-readable format)
- Table (formatted vulnerability summary)

#### CLI Features
- Recursive directory scanning
- File and directory support
- Configurable timeout (default: 300 seconds)
- Verbose mode for detailed output
- Skip modules functionality

#### Docker Support
- Alpine-based lightweight container (~64MB)
- Non-root execution (UID 1000)
- Read-only filesystem support
- Security-hardened configuration

#### Initial Compliance
- CWE mapping for detected vulnerabilities
- Basic OWASP Top 10 coverage for AI/ML risks
- Foundation for future compliance features

---

## Upgrade Guide

### From v2.x to v3.0.0
1. Update Docker image: `docker pull layerd/hex:3.0.0`
2. New scanners are automatically enabled - use `--skip` flag to disable specific modules if needed
3. Review new findings as v3.0.0 detects many additional vulnerability types

### From v1.x to v2.0.0
1. Update Docker image: `docker pull layerd/hex:2.0.0`
2. SBOM format has been enhanced - regenerate existing SBOMs for full AI/ML metadata
3. Some CVE IDs have been updated to latest NVD format

### From v1.0.0
- First installation - follow README.md for setup instructions

---

## Version History Summary

| Version | Release Date | Scanners | Major Focus |
|---------|-------------|----------|-------------|
| 3.0.0 | 2026-04-04 | 30 | Advanced AI Security Suite |
| 2.1.3 | 2026-02-01 | 12 | Bug fixes and stability |
| 2.1.0 | 2026-01-15 | 12 | Performance optimizations |
| 2.0.0 | 2025-12-15 | 12 | Enterprise Security Features |
| 1.2.0 | 2025-11-01 | 7 | Enhanced detection accuracy |
| 1.1.0 | 2025-10-01 | 7 | Docker improvements |
| 1.0.0 | 2025-09-01 | 7 | Initial Public Release |

---

## Roadmap

### Version 3.1 (Q2 2026)
- Enhanced RAG security with real-time monitoring
- Improved federated learning Byzantine tolerance
- GUI dashboard for security findings

### Version 3.2 (Q3 2026)
- Cloud-native deployment options
- Integration with major MLOps platforms
- Advanced threat intelligence feeds

### Version 4.0 (Q4 2026)
- Automated remediation capabilities
- AI-powered vulnerability prediction
- Comprehensive API for enterprise integration

---

## Support

For questions, bug reports, or feature requests:
- GitHub Issues: https://github.com/Layerd-AI/Hex/issues
- Enterprise Support: support@layerd.com
- Documentation: https://hex.layerd.com/docs

---

Copyright © 2026 Layerd AI. All rights reserved.
