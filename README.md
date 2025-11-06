# iOS Static Analysis & Xcode Build Automation Toolkit

![Xcode](https://img.shields.io/badge/Xcode-15.0+-blue.svg)
![Platform](https://img.shields.io/badge/platform-iOS%20%7C%20macOS%20%7C%20watchOS%20%7C%20tvOS-lightgrey.svg)
![CI](https://img.shields.io/badge/CI-GitHub%20Actions%20%7C%20Jenkins%20%7C%20GitLab%20CI-orange.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

A comprehensive automation toolkit for Xcode projects featuring static analysis, build automation, CI/CD integration, and code quality enforcement. This guide provides production-ready scripts and workflows for iOS/macOS development teams.

## 🌟 Features

### 🛠️ Core Capabilities
- **Advanced Static Analysis** - Deep Clang analyzer integration with customizable rules
- **Multi-Platform Support** - iOS, macOS, watchOS, tvOS compatibility
- **CI/CD Ready** - Pre-configured workflows for major CI platforms
- **Quality Gates** - Automated code quality enforcement
- **Performance Monitoring** - Build time optimization and caching
- **Security Scanning** - Vulnerability detection and reporting

### 📊 Analysis Types
- Memory leak detection
- Logic error identification
- API misuse detection
- Security vulnerability scanning
- Code style enforcement
- Performance issue detection

## 🚀 Quick Start

### Prerequisites

```bash
# Required
- Xcode 15.0+
- macOS 13.0+
- Bash 4.0+

# Optional but recommended
- CocoaPods 1.12.0+
- Swift Package Manager
- Fastlane 2.210+
```

### 5-Minute Setup

```bash
# 1. Clone the repository
git clone https://github.com/your-org/ios-build-automation.git
cd ios-build-automation

# 2. Run automated setup
./setup.sh --project-path /path/to/your/project

# 3. Verify installation
./scripts/verify-environment.sh

# 4. Run first analysis
./scripts/quick-analysis.sh
```

### One-Command Project Integration

```bash
# Integrate with existing Xcode project
./scripts/integrate-project.sh \
  --workspace MyApp.xcworkspace \
  --scheme MyApp \
  --team-id YOUR_TEAM_ID \
  --output-dir ./build-automation
```

## 📦 Installation

### Method 1: Automated Setup (Recommended)

```bash
curl -sSL https://raw.githubusercontent.com/your-org/ios-build-automation/main/remote-setup.sh | bash -s -- \
  --workspace MyApp.xcworkspace \
  --scheme MyApp \
  --ci-platform github
```

### Method 2: Manual Installation

```bash
# 1. Download the toolkit
git clone https://github.com/your-org/ios-build-automation.git
cd ios-build-automation

# 2. Install dependencies
./scripts/install-dependencies.sh

# 3. Configure for your project
./scripts/configure-project.sh

# 4. Set up Git hooks
./scripts/setup-git-hooks.sh
```

## 🛠️ Basic Usage

### Local Development Workflow

```bash
# 1. Daily development check
./scripts/daily-check.sh

# 2. Pre-commit analysis (automatically runs on git commit)
git add .
git commit -m "Your message"  # Triggers auto-analysis

# 3. Manual deep analysis
./scripts/deep-analysis.sh --level thorough

# 4. Generate reports
./scripts/generate-reports.sh --format html,pdf,json
```

### Common Analysis Commands

| Command | Purpose | Usage Example |
|---------|---------|---------------|
| **Quick Analysis** | Fast safety check | `./scripts/quick-analysis.sh` |
| **Deep Analysis** | Comprehensive check | `./scripts/deep-analysis.sh --level thorough` |
| **Security Scan** | Vulnerability focus | `./scripts/security-scan.sh` |
| **Performance Check** | Performance issues | `./scripts/performance-analysis.sh` |
| **Memory Analysis** | Memory leak detection | `./scripts/memory-analysis.sh` |

## ⚙️ Advanced Configuration

### Configuration Files

#### 1. Main Configuration (`.build-automation/config.json`)

```json
{
  "project": {
    "workspace": "MyApp.xcworkspace",
    "schemes": ["MyApp", "MyAppTests", "MyAppUITests"],
    "configurations": ["Debug", "Release", "Staging"]
  },
  "analysis": {
    "enabled": true,
    "level": "thorough",
    "max_issues": 10,
    "fail_on_warnings": true,
    "output_formats": ["html", "json", "plist"]
  },
  "ci": {
    "platform": "github-actions",
    "cache_enabled": true,
    "parallel_analysis": true
  }
}
```

### Custom Analysis Rules

#### 1. Security-Focused Analysis

```bash
#!/bin/bash
# security-analysis.sh

export CLANG_ANALYZER_SECURITY_INSECUREAPI=YES
export CLANG_ANALYZER_SECURITY_KEYCHAIN=YES
export CLANG_ANALYZER_SECURITY_FLOATLOOPCOUNTER=YES

./scripts/run-analysis.sh \
  --rule-set security \
  --fail-on warning \
  --output-format sarif
```

## 🔄 CI/CD Integration

### GitHub Actions

```yaml
# .github/workflows/ios-analysis.yml
name: iOS Static Analysis

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  static-analysis:
    name: Static Analysis
    runs-on: macos-latest
    
    steps:
    - name: Checkout
      uses: actions/checkout@v4
      
    - name: Run Analysis
      run: |
        ./scripts/ci-analysis.sh \
          --scheme MyApp \
          --output-dir ./results \
          --upload-artifacts
          
    - name: Quality Gate
      run: ./scripts/quality-gate.sh --threshold 5
```

### Jenkins Pipeline

```groovy
// Jenkinsfile
pipeline {
    agent { label 'macos' }
    
    stages {
        stage('Static Analysis') {
            steps {
                sh './scripts/ci-analysis.sh --jenkins'
            }
        }
    }
}
```

## 🐛 Troubleshooting

### Common Issues & Solutions

```bash
# Problem: Scheme not found
./scripts/troubleshoot.sh --issue scheme-not-found --workspace MyApp.xcworkspace

# Problem: Code signing issues  
./scripts/troubleshoot.sh --issue code-signing --team-id YOUR_TEAM_ID

# Problem: Memory issues during analysis
./scripts/troubleshoot.sh --issue memory --increase-memory-limit
```

### Debug Mode

Enable detailed debugging:

```bash
# Full debug output
./scripts/run-analysis.sh --debug --verbose --log-level debug

# Generate debug report
./scripts/generate-debug-report.sh --include-system-info --include-logs
```

## 📊 Best Practices

### 1. Code Quality Enforcement

#### Pre-commit Hooks

```bash
#!/bin/bash
# .git/hooks/pre-commit

# Run quick analysis before commit
if ! ./scripts/quick-analysis.sh --staged-only; then
    echo "❌ Quick analysis failed. Please fix issues before committing."
    exit 1
fi
```

#### Quality Gates Configuration

```bash
#!/bin/bash
# quality-gate-config.sh

# Define quality thresholds
export MAX_CRITICAL_ISSUES=0
export MAX_HIGH_ISSUES=2  
export MAX_MEDIUM_ISSUES=5
export MAX_LOW_ISSUES=10

# Run quality gate
./scripts/quality-gate.sh \
  --critical $MAX_CRITICAL_ISSUES \
  --high $MAX_HIGH_ISSUES \
  --medium $MAX_MEDIUM_ISSUES \
  --low $MAX_LOW_ISSUES
```

### 2. Team Collaboration

#### Shared Configuration

```bash
# Team configuration setup
./scripts/setup-team-config.sh \
  --team-name "iOS Team" \
  --quality-standards "high" \
  --report-frequency "daily"
```

## 🤝 Contributing

We welcome contributions from the community! Here's how to get involved:

### Development Setup

```bash
# 1. Fork and clone
git clone https://github.com/your-username/ios-build-automation.git
cd ios-build-automation

# 2. Set up development environment
./scripts/setup-development.sh

# 3. Run tests
./scripts/run-tests.sh --all
```

### Contribution Guidelines

1. **Feature Requests**: Use GitHub Issues with the `enhancement` label
2. **Bug Reports**: Include reproducible test cases
3. **Code Contributions**: Follow our coding standards

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Resources

### Documentation
- [**Full Documentation**](docs/README.md)
- [**Configuration Guide**](docs/CONFIGURATION.md)
- [**Troubleshooting Guide**](docs/TROUBLESHOOTING.md)

### Community
- [**GitHub Discussions**](https://github.com/your-org/ios-build-automation/discussions)
- [**Stack Overflow**](https://stackoverflow.com/questions/tagged/ios-build-automation)

## 🆘 Support

### Getting Help

- **Documentation**: Check our [comprehensive docs](docs/)
- **Issues**: [GitHub Issues](https://github.com/your-org/ios-build-automation/issues)
- **Discussions**: [GitHub Discussions](https://github.com/your-org/ios-build-automation/discussions)

---

<div align="center">

## 🚀 Ready to Get Started?

[**Quick Start Guide**](docs/QUICK_START.md) • 
[**Configuration Options**](docs/CONFIGURATION.md) • 
[**Examples Gallery**](docs/EXAMPLES.md)

**Made with ❤️ for the iOS Developer Community**

[⬆ Back to Top](#ios-static-analysis--xcode-build-automation-toolkit)

</div>
