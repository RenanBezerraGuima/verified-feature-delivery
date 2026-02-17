# Stack Adapters

Prefer repository-defined scripts first (`Makefile`, `package.json`, task runners, CI commands).
Use this file when no clear local convention exists.

## Policy discovery order

1. Use repository CI/workflow gate definitions.
2. Use repository local config files and scripts.
3. Use defaults from `default-quality-thresholds.md` if policy is missing.

## Universal order

1. Run the narrowest tests for touched behavior.
2. Run full relevant test suite.
3. Run lint/type/static checks used by the repository.
4. Run coverage check or coverage report.
5. Run algorithmic quality checks configured for the repository.

## Typical commands by ecosystem

### JavaScript / TypeScript

- tests: `npm test` or `pnpm test` or `yarn test`
- targeted tests: framework-specific filters (`--watch`, `--runInBand`, path filters)
- coverage: `npm test -- --coverage` (or equivalent script)
- lint/types: `npm run lint`, `npm run typecheck`

### Python

- tests: `pytest`
- targeted tests: `pytest path/to/test_file.py -k "<pattern>"`
- coverage: `pytest --cov --cov-report=term-missing`
- lint/types: `ruff check .`, `mypy .` (if configured)

### Ruby

- tests: `bundle exec rspec`
- targeted tests: `bundle exec rspec path/to/spec.rb`
- coverage: use configured SimpleCov profile
- lint/types: `bundle exec rubocop` (and type tooling if configured)

### Java (Maven / Gradle)

- tests: `mvn test` or `./gradlew test`
- coverage: JaCoCo report/check (`mvn verify`, `./gradlew jacocoTestReport jacocoTestCoverageVerification`)
- static checks: run configured plugins/tasks in CI parity

### .NET

- tests: `dotnet test`
- coverage: `dotnet test --collect:\"XPlat Code Coverage\"` or repository coverlet config
- static checks: analyzers and formatting checks configured by solution

### Go

- tests: `go test ./...`
- targeted tests: `go test ./path/to/pkg -run <Regex>`
- coverage: `go test ./... -coverprofile=coverage.out` and `go tool cover -func=coverage.out`
- static checks: `go vet ./...` and repository linters

### Rust

- tests: `cargo test`
- targeted tests: `cargo test <pattern>`
- coverage: use repository coverage tooling (for example `cargo llvm-cov` if configured)
- lint: `cargo clippy --all-targets --all-features`

## Coverage policy guidance

- Honor existing repository thresholds over skill defaults.
- If no threshold exists, require non-decreasing coverage for touched modules and explicit tests for new logic.
- Prefer meaningful assertions over metric inflation.

## Algorithmic quality guidance

- Require no new high-severity findings from static analyzers on touched code.
- Require one additional non-coverage signal for critical touched logic: mutation score meets repository threshold, complexity budget does not regress, or property-based tests enforce invariants.
- Prefer repository CI thresholds when available.
- Select gate rigor based on `risk-based-gating-matrix.md`.

## Typical algorithmic checks by ecosystem

### JavaScript / TypeScript

- static: `npm run lint`, `npm run typecheck`, `npx semgrep --config auto` (if configured)
- mutation: `npx stryker run` (if configured)

### Python

- static: `ruff check .`, `mypy .`, `bandit -r .` (if configured)
- mutation: `mutmut run` (if configured)

### Ruby

- static: `bundle exec rubocop`, `bundle exec brakeman` (if configured)
- mutation: `bundle exec mutant run` (if configured)

### Java (Maven / Gradle)

- static: SpotBugs/PMD/Checkstyle tasks configured in the project
- mutation: PIT/PITest plugin task (`mvn test` with plugin profile or `./gradlew pitest`, if configured)

### .NET

- static: `dotnet build` with analyzers enabled, plus repository formatting checks
- mutation: `dotnet stryker` (if configured)

### Go

- static: `go vet ./...`, `staticcheck ./...`, or `golangci-lint run` (if configured)
- mutation: project mutation tooling if configured

### Rust

- static: `cargo clippy --all-targets --all-features`, `cargo audit` (if configured)
- mutation: `cargo mutants` (if configured)

## Legacy code guidance

- Add characterization tests before refactoring.
- Add seam points only where needed to isolate behavior.
- Keep refactors behavior-preserving and test-backed.
