# Guide to Standardized Project Task Creation

This guide outlines the essential steps and structural requirements for preparing new project tasks to be integrated into the _Marketable IT Skills_ (MITS) repository and web application. Adhering to these standards ensures **consistency**, **usability**, and **long-term sustainability**.

---

## I. Task Content and Structure

Each task must be documented in **Markdown format** and stored in a dedicated **public GitHub repository**. The repository must contain the following key files and follow a consistent format:

### Required Files

```
/README.md
/project-description.md
/development-and-deployment.md
/metadata.json
/marking/marking-scheme.json
/assets/ (optional media files)
/assets/project-description-images (images for the project-description.md)
```

---

### 1. `project-description.md` – Task Specification

Use the following consistent structure:

#### Heading:

```markdown
# Test Project Outline – [Module Name] – [Skill Area]
```

**Example:**

```markdown
# Test Project Outline – Module A – Static Website Design
```

#### Competition Time:

```markdown
#### Competition time

[Duration in hours]
```

#### Introduction:

A brief description of the project, its context and purpose.

```markdown
## Introduction
```

#### General Description of Project and Tasks:

Include:

- Total number of pages or components
- Provided vs. custom asset expectations
- Technology restrictions (e.g., HTML/CSS only)
- Validation requirements (W3C compliance)
- Required responsive breakpoints (e.g., mobile: 360×640, tablet: 768×1024, desktop: 1920×1080)

```markdown
## General Description of Project and Tasks
```

#### Requirements:

Outline both functional and non-functional requirements include:

- The goal of the solution
- Detailed description of the overall requirements and each individual task requirements

```markdown
## Requirements
```

**Example**

```markdown
## Requirements

The goal of the website is to promote a suite of AI driven APIs.
Potential customers must be able to inform themselves about the possibilities of those APIs, the pricing, and the team behind this product.

You can add more information and elements to all pages as you see fit.
It's also possible to add links that point towards pages that do not exist yet (for example to a login page).

For each page, some example text and more are provided in the media files.
However, not all the provided material has to be used.

The following pages must be implemented.

### Home Page

A short but catching home page.
The idea is to show the product with some simple information and engaging media.
It must contain links to the product and pricing pages where interested visitors can find more information.

### Product Page

The product page shows the whole AI API suite, by listing all available APIs and their features.

### Pricing Page

...
```

#### Assessment:

List tools and methods used for evaluation (e.g., browsers, Axe for WCAG).

```markdown
## Assessment
```

#### Mark Distribution:

Provide a table following this structure:

```markdown
#### Mark distribution

| WSOS SECTION | Description                            | Points |
| ------------ | -------------------------------------- | ------ |
| 1            | Work organization and self-management  | X      |
| 2            | Communication and interpersonal skills | X      |
| 3            | Design Implementation                  | X      |
| 4            | Front-End Development                  | X      |
| 5            | Back-End Development                   | X      |
| **Total**    |                                        | XX     |
```

---

### 2. `README.md` – Repository Overview

Include:

- Title of the project task
- Short description (1–2 sentences)
- **Skill domain(s)** (e.g., Web Technologies)
- **Task origin** (competition name, year, module, authors)
- Links to important documents:
  - `project-description.md`
  - `assets/`
  - `development-and-deployment.md`
  - `marking/marking-scheme.json`
- Short section about the **MITS project**, mentioning:
  - Erasmus+ funding
  - Partner institutions
  - Real-world IT training objective

---

### 3. `metadata.json` – Machine-Readable Task Data

Use the structure below:

```json
{
  "id": 1,
  "name": "ES2023 S17 - Module A",
  "displayName": "AI Services Promo Website",
  "description": "Short description of the task.",
  "url": "https://github.com/marketable-it-skills/example-repo",
  "skillDomainIds": [1],
  "competition": "EuroSkills Gdansk 2023",
  "estTime": 4,
  "authors": [
    { "name": "Author Name", "url": "https://linkedin.com/in/example" }
  ],
  "technologies": ["HTML", "CSS", "JavaScript"],
  "tags": ["frontend", "design", "static website"]
}
```

- Ensure accurate **competition**, **authors**, and **technology tags**
- Follow **tag conventions** for filtering

---

### 4. `development-and-deployment.md` – Local Setup Guide

Explain the setup and deployment process:

````markdown
# How to develop and deploy the project?

1. Create a new GitHub repository using the [HTML and Vanilla JS template](https://github.com/new?template_name=mits-html-and-vanila-js-v1&template_owner=marketable-it-skills).
2. Place your solution code inside the `/src` folder.
3. Pushing to GitHub triggers GitHub Actions (see `.github/`) to:
   - Build a Docker image
   - Push it to GitHub Container Registry
4. In `docker-compose.yml`, update:
   `image: ghcr.io/<your-github-account>/<your-repo-name>:latest`
5. Run locally:
   ```bash
   docker compose up -d
   ```
````

6. Visit: [http://localhost](http://localhost)

---

## II. Technical Setup for Task Solutions

To ensure consistency and deployability:

1. **Repository Naming**: Follow pattern\
   `sXX-[year]-module_[letter]-[short-description]`
2. **Template Usage**: Always initialize from the correct base template
3. **CI/CD Setup**: Ensure `.github/workflows` is present for GitHub Actions
4. **Docker Config**: Adjust image name in `docker-compose.yml`
5. **Testing**: Verify that the solution runs correctly at `localhost` using Docker Compose

---

## III. Additional Technical Considerations

- ✅ **Markdown Conversion**: All task descriptions must be in `.md` format

- ✅ **Standard Structure**: Ensure headings and sections follow the naming conventions above

- ✅ **AI Review**: Use AI tools to improve clarity, grammar, and consistency

- ✅ **Professional Review**: Validate technical content, update any outdated instructions

- ✅ **Asset Management**: Keep `assets/` clean and organized

- ✅ **Meta Tagging**: Assign searchable tags in `metadata.json`

- ✅ **Marking Scheme JSON**: Store the evaluation breakdown in `/marking/marking-scheme.json`. Use types such as `judgement`, `measurement`, and structures like `options` or `pass-or-fail` to support the embedded web application interface.

  **Example:**

  ```json
  {
    "totalMark": 17,
    "wsosSections": {
      "1": "Work organization and self-management"
    },
    "subCriterions": [
      {
        "name": "Website Layout",
        "aspects": [
          {
            "type": "judgement",
            "description": "Common website elements (header, navigation, footer) are responsive",
            "wsosSection": 1,
            "judgementScoreDescription": [
              "All common elements are not responsive at all",
              "At least one common element is responsive",
              "All common elements look good on defined viewports",
              "All common elements always respond well across screen sizes"
            ],
            "maxMark": 0.5
          },
          {
            "type": "measurement",
            "description": "Header, Navigation, and Footer are on all pages",
            "extraDescription": "Elements are consistent across all pages (except highlighting)",
            "calculation": {
              "type": "options",
              "options": [
                { "value": 0, "description": "Not on all pages" },
                { "value": 0.25, "description": "Present but inconsistent" },
                { "value": 0.5, "description": "Present and consistent" }
              ]
            },
            "maxMark": 0.5
          }
        ]
      }
    ]
  }
  ```

- ✅ **Public Upload**: Push the full repository (including markdown, JSON, and media) to GitHub

---

By following this guide, new project tasks will be uniformly structured, easy to integrate into the MITS web application, and provide effective real-world learning experiences for vocational IT training.
