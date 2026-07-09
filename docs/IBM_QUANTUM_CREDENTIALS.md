# IBM Quantum credentials guide

This notebook can collect live IBM/Qiskit Runtime metadata. To do that, it needs IBM Quantum credentials provided locally by the user running the notebook.

You must provide two environment variables:

```bash
IBM_QUANTUM_TOKEN=your_ibm_cloud_api_key_here
IBM_QUANTUM_INSTANCE=your_ibm_quantum_runtime_crn_here
```

Do not commit these values to GitHub or GitLab.

---

## What these values mean

### `IBM_QUANTUM_TOKEN`

This is your IBM Cloud API key. Qiskit Runtime uses it to authenticate your account when connecting to IBM Quantum services.

### `IBM_QUANTUM_INSTANCE`

This is the Cloud Resource Name (CRN) of the IBM Quantum Runtime service instance that your account can access.

In Qiskit Runtime, this value is passed as the `instance` argument.

---

## How to obtain the IBM Quantum API key and Runtime instance CRN

### 1. Create or access an IBM Cloud account

Create or access your IBM Cloud account using the IBM Cloud website.

You may also receive access through an organization, university, research group, or enterprise account.

### 2. Open IBM Quantum Platform

Open IBM Quantum Platform in your browser and log in.

Make sure the correct IBM Cloud account and region are selected in the platform header.

### 3. Create or select an IBM Quantum service instance

Open the **Instances** area of IBM Quantum Platform.

Create a new IBM Quantum service instance or select an existing instance that you can access.

The instance identifies the IBM Quantum service context used by Qiskit Runtime.

### 4. Copy the Runtime instance CRN

From the selected instance page, copy the Cloud Resource Name (CRN).

This value should be saved locally as:

```bash
IBM_QUANTUM_INSTANCE=your_ibm_quantum_runtime_crn_here
```

### 5. Create or copy your IBM Cloud API key

From IBM Cloud, create or copy an API key associated with your account.

Save it locally as:

```bash
IBM_QUANTUM_TOKEN=your_ibm_cloud_api_key_here
```

### 6. Store the values locally

The recommended approach for this repository is to create a local `.env` file:

```bash
cp .env.example .env
```

Then edit `.env`:

```bash
IBM_QUANTUM_TOKEN=your_ibm_cloud_api_key_here
IBM_QUANTUM_INSTANCE=your_ibm_quantum_runtime_crn_here
```

The `.env` file is ignored by Git and must not be committed.

---

## Alternative: export credentials in the terminal

Linux/macOS:

```bash
export IBM_QUANTUM_TOKEN="your_ibm_cloud_api_key_here"
export IBM_QUANTUM_INSTANCE="your_ibm_quantum_runtime_crn_here"
```

Windows PowerShell:

```powershell
$env:IBM_QUANTUM_TOKEN="your_ibm_cloud_api_key_here"
$env:IBM_QUANTUM_INSTANCE="your_ibm_quantum_runtime_crn_here"
```

---

## Optional: initialize Qiskit Runtime directly

The notebook uses environment variables, but the equivalent Qiskit Runtime initialization is:

```python
from qiskit_ibm_runtime import QiskitRuntimeService

service = QiskitRuntimeService(
    channel="ibm_quantum_platform",
    token="API_KEY",
    instance="CRN",
)
```

You can also save the account locally in a trusted personal environment:

```python
from qiskit_ibm_runtime import QiskitRuntimeService

QiskitRuntimeService.save_account(
    channel="ibm_quantum_platform",
    token="API_KEY",
    instance="CRN",
    set_as_default=True,
)
```

Do this only on a trusted personal machine. Do not save credentials on shared machines, public notebooks, CI runners, or cloud environments that you do not control.

---

## Quick validation

After setting the environment variables, test the connection with:

```python
import os
from qiskit_ibm_runtime import QiskitRuntimeService

service = QiskitRuntimeService(
    channel="ibm_quantum_platform",
    token=os.environ["IBM_QUANTUM_TOKEN"],
    instance=os.environ["IBM_QUANTUM_INSTANCE"],
)

backends = service.backends(simulator=False, operational=True)
print(f"Operational real backends available: {len(backends)}")
for backend in backends[:5]:
    print(backend.name)
```

If this fails, check:

- the API key is correct;
- the Runtime instance CRN is correct;
- your IBM Cloud account has access to the selected instance;
- the correct region/account is selected;
- `qiskit-ibm-runtime` is installed and up to date;
- your network/firewall allows access to IBM Quantum API endpoints.

---

## Security checklist

Before pushing to GitHub or GitLab, run:

```bash
git status
```

Make sure the following files are not staged:

```text
.env
qiskit-ibm.json
qiskitrc
external_qpu_cache/
credentials/
secrets/
```

You can also search for accidental credentials:

```bash
grep -R "IBM_QUANTUM_TOKEN\|IBM_QUANTUM_INSTANCE\|apikey\|api_key\|CRN" . --exclude-dir=.git
```

This command may find documentation examples. That is expected. It must not find your real key or real private credential values.
