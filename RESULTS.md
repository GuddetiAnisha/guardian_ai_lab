# Guardian AI Lab — Final Validation Results

## Validation status

The project was validated locally after resolving the telemetry dataset path and test-client dependency issues.

Final local test result:

```text
12 passed, 1 warning
```

The remaining warning is a FastAPI/Starlette deprecation warning related to `TestClient`/`httpx`. It does not represent a failed test or broken application behavior.

## Issues found and resolved

### 1. Telemetry dataset path

The backend and tests expected the LTE telemetry sample at:

```text
data/sample/lte_trace.csv
```

The local project initially stored the dataset elsewhere, which caused telemetry-based tests to fail with `StopIteration` because no usable records were found at the expected path.

The dataset was placed in the expected directory and the telemetry tests were rerun successfully.

### 2. Missing test-client dependency

Initial API test collection failed with:

```text
RuntimeError: The starlette.testclient module requires the httpx package to be installed.
```

Installing `httpx` in the active virtual environment resolved the test collection issue.

## Verified test coverage

The passing suite validates the bundled project behaviors, including:

- FastAPI endpoint behavior
- JWT signing and tamper detection
- role-based access control
- least-privilege workflow behavior
- analyst approval/authorization restrictions
- prompt-injection blocking
- agent investigation workflow
- gated action creation
- telemetry loading
- anomaly-detection logic
- reproducible evaluation behavior

## Final result

```text
12/12 tests passed
```

This confirms that the bundled implementation and test suite execute successfully in the validated local environment.

## Reproduce locally

From the project root:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r .\backend\requirements.txt
pip install httpx
python -m pytest -q
```

Expected result:

```text
12 passed, 1 warning
```

## Scope and limitations

These results validate the software behavior covered by the repository's bundled tests. They do not constitute production-security certification, comprehensive prompt-injection robustness, or real-world telecom performance validation.
