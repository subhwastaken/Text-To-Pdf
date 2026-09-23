<div align="center">

# ClarityOS (formerly Text-To-Pdf)

**The AI-powered clarity and document operating system for humans who refuse to read walls of text.**

[![Next.js](https://img.shields.io/badge/Next.js-16-black?style=for-the-badge&logo=next.js)](https://nextjs.org/)
[![React](https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://react.dev/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-4-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Google Gemini](https://img.shields.io/badge/Google-Gemini_AI-4285F4?style=for-the-badge&logo=google&logoColor=white)](https://ai.google.dev/)
[![React-PDF](https://img.shields.io/badge/React--PDF-4.5-E11D48?style=for-the-badge)](https://react-pdf.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

*Because turning raw existential dread and messy brain dumps into pristine, structured PDFs should feel like magic, not a root canal.*

[Overview](#overview) • [Key Features](#key-features) • [Architecture](#architecture) • [Getting Started](#getting-started) • [Project Structure](#project-structure) • [Deployment](#deployment)

</div>

---

## Overview

**ClarityOS** (built on our high-performance Text-to-PDF engine) is your personal sanity-preserving operating system. We take raw, unhinged stream-of-consciousness text, meeting transcripts, or late-night brainstorms and run them through advanced LLM structuring intelligence. 

The result? Publication-ready PDF documents with 1:1 layout fidelity, structured headings, clean tables, and zero formatting headaches. 

> *"Like having a meticulous executive assistant who lives inside your browser and doesn't judge your grammar."* — Nobody yet, but we're claiming the quote.

---

## Key Features

- **Split-Pane Markdown Editor**: Real-time side-by-side editing with GitHub Flavored Markdown (GFM) support powered by `@uiw/react-md-editor`.
- **Intelligent AI Restructuring**: Powered by the Google Gemini API to parse unformatted ramblings into:
  - Structured heading hierarchies (`H1` to `H4`)
  - Formatted Markdown tables (because spreadsheets are scary)
  - Styled alert callout boxes for Notes, Warnings, and Pro-Tips
  - Syntax-highlighted code blocks
  - Bulleted and numbered procedural checklists
- **1:1 Pixel-Accurate PDF Generation**: Bridges `@react-pdf/renderer` with `react-pdf-html` and `marked` so your exported PDFs actually look like the preview instead of abstract modern art.
- **Automated Table of Contents (TOC)**: Dynamically indexes document headings and calculates page anchors.
- **Dual Export Modes**:
  - **Raw Text PDF**: Fast, minimal export preserving raw formatting.
  - **AI Enhanced PDF**: Formatted output with typographic hierarchy, badges, callouts, and borders.
- **Zero Lock-in & Privacy**: Runs on your own Gemini API key with client-side PDF rendering. Your secrets stay yours.

---

## Architecture

```mermaid
flowchart LR
    subgraph UI["Frontend UI (Next.js 16)"]
        Editor["@uiw/react-md-editor\n(Live Markdown View)"]
        Toolbar["Export & AI Controls"]
    end

    subgraph API["Backend API Route"]
        GeminiRoute["/api/format\n(Gemini 1.5 / 2.0 Flash)"]
    end

    subgraph Engine["PDF Generation Pipeline"]
        MarkedParser["Marked.js\n(Markdown to HTML)"]
        PDFHTML["react-pdf-html\n(HTML to PDF Primitives)"]
        ReactPDF["@react-pdf/renderer\n(Vector PDF Engine)"]
    end

    subgraph Output["Artifact Deliverable"]
        PDFFile["Downloadable PDF\n(1:1 Layout Matched)"]
    end

    Editor --> Toolbar
    Toolbar -->|"Raw Prompt / Text"| GeminiRoute
    GeminiRoute -->|"Structured Markdown"| Editor
    Editor --> MarkedParser
    MarkedParser --> PDFHTML
    PDFHTML --> ReactPDF
    ReactPDF --> PDFFile
```

---

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) v18.18.0 or higher
- [npm](https://www.npmjs.com/) or [pnpm](https://pnpm.io/)
- A [Google AI Studio Gemini API Key](https://aistudio.google.com/) (bring your own caffeine too)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/subhwastaken/Text-To-Pdf.git
   cd Text-To-Pdf
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Configure Environment Variables:**
   Create a `.env.local` file in the project root:
   ```env
   GEMINI_API_KEY=your_gemini_api_key_here
   ```

4. **Start the Development Server:**
   ```bash
   npm run dev
   ```

5. **Access the Application:**
   Open your browser and navigate to `http://localhost:3000` and experience true clarity.

---

## Project Structure

```
Text-To-Pdf/
├── public/                  # Static assets and brand icons
├── src/
│   ├── app/
│   │   ├── api/
│   │   │   └── format/      # Gemini API formatting route
│   │   │       └── route.js
│   │   ├── globals.css      # Custom design system & theme variables
│   │   ├── layout.js        # Root application layout
│   │   └── page.js          # Main split-pane workspace
│   └── components/
│       ├── MarkdownPDF.js   # @react-pdf document definition & styling
│       └── PDFDownloadSection.js # PDF preview & download handler
├── package.json
├── next.config.mjs
├── postcss.config.mjs
└── README.md
```

---

## Deployment

### Deploy on Vercel

The fastest way to deploy your ClarityOS instance:

1. Push your repository to GitHub.
2. Import the repository into [Vercel](https://vercel.com/new).
3. Under **Environment Variables**, configure:
   - `GEMINI_API_KEY`: Your Google AI Studio API key.
4. Click **Deploy** and marvel at your new creation.

---

## License

This project is licensed under the [MIT License](LICENSE).
