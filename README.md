# Hex - AI Model Security Scanner by Layerd AI

<div align="center">

![Version](https://img.shields.io/docker/v/layerd/hex?sort=semver&label=version)
![Docker Pulls](https://img.shields.io/docker/pulls/layerd/hex)
![Image Size](https://img.shields.io/docker/image-size/layerd/hex/latest)
![Go Version](https://img.shields.io/badge/Go-1.21+-00ADD8?logo=go)
![License](https://img.shields.io/badge/license-MIT-green)
![Security](https://img.shields.io/badge/security-hardened-red)

**Enterprise-Grade AI/ML Model Security Scanner**

[Website](https://www.layerd.com) | [GitHub](https://github.com/Layerd-AI/layerd-hex) | [Support](mailto:support@layerd.com) | [Documentation](https://www.layerd.com/docs/hex)

</div>

## Overview

Hex is an enterprise-grade security scanner specifically designed for AI/ML models, providing comprehensive protection against supply chain attacks, vulnerabilities, and compliance violations. Built by Layerd AI, Hex delivers mission-critical security for AI infrastructure with real-time threat intelligence and advanced detection capabilities.

## Key Features

### Comprehensive Security Coverage

- **Supply Chain Security**: Detects vulnerable dependencies, malicious packages, and compromised models
- **Adversarial Robustness**: Analyzes model resilience against adversarial attacks (FGSM, PGD, Lipschitz continuity)
- **Backdoor Detection**: Identifies hidden backdoors and trigger patterns using Neural Cleanse and activation analysis
- **Data Privacy**: Detects PII leakage, model inversion risks, and memorization vulnerabilities
- **LLM Security**: Protects against prompt injection, jailbreaks, and excessive agency risks
- **License Compliance**: Ensures GPL compliance and license compatibility

### Advanced Detection Capabilities

- **Model Discovery**: Automatically identifies 15+ ML model formats (.safetensors, .pth, .onnx, .bin, .h5, .pkl, .joblib, .tf, .tflite, .mlmodel, .pt, .model, .weights, .caffemodel, .pb)
- **Pickle Security**: Deep inspection of pickle files for arbitrary code execution risks
- **Entropy Analysis**: Statistical analysis to detect hidden malicious payloads
- **Signature Verification**: Cryptographic verification of model integrity
- **Real-time CVE Database**: Live vulnerability feeds from NVD and OSV databases
- **CVSS v3.1 Scoring**: Industry-standard vulnerability scoring with EPSS integration

### Enterprise Features

- **SBOM Generation**: CycloneDX-compliant Software Bill of Materials
- **Multiple Output Formats**: JSON, SARIF, Table, Text, XML for CI/CD integration
- **Configurable Scanning**: Granular control over scan depth and timeout settings
- **Finding Deduplication**: Intelligent tracking to prevent duplicate alerts
- **Parallel Processing**: Multi-threaded scanning with configurable worker pools
- **Low False Positives**: Advanced heuristics minimize alert fatigue

## Quick Start

### Basic Usage

```bash
# Scan current directory
docker run --rm -v $(pwd):/scan:ro layerd/hex:latest /scan

# Scan specific model file
docker run --rm -v $(pwd):/scan:ro layerd/hex:latest /scan/model.safetensors

# Generate JSON report
docker run --rm -v $(pwd):/scan:ro layerd/hex:latest /scan --json > report.json
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

# Generate SBOM for compliance
docker run --rm \
  -v $(pwd):/scan:ro \
  -v $(pwd)/output:/output \
  layerd/hex:latest /scan --sbom /output/sbom.json

# CI/CD Integration with timeout
docker run --rm \
  -v $(pwd):/scan:ro \
  -e HEX_TIMEOUT=600 \
  layerd/hex:latest /scan --format json --output /scan/results.json
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
| `--sbom` | Generate SBOM file | - |
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
# Scan multiple directories
for dir in model1 model2 model3; do
  docker run --rm -v $(pwd)/$dir:/scan:ro \
    layerd/hex:latest /scan \
    --json > results-$dir.json
done
```

## Output Examples

### JSON Output Structure

```json
{
  "scan_id": "550e8400-e29b-41d4-a716-446655440000",
  "timestamp": "2024-01-15T10:30:00Z",
  "target": "/scan",
  "version": "1.0.0",
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
  ],
  "summary": {
    "total_issues": 15,
    "critical": 2,
    "high": 5,
    "medium": 6,
    "low": 2,
    "security_score": 72
  }
}
```

## Performance Benchmarks

| Model Size | Files | Scan Time | Memory Usage |
|------------|-------|-----------|--------------|
| < 100 MB | 10 | ~5 seconds | < 50 MB |
| 100 MB - 1 GB | 50 | ~30 seconds | < 100 MB |
| 1 GB - 10 GB | 100 | ~2 minutes | < 200 MB |
| > 10 GB | 500+ | ~10 minutes | < 500 MB |

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
- Full Documentation: https://www.layerd.com/docs/hex
- API Reference: https://www.layerd.com/docs/hex/api
- Best Practices: https://www.layerd.com/docs/hex/best-practices

### Support Channels
- Enterprise Support: support@layerd.com
- GitHub Issues: https://github.com/Layerd-AI/layerd-hex/issues
- Community Forum: https://community.layerd.com

### License
- Open Source: MIT License
- Enterprise: Contact sales@layerd.com for commercial licensing

## About Layerd AI

Layerd AI is a leader in AI/ML security, providing enterprise-grade solutions for securing the AI supply chain. Our mission is to enable organizations to deploy AI safely and confidently.

---

Copyright 2026 Layerd AI. All rights reserved.
