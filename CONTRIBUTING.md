# Contributing to ProjectPulse

Thank you for your interest in contributing to ProjectPulse! We welcome contributions from the community to help improve this Java-based desktop application for project management visualization. Whether you're fixing bugs, adding features, improving documentation, or reporting issues, your help is appreciated.

By contributing, you agree to abide by the project's [Code of Conduct](#code-of-conduct) (if one is added in the future; currently, we expect respectful and collaborative behavior).

## Getting Started

### Prerequisites
- Java 17 or higher (JDK for development)
- Maven 3.6 or higher
- Git for version control
- Familiarity with Java, JavaFX, H2 Database, and related libraries (see `pom.xml` for dependencies)

### Installation
1. Fork the repository on GitHub.
2. Clone your fork:
   ```
   git clone https://github.com/YOUR_USERNAME/project-pulse.git
   cd project-pulse
   ```
3. Build the project:
   ```
   mvn clean install
   ```
   This compiles the code, runs tests, and generates the executable JAR in `target/`.

4. Run the application:
   ```
   java -jar target/projectpulse-1.0-SNAPSHOT.jar
   ```
   Or for development:
   ```
   mvn exec:java -Dexec.mainClass="com.projectpulse.MainApp"
   ```

For more details, refer to the [README.md](./README.md#setup-instructions).

## Development Workflow

### Branching Strategy
- Create a new branch from `main` for each feature, bug fix, or improvement.
- Use descriptive branch names, e.g., `feature/add-export-functionality` or `fix/database-connection-issue`.
- Follow the structure outlined in [docs/TASKS.md](./docs/TASKS.md), where features are broken into Epics, Pull Requests (PRs), and atomic commits.

### Commit Messages
- Use [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) for clarity, e.g.:
  - `feat: add JSON export functionality`
  - `fix: resolve null pointer in DatabaseManager`
  - `chore: update dependencies`
  - `test: add unit tests for import component`
- Keep commits small and atomic—each should represent a single, testable change.
- Reference related issues or epics if applicable, e.g., `feat: implement CSV import (closes #12)`.

### Coding Standards
- Follow standard Java conventions (e.g., camelCase for methods/variables, PascalCase for classes).
- Use 4-space indentation.
- Add Javadoc comments for public methods and classes.
- Handle exceptions gracefully and use SLF4J for logging.
- Ensure code is modular and aligns with the components described in [docs/PRD.md](./docs/PRD.md) (e.g., DataImportComponent, DependencyAnalyzer).
- Reference code examples in [docs/CODE-SNIPPETS.md](./docs/CODE-SNIPPETS.md) for style and implementation.

### Testing
- Write unit and integration tests using JUnit.
- Aim for high coverage (target: 80%+).
- Run tests before committing:
  ```
  mvn test
  ```
- Include tests for edge cases, such as empty data, invalid imports, or cyclic dependencies.
- Integration tests should cover flows like import-to-visualization.

## Pull Request Process
1. Ensure your branch is up-to-date with `main`:
   ```
   git checkout main
   git pull origin main
   git checkout your-branch
   git rebase main
   ```
2. Push your branch to your fork:
   ```
   git push origin your-branch
   ```
3. Open a Pull Request (PR) on the original repository:
   - Target the `main` branch.
   - Provide a clear title and description, referencing the epic/PR from [docs/TASKS.md](./docs/TASKS.md) if applicable.
   - Include screenshots for UI changes.
   - Link to any related issues.
4. Your PR will be reviewed by maintainers. Address feedback promptly.
5. Once approved, it will be merged. Thank you for your contribution!

PRs should group related commits (e.g., a feature branch with multiple commits under one PR). Follow the granular breakdown in [docs/TASKS.md](./docs/TASKS.md) for inspiration.

## Reporting Issues
- Check existing issues to avoid duplicates.
- Open a new issue with:
  - A descriptive title.
  - Steps to reproduce.
  - Expected vs. actual behavior.
  - Environment details (Java version, OS, etc.).
  - Screenshots or logs if relevant.
- Use labels like `bug`, `enhancement`, or `documentation` for categorization.

## Documentation
- Update [README.md](./README.md) for setup/user changes.
- Enhance docs in the `./docs` folder as needed (e.g., add to CODE-SNIPPETS.md for new code).
- Ensure all changes are documented in the PR description.

## License
By contributing, you agree that your contributions will be licensed under the [MIT License](./LICENSE). See the LICENSE file for details.

If you have questions, feel free to open an issue or reach out via GitHub discussions (if enabled). Happy contributing! 🚀
