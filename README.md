# ProjectPulse

[![Java](https://img.shields.io/badge/Java-17+-orange.svg)](https://www.oracle.com/java/)
[![Maven](https://img.shields.io/badge/Maven-3.6+-blue.svg)](https://maven.apache.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## Introduction

ProjectPulse is an innovative Java Desktop application designed to visualize project timelines and dependencies, empowering project managers to identify potential bottlenecks and optimize resource allocation. Built with a focus on simplicity and efficiency, it leverages an embedded H2 database for data storage and JavaFX for a responsive user interface. This tool addresses key challenges in project management by automating dependency analysis, providing interactive visualizations, and offering actionable optimization suggestions—helping teams reduce delays, control costs, and boost productivity.

In today's fast-paced environments, like mid-sized tech firms, project managers often grapple with complex inter-task dependencies that spreadsheets and general-purpose tools can't adequately handle. ProjectPulse fills this gap by specializing in timeline visualization and proactive insights, making it easier to spot critical paths, communicate with stakeholders, and make data-driven decisions. Whether you're overseeing budgets up to $500K or timelines spanning months, ProjectPulse turns raw project data into clear, visual narratives that drive success.

Key highlights:
- **Target Users**: Project managers like Sarah Collins, who handle multiple cross-functional projects and need intuitive tools for dependency mapping and optimization.
- **Differentiation**: Unlike broad tools like Asana or MS Project, ProjectPulse emphasizes lightweight, offline desktop functionality with specialized features for bottleneck detection and suggestions.
- **Market Fit**: Positioned in the growing $15B+ project management software market, focusing on an underserved niche for visualization and analysis.

For detailed product requirements, development tasks, and code examples, refer to the [docs](./docs) folder.

## Features

- **Data Import**: Seamlessly import project data from CSV or JSON files, including task IDs, names, durations, dates, and dependencies.
- **Dependency Analysis**: Builds a graph of task dependencies to uncover relationships and potential cycles.
- **Timeline Visualization**: Interactive JavaFX-based Gantt-like charts and dependency diagrams for at-a-glance insights.
- **Bottleneck Detection**: Identifies high-impact tasks using algorithms like degree centrality and critical path analysis.
- **Optimization Suggestions**: Provides practical recommendations, such as resource reallocation or task parallelization, based on analysis.
- **Offline Capabilities**: Runs entirely on your desktop with embedded H2 database—no cloud dependencies or subscriptions required.

## Prerequisites

- Java 17 or higher (JDK recommended for development)
- Maven 3.6 or higher for build management
- Optional: Git for cloning the repository

## Setup Instructions

1. **Clone the Repository**:
   ```
   git clone https://github.com/decagondev/project-pulse.git
   cd project-pulse
   ```

2. **Build the Project**:
   Use Maven to resolve dependencies and build the executable JAR.
   ```
   mvn clean install
   ```
   This will compile the code, run tests, and package the application into `target/projectpulse-1.0-SNAPSHOT.jar` using the Maven Shade plugin.

3. **Run the Application**:
   Launch the app directly from the JAR:
   ```
   java -jar target/projectpulse-1.0-SNAPSHOT.jar
   ```
   Alternatively, for development:
   ```
   mvn exec:java -Dexec.mainClass="com.projectpulse.MainApp"
   ```

4. **Database Initialization**:
   The app uses an embedded H2 database stored in `./projectpulse.mv.db` (created automatically on first run). No external setup is needed.

5. **Verify Installation**:
   Upon launch, the main window should appear with options to import data and visualize timelines. If issues arise, check the console for logs (SLF4J is used for debugging).

For advanced configuration, refer to the `pom.xml` in the root directory, which includes dependencies for H2, JavaFX, Jackson (JSON), OpenCSV (CSV), and JUnit (testing).

## Usage

1. **Import Data**: Use the menu to select a CSV or JSON file containing project tasks. Sample formats are described in [docs/PRD.md](./docs/PRD.md).
2. **Visualize Timeline**: After import, click "Visualize" to render the Gantt chart and dependency graph.
3. **Detect Bottlenecks**: Trigger analysis to highlight potential issues.
4. **View Suggestions**: Review optimization recommendations in the suggestions pane.
5. **Interact**: Zoom, highlight tasks, or refresh views as needed.

For code examples and implementation details, see [docs/CODE-SNIPPETS.md](./docs/CODE-SNIPPETS.md). Development tasks are outlined in [docs/TASKS.md](./docs/TASKS.md).

## Contributing

Contributions are welcome! Please fork the repo, create a feature branch, and submit a pull request following the structure in [docs/TASKS.md](./docs/TASKS.md) (e.g., conventional commits). Run `mvn test` before submitting.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

Inspired by real-world project management challenges. Built with open-source tools like JavaFX and H2. For future roadmap ideas, check [docs/PRD.md](./docs/PRD.md).
