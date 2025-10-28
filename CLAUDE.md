# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

RGAA Plugin is a Claude Code plugin designed to provide expert guidance on digital accessibility and RGAA (Référentiel Général d'Amélioration de l'Accessibilité) standards. The plugin delivers comprehensive support for accessibility audits, criteria explanation, and WCAG 2.1 compliance verification.

## Project Structure

```
rgaa-pluging/
├── pluging/
│   ├── agents/
│   │   └── rgaa.md                 # RGAA Expert agent definition
│   ├── commands/
│   │   └── audit-rgaa.md           # RGAA audit workflow command
│   └── README.md
├── .claude-plugin/
│   └── marketplace.json            # Plugin configuration for Claude Code marketplace
├── README.md                        # Installation and resource documentation
├── .gitignore                       # Git ignore configuration
└── CLAUDE.md                        # This file
```

## Plugin Architecture

### Agents (`pluging/agents/`)

The agent system defines specialized personalities and capabilities:

- **rgaa.md**: Core RGAA 4.1 accessibility expert agent with:
  - 13 RGAA thematic categories
  - 106 accessibility criteria definitions
  - 257 technical tests for verification
  - 91-term glossary
  - Audit methodologies (rapid, standard, complete)

### Commands (`pluging/commands/`)

Commands define workflow automations:

- **audit-rgaa.md**: Structured RGAA audit workflow for web accessibility assessment

### Plugin Configuration

- **.claude-plugin/marketplace.json**: Plugin metadata for Claude Code marketplace registration and discovery

## Data Sources

The RGAA agent pulls live data from the official DISIC repository to ensure accuracy:

### CURL Data Retrieval

The agent fetches data using CURL from: `https://github.com/DISIC/accessibilite.numerique.gouv.fr/tree/main/RGAA`

Key data sources:

1. **Criteria** (`criteres.json`)

   ```bash
   curl -s https://raw.githubusercontent.com/DISIC/accessibilite.numerique.gouv.fr/main/RGAA/criteres.json
   ```

   - 106 RGAA criteria with WCAG levels (A, AA, AAA)
   - Technical test details
   - Official definitions

2. **Glossary** (`glossaire.json`)

   ```bash
   curl -s https://raw.githubusercontent.com/DISIC/accessibilite.numerique.gouv.fr/main/RGAA/glossaire.json
   ```

   - 91 official term definitions
   - Technical vocabulary reference

3. **Methodologies** (`methodologies.json`)
   ```bash
   curl -s https://raw.githubusercontent.com/DISIC/accessibilite.numerique.gouv.fr/main/RGAA/methodologies.json
   ```

   - Detailed test procedures
   - Verification methods

## Development Guidelines

### Adding New Agents

When creating new agents in `pluging/agents/`:

1. Define the agent's identity and expertise domain
2. Specify capabilities and methodologies
3. Include CURL data retrieval instructions for external sources
4. Define response formats with examples
5. Include transparency about limitations

### Adding New Commands

When creating commands in `pluging/commands/`:

1. Document the workflow step-by-step
2. Reference the agent(s) that execute the command
3. Define input parameters and expected outputs
4. Provide usage examples

### Maintaining Data Accuracy

- Agents must systematically call CURL to fetch live data from DISIC
- Before providing critical responses about:
  - Specific RGAA criteria → Use `criteres.json`
  - Term definitions → Use `glossaire.json`
  - Test methods → Use `methodologies.json`
  - Version-specific clarifications → Check `RGAA/4.1`

## Plugin Marketplace Integration

The plugin is installed via Claude Code's marketplace system:

```bash
/plugin marketplace add https://github.com/leobrival/rgaa-pluging
/plugin
```

Configuration is managed through `.claude-plugin/marketplace.json`.

## Language Conventions

- **Agent and command content**: French (FR) - User-facing text and explanations
- **Configuration and documentation**: English (EN) - For international compatibility
- **Code comments and identifiers**: English (EN)

## Key Principles

1. **Accuracy First**: All responses must reference official RGAA sources via CURL data retrieval
2. **User-Centric**: Agents explain complex accessibility concepts in simple terms
3. **Practical Solutions**: Always provide concrete, actionable recommendations
4. **WCAG-Aligned**: All guidance references WCAG 2.1 and RGAA 4.1 standards
5. **Transparency**: Clearly state limitations and when human judgment is needed
