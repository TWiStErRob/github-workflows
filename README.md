# github-workflows
Reusable GitHub Actions workflows for my repositories.

## [validate.yml](.github/workflows/validate.yml)
Gradle wrapper validation.

```yaml
jobs:
  validate:
    name: "🦺 Validation"
    uses: TWiStErRob/github-workflows/.github/workflows/validate.yml@v1
```

## [instrumentation.yml](.github/workflows/instrumentation.yml)
Run Android instrumentation tests on an emulator and upload artifacts.

```yaml
jobs:
  instrumentation:
    name: "🧪 Instrumentation Tests on" # / API ${{ matrix.api }} will be appended by used workflow.
    needs: validate
    uses: ./.github/workflows/instrumentation.yml
```

```yaml
name: "🧪 Instrumentation Test Matrix"

on:
  workflow_call

jobs:
  instrumentation:
    name: "${{ matrix.api }}"

    uses: TWiStErRob/github-workflows/.github/workflows/instrumentation.yml@v1
    with:
      android-api: ${{ matrix.api }}
      script: >
        ./gradlew
        --no-daemon
        --continue
        --stacktrace
        :app:connectedCheck

    strategy:
      fail-fast: false
      matrix:
        # The API level, see https://apilevels.com/.
        api:
          - 29
          - 33
```

## Related docs
 * https://docs.github.com/en/actions/using-workflows/reusing-workflows
