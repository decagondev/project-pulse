# ProjectPulse Tasks

This document outlines the development tasks for ProjectPulse, structured into **Epics**, **Pull Requests (PRs)**, and **Commits**. This breakdown ensures the project is manageable, allowing a developer or an LLM to tackle work in granular, incremental steps. Each commit represents a small, atomic change that can be implemented, tested, and reviewed independently.

The structure is based on the PRD, user stories, features, system components, code snippets, and implementation plan. Epics align with the high-level phases from the original plan, expanded for completeness (e.g., adding setup, integration, and testing). PRs group related sub-tasks within an Epic, and commits detail specific code changes or actions.

Assumptions:
- Development uses Git for version control.
- Each PR targets a feature branch from `main` (e.g., `feature/data-import`).
- Commits follow conventional commit messages (e.g., `feat: add CSV parser`).
- Total timeline: ~1 week, as per the plan, with testing/debugging integrated.
- Dependencies: Java 17+, H2 DB, JavaFX; use Gradle for build management (assume Gradle for specificity).
- Testing: Include unit/integration tests in relevant commits using JUnit.
- Code style: Follow Java conventions; use provided code snippets as starting points.

## Epic 1: Project Setup and Infrastructure
**Description**: Establish the foundational project structure, dependencies, and database setup. This ensures a clean starting point before feature development.
**Estimated Time**: 0.5 days
**Dependencies**: None

### PR 1.1: Initialize Project Repository and Build System
**Branch**: `feature/project-setup`
**Description**: Set up the Gradle project, add dependencies, and configure basic structure.

- **Commit 1**: `chore: initialize Gradle project with Java 17 configuration`  
  Create `build.gradle` with Java 17, add group/version for ProjectPulse.

- **Commit 2**: `feat: add dependencies for H2 DB, JavaFX, and parsing libraries`  
  Add H2 (`com.h2database:h2`), JavaFX (`org.openjfx:javafx-controls`, etc.), Jackson for JSON (`com.fasterxml.jackson.core:jackson-databind`), OpenCSV for CSV (`com.opencsv:opencsv`).

- **Commit 3**: `chore: create basic directory structure`  
  Set up `src/main/java/com/projectpulse/` with packages for models, components, ui, etc.; add `src/test/java` for tests.

- **Commit 4**: `test: add initial JUnit setup and smoke test`  
  Add JUnit dependency; write a simple test to verify build (use JUnit Platform).

### PR 1.2: Set Up H2 Database Integration
**Branch**: `feature/database-setup`
**Description**: Configure embedded H2 DB for data storage.

- **Commit 1**: `feat: create DatabaseManager class for H2 connection`  
  Implement singleton for JDBC connection to H2 (file-based mode).

- **Commit 2**: `feat: define schema for tasks table`  
  Create SQL schema for tasks (columns: id, name, duration, start_date, end_date, dependencies as JSON string).

- **Commit 3**: `feat: add methods to initialize DB and insert sample data`  
  Add init() method to create tables if not exists.

- **Commit 4**: `test: add unit tests for DB connection and schema creation`  
  Test connection, table existence, and basic CRUD.

## Epic 2: Data Import
**Description**: Implement functionality to import project data from CSV/JSON files into the H2 DB. Aligns with User Story: "As a project manager, I want to import project data from CSV/JSON so that I can visualize my project's timeline."
**Estimated Time**: 1 day
**Dependencies**: Epic 1

### PR 2.1: Implement CSV Import
**Branch**: `feature/csv-import`
**Description**: Parse CSV files and load data into DB.

- **Commit 1**: `feat: create DataImportComponent class`  
  Skeleton class with importFromCSV method.

- **Commit 2**: `feat: implement CSV parsing using OpenCSV`  
  Read file, map columns to Task model (define Task class with fields: id, name, duration, dependencies as List<String>).

- **Commit 3**: `feat: validate and insert parsed data into H2 DB`  
  Use DatabaseManager to batch insert tasks.

- **Commit 4**: `test: add unit tests for CSV parsing and import`  
  Test with sample CSV; handle edge cases like missing fields.

### PR 2.2: Implement JSON Import
**Branch**: `feature/json-import`
**Description**: Parse JSON files and load data into DB.

- **Commit 1**: `feat: add importFromJSON method to DataImportComponent`  
  Use Jackson to deserialize JSON array into List<Task>.

- **Commit 2**: `feat: handle nested dependencies in JSON`  
  Ensure dependencies are parsed as arrays.

- **Commit 3**: `feat: integrate with DB insertion`  
  Reuse validation and insert logic from CSV.

- **Commit 4**: `test: add unit tests for JSON parsing and import`  
  Test with sample JSON; handle malformed input.

### PR 2.3: UI for Data Import
**Branch**: `feature/import-ui`
**Description**: Add basic JavaFX UI elements for file selection.

- **Commit 1**: `feat: create ImportUI class with file chooser`  
  Use FileChooser for CSV/JSON selection.

- **Commit 2**: `feat: trigger import on file select and show success/error dialog`  
  Call DataImportComponent methods.

- **Commit 3**: `test: add integration tests for import flow`  
  Mock file input and verify DB population.

## Epic 3: Dependency Analysis
**Description**: Analyze task dependencies and build a graph. Aligns with User Story: "As a project manager, I want to visualize my project's timeline and dependencies so that I can identify potential bottlenecks."
**Estimated Time**: 1 day
**Dependencies**: Epic 2

### PR 3.1: Define Models and Graph Structure
**Branch**: `feature/dependency-models`
**Description**: Create core models for tasks and graphs.

- **Commit 1**: `feat: refine Task model with getters/setters`  
  Ensure serializable for DB.

- **Commit 2**: `feat: create DependencyGraph class`  
  Use adjacency list (Map<String, List<String>>) for nodes/edges.

- **Commit 3**: `feat: add methods for addNode, addEdge, getDegree`  
  Basic graph operations.

- **Commit 4**: `test: unit tests for graph construction and queries`

### PR 3.2: Implement Dependency Analyzer
**Branch**: `feature/dependency-analyzer`
**Description**: Build graph from DB data.

- **Commit 1**: `feat: create DependencyAnalyzer class`  
  Use provided code snippet as base.

- **Commit 2**: `feat: fetch tasks from DB and build graph`  
  Query H2 for tasks, populate graph.

- **Commit 3**: `feat: handle cyclic dependency detection`  
  Add simple cycle check (optional but good for robustness).

- **Commit 4**: `test: unit tests for analyze method with sample data`

## Epic 4: Visualization
**Description**: Implement JavaFX UI for timeline and dependency visualization. Aligns with User Story: "As a project manager, I want to visualize my project's timeline and dependencies..."
**Estimated Time**: 2 days
**Dependencies**: Epic 3

### PR 4.1: Set Up JavaFX Application
**Branch**: `feature/javafx-setup`
**Description**: Bootstrap the main app UI.

- **Commit 1**: `feat: create MainApp class extending Application`  
  Set up stage, scene.

- **Commit 2**: `feat: add menu bar with import option`  
  Link to ImportUI.

- **Commit 3**: `test: add launch test for app`

### PR 4.2: Implement Timeline Visualization
**Branch**: `feature/timeline-vis`
**Description**: Render Gantt-like chart.

- **Commit 1**: `feat: create VisualizationComponent class`  
  Skeleton with renderTimeline method.

- **Commit 2**: `feat: use JavaFX Canvas or Chart for Gantt representation`  
  Plot tasks by start/end dates.

- **Commit 3**: `feat: add dependency lines between tasks`  
  Draw arrows based on graph.

- **Commit 4**: `feat: add interactivity (zoom, highlight)`  
  Event handlers for user interaction.

- **Commit 5**: `test: unit/integration tests for rendering`

### PR 4.3: Integrate Visualization into UI
**Branch**: `feature/vis-integration`
**Description**: Embed visualization in main app.

- **Commit 1**: `feat: add visualize button post-import`  
  Trigger analysis and render.

- **Commit 2**: `feat: handle refresh on data changes`  
  Observer pattern for updates.

- **Commit 3**: `test: end-to-end test for import-to-vis flow`

## Epic 5: Bottleneck Detection
**Description**: Identify bottlenecks using graph analysis. Aligns with User Story: "As a project manager, I want the application to suggest optimization strategies..."
**Estimated Time**: 1 day
**Dependencies**: Epic 4

### PR 5.1: Implement Bottleneck Detector
**Branch**: `feature/bottleneck-detector`
**Description**: Algorithm for detection.

- **Commit 1**: `feat: create BottleneckDetector class`  
  Use provided code snippet; define threshold (e.g., configurable).

- **Commit 2**: `feat: enhance with critical path analysis`  
  Use topological sort to find longest paths.

- **Commit 3**: `feat: integrate with graph from analyzer`  
  Detect and return list of bottleneck tasks.

- **Commit 4**: `test: unit tests for detection on sample graphs`

### PR 5.2: UI for Bottleneck Display
**Branch**: `feature/bottleneck-ui`
**Description**: Highlight bottlenecks in visualization.

- **Commit 1**: `feat: add highlight method in VisualizationComponent`  
  Color-code bottlenecks.

- **Commit 2**: `feat: add button to trigger detection`  
  Show list in dialog or pane.

- **Commit 3**: `test: integration tests for detection UI`

## Epic 6: Optimization Suggestions
**Description**: Provide strategies based on bottlenecks. Aligns with User Story: "As a project manager, I want the application to suggest optimization strategies..."
**Estimated Time**: 1 day
**Dependencies**: Epic 5

### PR 6.1: Implement Optimization Logic
**Branch**: `feature/optimization-logic`
**Description**: Heuristics for suggestions.

- **Commit 1**: `feat: create OptimizationSuggestionsComponent class`  
  Method to generate suggestions from bottlenecks.

- **Commit 2**: `feat: add basic rules (e.g., parallelize high-degree tasks)`  
  Generate strings like "Reallocate resources to Task X".

- **Commit 3**: `feat: make suggestions configurable/extensible`  
  Use rule-based system.

- **Commit 4**: `test: unit tests for suggestion generation`

### PR 6.2: UI for Suggestions
**Branch**: `feature/optimization-ui`
**Description**: Display suggestions.

- **Commit 1**: `feat: add suggestions pane in UI`  
  List view with actionable items.

- **Commit 2**: `feat: link to detection trigger`  
  Auto-show after detection.

- **Commit 3**: `test: integration tests for full flow`

## Epic 7: Testing, Debugging, and Polish
**Description**: Comprehensive testing, debugging, and final integrations. Ensures acceptance criteria are met.
**Estimated Time**: 2 days
**Dependencies**: All previous Epics

### PR 7.1: Unit and Integration Testing
**Branch**: `feature/full-testing`
**Description**: Cover all components.

- **Commit 1**: `test: add tests for end-to-end import-to-optimization`  
  Use sample data files.

- **Commit 2**: `test: coverage for edge cases (e.g., empty data, cycles)`  
  Aim for 80%+ coverage.

- **Commit 3**: `fix: address any bugs from tests`

### PR 7.2: Debugging and Performance
**Branch**: `feature/debug-polish`
**Description**: Optimize and fix issues.

- **Commit 1**: `perf: optimize graph building for large datasets`  
  Profile and improve.

- **Commit 2**: `fix: handle UI threading issues in JavaFX`  
  Use Platform.runLater where needed.

- **Commit 3**: `chore: add logging with SLF4J`  
  For debugging.

- **Commit 4**: `docs: update README with build/run instructions`

### PR 7.3: Final Integration and Release Prep
**Branch**: `feature/final-integration`
**Description**: Merge everything and prepare for release.

- **Commit 1**: `feat: integrate all components into MainApp`  
  Full flow: import -> analyze -> visualize -> detect -> suggest.

- **Commit 2**: `test: system tests against acceptance criteria`  
  Verify visualization accuracy, etc.

- **Commit 3**: `chore: create executable JAR`  
  Configure Gradle Shadow plugin to produce a fat JAR in `build/libs/*-all.jar`.

- **Commit 4**: `docs: add user guide in docs folder`
