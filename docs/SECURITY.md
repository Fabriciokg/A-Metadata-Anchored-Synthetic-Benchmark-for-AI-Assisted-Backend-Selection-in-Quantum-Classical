# Security policy and credential handling

This project may use IBM Quantum credentials to collect live Qiskit Runtime metadata.

Never publish real credentials.

---

## Do not commit

Do not commit any of the following:

```text
.env
*.key
*.pem
qiskit-ibm.json
qiskitrc
credentials/
secrets/
external_qpu_cache/
private execution logs
```

---

## Recommended credential handling

Use environment variables:

```bash
IBM_QUANTUM_TOKEN=your_ibm_cloud_api_key_here
IBM_QUANTUM_INSTANCE=your_ibm_quantum_runtime_crn_here
```

Or create a local `.env` file copied from `.env.example`:

```bash
cp .env.example .env
```

The `.env` file is ignored by Git.

---

## Before pushing to GitHub or GitLab

Run:

```bash
git status
```

Check that `.env` and other credential files are not staged.

Search for accidental secrets:

```bash
grep -R "IBM_QUANTUM_TOKEN\|IBM_QUANTUM_INSTANCE\|apikey\|api_key\|CRN" . --exclude-dir=.git
```

Documentation examples may appear. Real private values must not appear.

---

## If a secret is accidentally committed

If you accidentally commit an IBM API key:

1. Revoke or rotate the key immediately in IBM Cloud.
2. Remove the secret from the repository history.
3. Force-push only if you understand the consequences for collaborators.
4. Treat the exposed key as compromised.

Removing a secret from the latest commit is not enough if it remains in Git history.
