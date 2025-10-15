# Security Policy

## 🔒 Reporting Security Issues

If you discover a security vulnerability in this repository, please **do not** use the public issue tracker. Instead:

1. Create a private security advisory on GitHub (Security tab → Advisories → New draft)
2. Or contact the repository owner directly

Security reports will be acknowledged within 48 hours.

## 🛡️ Security Best Practices

### API Key Safety

**⚠️ CRITICAL: Never commit API keys to this repository**

- ✅ **Always use environment variables** for credentials
- ✅ **Clear notebook outputs** before committing: `Cell → All Output → Clear`
- ✅ **Review notebooks** for hardcoded secrets before pushing
- ✅ **Add `.env` files to `.gitignore`** (already configured)

### Before Committing

Run this checklist before every commit:

```bash
# 1. Clear all notebook outputs
jupyter nbconvert --clear-output --inplace *.ipynb

# 2. Search for potential secrets (should return nothing)
grep -r "sk-" *.ipynb
grep -r "api_key.*=" *.ipynb | grep -v "os.getenv"

# 3. Check for environment variable files
ls -la | grep .env
```

### Recommended Environment Setup

```bash
# Set environment variables in your shell config (~/.zshrc, ~/.bashrc)
export PANW_AI_SEC_API_KEY="your-key"
export PRISMA_AIRS_PROFILE="your-profile"
export OPENAI_API_KEY="your-key"

# Or use a .env file (which is in .gitignore)
echo 'PANW_AI_SEC_API_KEY=your-key' > .env
echo 'PRISMA_AIRS_PROFILE=your-profile' >> .env
echo 'OPENAI_API_KEY=your-key' >> .env
```

## 📦 Dependency Security

### Keeping Dependencies Updated

```bash
# Check for outdated packages
pip list --outdated

# Update all dependencies
pip install --upgrade -r requirements.txt
```

### Dependency Vulnerability Scanning

This repository uses:
- **Dependabot** - Automatically creates PRs for dependency updates
- **GitHub Security Advisories** - Alerts for known vulnerabilities

To manually check for vulnerabilities:
```bash
pip install safety
safety check -r requirements.txt
```

## 🚨 Known Risks & Mitigations

### Risk: Notebook Output May Contain Sensitive Data

**Mitigation:**
- Always clear outputs before sharing: `Cell → All Output → Clear`
- Review API responses for PII or sensitive information
- The `.gitignore` is configured to ignore notebook checkpoints

### Risk: Test Prompts May Trigger API Rate Limits

**Mitigation:**
- Use the synchronous notebook for individual tests
- Add delays between batch requests in the asynch notebook
- Monitor your Prisma AIRS API usage dashboard

### Risk: Hardcoded Test Data in Notebooks

**Mitigation:**
- Example prompts use fake/sanitized data only
- Do not use real PII, credentials, or production data in tests
- Replace example data before sharing notebooks

## 📋 Supported Versions

This is a testing repository. Security updates apply to:

| Version | Supported          |
| ------- | ------------------ |
| Latest commit (main) | ✅ Supported |
| Older commits | ❌ Not supported - please update |

## 🔍 Security Features in Notebooks

The notebooks include built-in security practices:

- ✅ Environment variable usage by default
- ✅ No hardcoded credentials in shared versions
- ✅ Clear documentation on credential management
- ✅ Error handling for API failures
- ✅ Timeout configurations to prevent hanging requests

## 📚 Additional Resources

- [Prisma AIRS Security Best Practices](https://pan.dev/prisma-airs/)
- [Jupyter Security Best Practices](https://jupyter-notebook.readthedocs.io/en/stable/security.html)
- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)

## ✅ Security Checklist for Contributors

Before submitting any changes:

- [ ] No API keys or secrets in code
- [ ] All notebook outputs cleared
- [ ] Environment variables used for credentials
- [ ] `.gitignore` includes all sensitive file patterns
- [ ] No real PII or production data in examples
- [ ] Dependencies are up to date
- [ ] Code follows security best practices

---

**Last Updated:** October 2025
