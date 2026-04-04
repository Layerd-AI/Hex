# Hex - AI Model Security Scanner by Layerd AI

<div align="center">

![Version](https://img.shields.io/badge/version-v3.0.0-blue)
![Scanners](https://img.shields.io/badge/scanners-30-green)
![Docker Pulls](https://img.shields.io/docker/pulls/layerd/hex)
![Image Size](https://img.shields.io/docker/image-size/layerd/hex/latest)
![Go Version](https://img.shields.io/badge/Go-1.21+-00ADD8?logo=go)
![License](https://img.shields.io/badge/license-MIT-green)
![Security](https://img.shields.io/badge/security-hardened-red)

**Enterprise-Grade AI/ML Model Security Scanner**

**v3.0.0 Released - 30 Security Scanners | 18 New Advanced AI Security Features**

[Website](https://hex.layerd.com) | [GitHub](https://github.com/Layerd-AI/layerd-hex) | [Support](mailto:support@layerd.com) | [Documentation](https://hex.layerd.com/docs) | [Release Notes](./RELEASES.md)

</div>

## Overview

Hex is an enterprise-grade security scanner specifically designed for AI/ML models, providing comprehensive protection against supply chain attacks, vulnerabilities, and compliance violations. Built by Layerd AI, Hex delivers mission-critical security for AI infrastructure with real-time threat intelligence, advanced detection capabilities, and comprehensive AI/ML metadata extraction for governance and compliance.

## Key Features

### Comprehensive Security Coverage (30 Scanner Modules)

#### Core Security Features
- **Supply Chain Security**: Detects vulnerable dependencies, malicious packages, and compromised models
- **Adversarial Robustness**: Analyzes model resilience against adversarial attacks (FGSM, PGD, Lipschitz continuity)
- **Backdoor Detection**: Identifies hidden backdoors and trigger patterns using Neural Cleanse and activation analysis
- **Data Privacy**: Detects PII leakage, model inversion risks, and memorization vulnerabilities
- **LLM Security**: Protects against prompt injection, jailbreaks, and excessive agency risks
- **License Compliance**: Ensures GPL compliance and license compatibility

#### Advanced AI/ML Security Features (NEW)
- **Model Poisoning Detection**: Identifies data poisoning, gradient poisoning, and label flipping attacks in training datasets
- **Federated Learning Security**: Detects Byzantine attacks, aggregation tampering, and client authentication issues
- **Model Extraction Prevention**: Monitors API query patterns and detects model stealing attempts
- **Differential Privacy Verification**: Validates privacy budget, noise calibration, and membership inference resistance
- **Explainability Attack Detection**: Identifies SHAP/LIME manipulation and saliency map poisoning
- **Model Watermarking & Fingerprinting**: Detects embedded watermarks and verifies model ownership
- **Quantization Security**: Identifies bit-flip attacks and compression-induced vulnerabilities
- **Multi-Modal Security**: Protects against cross-modal injection and alignment manipulation
- **RAG Security**: Detects knowledge base poisoning, vector DB manipulation, and context injection
- **Model Drift Monitoring**: Tracks performance degradation and concept drift
- **Homomorphic Encryption Compatibility**: Verifies FHE readiness and encrypted inference support
- **Zero-Knowledge Proof Integration**: Validates privacy-preserving audit trails
- **Synthetic Data Detection**: Identifies AI-generated training data and deepfakes
- **Model Behavior Anomaly Detection**: Monitors runtime anomalies and unexpected outputs
- **Supply Chain Provenance**: Blockchain-based lineage tracking and tamper detection
- **Regulatory Compliance**: GDPR/CCPA compliance, EU AI Act readiness, bias auditing
- **Edge Deployment Security**: Verifies model obfuscation and side-channel resistance
- **AutoML Security**: Detects NAS poisoning and hyperparameter manipulation

### Advanced Detection Capabilities

- **Model Discovery**: Automatically identifies 15+ ML model formats (.safetensors, .pth, .onnx, .bin, .h5, .pkl, .joblib, .tf, .tflite, .mlmodel, .pt, .model, .weights, .caffemodel, .pb)
- **Pickle Security**: Deep inspection of pickle files for arbitrary code execution risks
- **Entropy Analysis**: Statistical analysis to detect hidden malicious payloads
- **Signature Verification**: Cryptographic verification of model integrity
- **Model Card Extraction**: Automatic parsing of README.md, config.json, and model_card.md files
- **Training Metadata**: Captures framework versions, hyperparameters, and architecture details
- **Dataset Provenance**: Tracks data sources, preprocessing steps, and ethical reviews
- **Real-time CVE Database**: Live vulnerability feeds from NVD and OSV databases
- **CVSS v3.1 Scoring**: Industry-standard vulnerability scoring with EPSS integration

### Enterprise Features

- **SBOM Generation**: Multi-format support (JSON, CycloneDX, SPDX 2.3) with AI/ML metadata
- **AI/ML Model Cards**: Automatic extraction of model documentation and metadata
- **Training Provenance**: Captures training framework, parameters, and device information
- **Dataset Lineage**: Tracks dataset sources, licenses, and preprocessing details
- **Supply Chain Attestations**: SLSA and in-toto attestation support
- **Multiple Output Formats**: JSON, SARIF, Table, Text, XML for CI/CD integration
- **Configurable Scanning**: Granular control over scan depth and timeout settings
- **Finding Deduplication**: Intelligent tracking to prevent duplicate alerts
- **Parallel Processing**: Multi-threaded scanning with configurable worker pools
- **Low False Positives**: Advanced heuristics minimize alert fatigue

## Quick Start

### What's New in v3.0.0
- **18 new advanced AI security scanners** for comprehensive threat detection
- **RAG Security**: Complete protection for retrieval augmented generation systems
- **Federated Learning Security**: Byzantine attack and aggregation tampering detection
- **Model Poisoning Detection**: Data and gradient poisoning identification
- **Regulatory Compliance**: GDPR, CCPA, and EU AI Act compliance checking
- See [Release Notes](./RELEASES.md) for complete list

### Basic Usage

```bash
# Scan current directory with all 30 scanners
docker run --rm -v $(pwd):/scan:ro layerd/hex:3.0.0 /scan

# Scan specific model file
docker run --rm -v $(pwd):/scan:ro layerd/hex:3.0.0 /scan/model.safetensors

# Generate JSON report with new v3 features
docker run --rm -v $(pwd):/scan:ro layerd/hex:3.0.0 /scan --json > report.json

# Scan with specific new scanners only
docker run --rm -v $(pwd):/scan:ro layerd/hex:3.0.0 /scan \
  --skip adversarial,backdoor,llm \
  --verbose

# Focus on RAG system security
docker run --rm -v $(pwd):/scan:ro layerd/hex:3.0.0 /scan/rag_system \
  --skip model-poisoning,federated,differential \
  --json
```

### Production Deployment

```bash
# Scan with security options enabled
docker run --rm \
  --security-opt=no-new-privileges:true \
  --cap-drop=ALL \
  --read-only \
  -v $(pwd):/scan:ro \
  layerd/hex:latest /scan --verbose

# Generate SBOM for compliance (JSON format with AI/ML metadata)
docker run --rm \
  -v $(pwd):/scan:ro \
  -v $(pwd)/output:/output \
  layerd/hex:latest /scan --sbom /output/sbom.json

# Generate SBOM in SPDX format (ISO/IEC 5962:2021 standard)
docker run --rm \
  -v $(pwd):/scan:ro \
  -v $(pwd)/output:/output \
  layerd/hex:latest /scan --sbom /output/sbom.spdx.json --sbom-format spdx

# Generate SBOM in CycloneDX format with ML-MODEL components
docker run --rm \
  -v $(pwd):/scan:ro \
  -v $(pwd)/output:/output \
  layerd/hex:latest /scan --sbom /output/sbom.cdx.json --sbom-format cyclonedx

# CI/CD Integration with timeout
docker run --rm \
  -v $(pwd):/scan:ro \
  -e HEX_TIMEOUT=600 \
  layerd/hex:latest /scan --format json --output /scan/results.json
```

## Installation

### Docker (Recommended)

```bash
# Pull the latest image
docker pull layerd/hex:latest

# Run a scan
docker run --rm -v $(pwd):/scan:ro layerd/hex:latest /scan
```

### From Source

```bash
# Clone the repository
git clone https://github.com/Layerd-AI/layerd-hex.git
cd layerd-hex

# Build the binary
go build -o hex ./cmd/hex

# Install to system (optional)
sudo mv hex /usr/local/bin/
```

### Using Go

```bash
go install github.com/Layerd-AI/layerd-hex/cmd/hex@latest
```

## Configuration Options

### Command Line Arguments

| Flag | Description | Default |
|------|-------------|---------|
| `--verbose, -v` | Enable detailed output | false |
| `--recursive, -r` | Scan directories recursively | true |
| `--workers, -w` | Number of parallel workers | 4 |
| `--timeout` | Scan timeout in seconds | 300 |
| `--format, -f` | Output format (text/json/table) | text |
| `--output, -o` | Output file path | stdout |
| `--sbom` | Generate SBOM with AI/ML metadata | - |
| `--sbom-format` | SBOM format (json/spdx/cyclonedx) | json |
| `--skip` | Skip specific scanners | - |
| `--clear` | Clear previous findings | false |
| `--json` | Shorthand for --format json | false |

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `HEX_TIMEOUT` | Global timeout override | 300 |
| `HEX_VERBOSE` | Enable verbose logging | false |
| `HEX_WORKERS` | Worker pool size | 4 |
| `NO_COLOR` | Disable colored output | false |

## Docker Compose Integration

```yaml
version: '3.8'

services:
  hex-scanner:
    image: layerd/hex:latest
    volumes:
      - ./models:/scan:ro
      - ./reports:/output
    environment:
      - HEX_VERBOSE=true
      - HEX_TIMEOUT=600
    command: ["/scan", "--json", "--output", "/output/report.json"]
    security_opt:
      - no-new-privileges:true
    cap_drop:
      - ALL
    read_only: true
    user: "1000:1000"
```

## CI/CD Integration

### GitHub Actions

```yaml
- name: Security Scan with Hex
  uses: docker://layerd/hex:latest
  with:
    args: /github/workspace --json --output scan-results.json

- name: Upload Results
  uses: github/codeql-action/upload-sarif@v2
  with:
    sarif_file: scan-results.json
```

### GitLab CI

```yaml
security_scan:
  image: layerd/hex:latest
  script:
    - hex . --json > security-report.json
  artifacts:
    reports:
      security: security-report.json
```

### Jenkins Pipeline

```groovy
stage('Security Scan') {
  agent {
    docker {
      image 'layerd/hex:latest'
      args '-v $WORKSPACE:/scan:ro'
    }
  }
  steps {
    sh 'hex /scan --json --output /scan/hex-report.json'
    archiveArtifacts 'hex-report.json'
  }
}
```

## Security Compliance

### Container Security

- **Non-root execution**: Runs as UID 1000 (hex user)
- **Read-only filesystem**: Supports read-only root filesystem
- **Minimal attack surface**: Alpine-based image (~64MB)
- **No shell access**: Security-hardened container
- **Signed images**: Cosign signatures for authenticity
- **Regular updates**: Weekly vulnerability scans and patches

### Compliance Standards

- **CWE Coverage**: Maps to 50+ Common Weakness Enumerations
- **OWASP Top 10**: Addresses AI/ML specific security risks
- **NIST AI RMF**: Aligns with NIST AI Risk Management Framework
- **EU AI Act**: Supports compliance requirements
- **SOC 2**: Audit-ready security controls

## Advanced Usage

### AI/ML Metadata Extraction

```bash
# Extract model card and training information
docker run --rm -v $(pwd):/scan:ro \
  layerd/hex:latest /scan \
  --sbom model-metadata.json

# Generate SPDX SBOM with full AI/ML provenance
docker run --rm -v $(pwd):/scan:ro \
  layerd/hex:latest /scan \
  --sbom-format spdx \
  --sbom model-provenance.spdx.json
```

### Vulnerability Database Updates

```bash
# Update vulnerability database
docker run --rm \
  -v hex-data:/home/hex/.layerd/hex \
  layerd/hex:latest vulnfetch fetch

# Schedule automatic updates (cron)
0 */6 * * * docker run -v hex-data:/home/hex/.layerd/hex layerd/hex:latest vulnfetch fetch
```

### Custom Scanner Configuration

```bash
# Skip specific scanners
docker run --rm -v $(pwd):/scan:ro \
  layerd/hex:latest /scan \
  --skip entropy,metadata

# Focus on critical vulnerabilities only
docker run --rm -v $(pwd):/scan:ro \
  layerd/hex:latest /scan \
  --severity critical,high
```

### Batch Processing

```bash
# Scan multiple directories with SBOM generation
for dir in model1 model2 model3; do
  docker run --rm -v $(pwd)/$dir:/scan:ro \
    layerd/hex:latest /scan \
    --json > results-$dir.json \
    --sbom sbom-$dir.json
done
```

## Output Examples

### JSON Output Structure

```json
{
  "summary": {
    "total_issues": 15,
    "critical": 2,
    "high": 5,
    "medium": 6,
    "low": 2,
    "security_score": 72,
    "security_grade": "C",
    "verdict": "UNSAFE - High severity vulnerabilities detected"
  },
  "results": [
    {
      "id": "CVE-2023-45857",
      "type": "vulnerability",
      "severity": "CRITICAL",
      "title": "Arbitrary code execution in pickle file",
      "description": "Unsafe deserialization vulnerability",
      "file_path": "/scan/model.pkl",
      "line_number": 42,
      "confidence": 0.95,
      "cvss": {
        "version": "3.1",
        "vector_string": "CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H",
        "base_score": 9.8,
        "base_severity": "CRITICAL"
      },
      "cwe": ["CWE-502"],
      "remediation": "Avoid using pickle files or implement secure deserialization",
      "references": [
        "https://nvd.nist.gov/vuln/detail/CVE-2023-45857"
      ]
    }
  ]
}
```

### Command Line Output

```
╔══════════════════════════════════════════╗
║       Hex AI Model Scanner v3.0.0        ║
║            by Layerd AI                  ║
║       https://hex.layerd.com            ║
╚══════════════════════════════════════════╝

Scanning: /models/production
Mode: Directory
Scanners: 30 active (including AI/ML metadata)
Workers: 4

Scanning 100% [========================================]

Scan Summary
──────────────────────────────────────────
Total Issues: 5
  ● Critical: 1 (CVE-2023-25801)
  ● High: 2 (CVE-2022-45907, CVE-2022-35934)
  ● Medium: 2 (CVE-2021-41495)

Security Score: B (85/100)
Verdict: UNSAFE - High severity vulnerabilities detected

[1] Vulnerable package: tensorflow CVE-2023-25801
    CVSS: 9.8 (v3.1) - Critical
    CWE: CWE-190, CWE-787
    Fix: Update to tensorflow 2.11.1 or later
```

## Performance Benchmarks

| Model Size | Files | Scan Time | Memory Usage |
|------------|-------|-----------|--------------|
| < 100 MB | 10 | ~5 seconds | < 50 MB |
| 100 MB - 1 GB | 50 | ~30 seconds | < 100 MB |
| 1 GB - 10 GB | 100 | ~2 minutes | < 200 MB |
| > 10 GB | 500+ | ~10 minutes | < 500 MB |

## Architecture

Hex v2.1+ features 30 specialized security scanners organized in a modular architecture:

```
┌──────────────────────────────────────────────────┐
│             Hex Scanner Core v2.1+              │
├──────────────────────────────────────────────────┤
│                Core Scanners                     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐     │
│  │Discovery │  │  Pickle  │  │ Manifest │     │
│  │ Engine   │  │ Detector │  │ Scanner  │     │
│  └──────────┘  └──────────┘  └──────────┘     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐     │
│  │Entropy   │  │Metadata  │  │Signature │     │
│  │Analyzer  │  │Inspector │  │Verifier  │     │
│  └──────────┘  └──────────┘  └──────────┘     │
├──────────────────────────────────────────────────┤
│            Security Scanners                     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐     │
│  │Adversarial│ │ Backdoor │  │   LLM    │     │
│  │Robustness│ │ Detector │  │ Security │     │
│  └──────────┘  └──────────┘  └──────────┘     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐     │
│  │ Privacy  │  │ License  │  │Model Card│     │
│  │ Leakage  │  │Compliance│  │Extractor │     │
│  └──────────┘  └──────────┘  └──────────┘     │
├──────────────────────────────────────────────────┤
│        Advanced AI Security (NEW)                │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐     │
│  │Poisoning │  │Federated │  │   RAG    │     │
│  │Detection │  │ Learning │  │ Security │     │
│  └──────────┘  └──────────┘  └──────────┘     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐     │
│  │Extraction│  │Differential│ │Explainability│ │
│  │Prevention│  │ Privacy  │  │  Attack   │     │
│  └──────────┘  └──────────┘  └──────────┘     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐     │
│  │Watermark │  │Quantization│ │Multi-Modal│    │
│  │Detection │  │ Security │  │ Security  │     │
│  └──────────┘  └──────────┘  └──────────┘     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐     │
│  │  Drift   │  │Homomorphic│ │ ZK Proof │     │
│  │ Monitor  │  │Encryption│  │Integration│     │
│  └──────────┘  └──────────┘  └──────────┘     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐     │
│  │Synthetic │  │ Behavior │  │Provenance│     │
│  │   Data   │  │ Anomaly  │  │ Tracking │     │
│  └──────────┘  └──────────┘  └──────────┘     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐     │
│  │Regulatory│  │   Edge   │  │  AutoML  │     │
│  │Compliance│  │ Security │  │ Security │     │
│  └──────────┘  └──────────┘  └──────────┘     │
├──────────────────────────────────────────────────┤
│         Vulnerability Database                   │
│      (CVE, CVSS, CWE, EPSS Data)               │
├──────────────────────────────────────────────────┤
│       AI/ML Metadata Enrichment                  │
│    (Training Info, Model Cards, SBOM)           │
└──────────────────────────────────────────────────┘
```

## Supply Chain Security

Hex Docker images include comprehensive supply chain attestations:

- **SLSA Provenance**: Build provenance with source verification
- **SBOM Attestation**: Complete dependency inventory in CycloneDX format
- **Cosign Signatures**: Keyless signing via Sigstore for authenticity

Verify image authenticity:
```bash
cosign verify layerd/hex:latest \
  --certificate-identity-regexp "https://github.com/Layerd-AI/layerd-hex" \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com
```

## Troubleshooting

### Common Issues

```bash
# Permission denied errors
docker run --rm -v $(pwd):/scan:ro --user $(id -u):$(id -g) layerd/hex:latest /scan

# Timeout on large files
docker run --rm -v $(pwd):/scan:ro -e HEX_TIMEOUT=1800 layerd/hex:latest /scan

# Memory constraints
docker run --rm -m 1g -v $(pwd):/scan:ro layerd/hex:latest /scan
```

## Support and Resources

### Documentation
- Full Documentation: https://hex.layerd.com/docs

### Support Channels
- Enterprise Support: support@layerd.com
- GitHub Issues: https://github.com/Layerd-AI/Hex/issues

### License
- Open Source: MIT License
- Enterprise: Contact hello@layerd.com for commercial licensing

## Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

## About Layerd AI

Layerd AI is a leader in AI/ML security, providing enterprise-grade solutions for securing the AI supply chain. Our mission is to enable organizations to deploy AI safely and confidently.

Visit [https://hex.layerd.com](https://hex.layerd.com) to learn more.

---

Copyright © 2026 Layerd AI. All rights reserved.
