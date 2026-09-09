# TaskFlow AI

Task management software with automated priority assignment and team collaboration tools.

![Status](https://img.shields.io/badge/status-active-success)
![License](https://img.shields.io/badge/license-MIT-green)

## Overview

TaskFlow AI is a web application that organizes work for individuals and teams. The system uses machine learning models to classify task descriptions, assign priority levels, and suggest completion dates. Teams can share project boards, assign tasks, and track project progress through a central dashboard.

## Why TaskFlow AI?

Manual task tracking requires constant updates and sorting. Unorganized task lists make it difficult to identify urgent assignments.

TaskFlow AI automates routine organization tasks so team members can focus on execution. The application provides:

* Automated priority scores based on task urgency and deadlines
* Automated categorization for incoming requests
* Shared project boards with real-time status updates
* Completion metrics and project velocity charts
* PostgreSQL storage for reliable data persistence

## Features

### Automated Task Classification

The system evaluates task titles and descriptions using language models. It assigns categories, urgency tags, and estimated durations automatically.

### Task Organization

Users can create, edit, group, and filter tasks. The interface supports list views, project boards, and status columns.

### Team Collaboration

Team members can share boards, assign tasks to owners, and leave comments. Status updates appear immediately across active sessions.

### Progress Analytics

The analytics dashboard shows task completion rates, average turnaround time, and overdue items across projects.

### Access Control and Data Storage

TaskFlow AI stores user data in PostgreSQL. Role-based permissions ensure that only authorized team members can access sensitive project boards.

### Responsive Interface

The interface adapts to desktop, tablet, and mobile screens. Keyboard shortcuts allow quick task creation and navigation.

## Tech Stack

| Component | Technology | Function |
|---|---|---|
| Frontend | React, TypeScript, Tailwind CSS | Renders the user interface |
| Backend | Node.js, Express | Manages application logic and API requests |
| Database | PostgreSQL | Stores application and user data |
| Language Model | OpenAI API or local Ollama endpoint | Evaluates task text for category and priority |

The frontend communicates with the Node.js API server over HTTP. The server writes data to PostgreSQL and dispatches text classification requests to the configured model endpoint.

## Getting Started

### Prerequisites

Verify that your system has the following software installed:

* Node.js version 18.0.0 or later
* npm version 9.0.0 or later
* PostgreSQL version 14 or later

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/example/taskflow-ai.git
   cd taskflow-ai
   ```

2. Install the required dependencies:

   ```bash
   npm install
   ```

3. Create the environment configuration file:

   ```bash
   cp .env.example .env
   ```

4. Configure the environment variables in the `.env` file:

   ```env
   PORT=3000
   DATABASE_URL=postgresql://postgres:postgres@localhost:5432/taskflow
   OPENAI_API_KEY=your-api-key-here
   OPENAI_MODEL=gpt-4o-mini
   ```

   If you use local inference, set `OLLAMA_BASE_URL` instead of `OPENAI_API_KEY`.

5. Apply database migrations:

   ```bash
   npm run db:migrate
   ```

6. Start the development server:

   ```bash
   npm run dev
   ```

7. Open `http://localhost:3000` in your web browser.

## System Architecture

TaskFlow AI processes tasks through five stages:

1. **Task creation**: The user submits a task with a title and optional description.
2. **Analysis**: The backend server extracts the text and prepares a structured prompt.
3. **Evaluation**: The model assigns a category, priority level, and estimated duration.
4. **Storage**: The application writes the enriched task record to the PostgreSQL database.
5. **Display**: The frontend receives the updated record and displays it on the active board.

If the model request fails or times out, the system applies default tags and marks the task for manual review.

## Roadmap

* [x] Core task creation, updates, and deletion
* [x] Board and list views
* [x] Automated priority and category suggestions
* [x] PostgreSQL storage with schema migrations
* [ ] Real-time updates with WebSockets
* [ ] Third-party issue tracker synchronization
* [ ] Mobile application builds for iOS and Android
* [ ] CSV and JSON data export

To suggest a feature or report a defect, open an issue in the repository.

## Contributing

To contribute code or documentation to TaskFlow AI:

1. Fork the repository on GitHub.
2. Create a feature branch:

   ```bash
   git checkout -b feature/your-feature-name
   ```

3. Make your modifications.
4. Verify that all automated tests pass:

   ```bash
   npm test
   ```

5. Commit your changes with a descriptive message.
6. Push your branch to GitHub.
7. Open a pull request against the `main` branch.

## Project Scope

TaskFlow AI is designed to minimize manual task administration. The system provides predictable, automated organization for teams that manage high volumes of daily tasks.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

## Acknowledgments

This application uses open-source software, including React, Node.js, Express, Tailwind CSS, and Prisma.
