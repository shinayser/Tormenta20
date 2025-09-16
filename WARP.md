# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project Overview

T20MasterTools is a comprehensive data repository and PowerShell toolkit for the Tormenta20 tabletop RPG system. The project contains structured JSON data files with game content (weapons, spells, items, creatures, etc.) and PowerShell functions to query and manipulate this data for game masters and players.

## Architecture and Structure

### Core Data Organization

The repository follows a modular data structure with content organized by expansion and source book:

- **`json-t20/`** - Core Tormenta20 rulebook content (weapons, armor, spells, items, etc.)
- **`json-ameacas-arton/`** - "Ameaças de Arton" expansion content
- **`json-ghanor/`** - Ghanor region-specific content
- **`json-deuses-e-herois/`** - Gods and Heroes expansion content, with subdirectories:
  - `deuses/` - Deity-specific items and content
  - `herois/` - Hero-specific content like beverages
- **`utils/`** - Utility files including tavern names and humorous artifacts

### Data Categories

Each JSON directory contains standardized categories:
- `armas.json` - Weapons with stats, descriptions, and properties
- `armaduras.json` - Armor and shields
- `magias.json` - Spells with schools, circles, and improvements
- `esotericos.json` - Esoteric/magical items
- `itens-gerais.json` - General items and equipment
- `alimentacao.json` - Food and provisions
- `animais.json` - Animals and mounts
- Plus specialized files like poisons, catalysts, tools, etc.

### PowerShell Command System

The `powershell/init.ps1` file provides a comprehensive function library with over 50 commands for querying game data. Key functions include:

#### Search Functions
- `Armas()` - Search weapons by name, class, type, grip
- `Magias()` - Search spells by name, class, school, circle
- `Armaduras()` - Search armor by name, class
- `Busca-Item()` - Universal item search across all categories
- `Pericias()` - Search skills and their uses

#### Random Generation
- `Item-Random()` - Generate random weapons, armor, or esoteric items
- `Riquezas()` - Generate treasure by tier (menor/media/maior)
- `Pocoes()` - Random potion generation
- `Personalidade()` - Generate NPC personality traits

#### Game Master Tools
- `Estatisticas-Criaturas()` - Creature statistics by type and challenge rating
- `Armadilhas()` - Trap generation and lookup
- `Perigos-Complexos()` - Complex encounter hazards

## Common Development Tasks

### Loading the PowerShell Environment

To initialize the full toolkit:
```powershell
# Load main functions
. .\powershell\init.ps1

# Load AI-powered functions (requires PSOpenAI module)
. .\powershell\init-ai.ps1

# Load utility functions
. .\powershell\init-utils.ps1
```

### Adding New Content

When adding new game content:

1. **Follow JSON schema patterns** from existing files
2. **Maintain consistent property names** across similar content types
3. **Add content to appropriate expansion directories**
4. **Update PowerShell functions** if new data structures are introduced

### Working with Data

The PowerShell functions handle cross-expansion merging automatically. Functions merge content from multiple sources based on global variables:
- `$includeGhanor` - Include Ghanor content
- `$includeAmeacas` - Include Ameaças de Arton content  
- `$includeHeroisDeArton` - Include Heroes content
- `$includeDeusesDeArton` - Include Gods content

### Content Processing Tools

- **`powershell/Transforma-Magia.ps1`** - Utility to parse and format spell text from clipboard into JSON structure

## Data Schema Patterns

### Standard Item Structure
```json
{
  "nome": "Item Name",
  "preco": 100,
  "descricao": "Item description with mechanics",
  "outros": "Additional properties as needed"
}
```

### Weapon Structure
```json
{
  "nome": "Weapon Name",
  "classe": "simples/marcial/exotica",
  "preco": 50,
  "dano": "1d8",
  "ameaca": 20,
  "critico": "x2",
  "tipo": "corte/perfuracao/impacto",
  "empunhadura": "uma-mao/duas-maos/leve",
  "descricao": "Full description with special rules"
}
```

### Spell Structure
```json
{
  "nome": "Spell Name",
  "classe": "arcana/divina/universal",
  "ciclo": 2,
  "escola": "evocacao",
  "execucao": "padrão",
  "alcance": "curto",
  "duracao": "cena",
  "desc": "Spell description",
  "aprimoramentos": [
    {
      "custo": "+1 PM",
      "desc": "Enhancement description"
    }
  ]
}
```

## Key Files and Usage

- **`jsonGiganteTormenta.json`** - Massive consolidated reference file with core rules data
- **`livros-md/T20 - Jogo do Ano (completo).md`** - Complete game manual in Markdown
- **`utils/artefatos-engracados.json`** - Humorous/gag magical items for comic relief

## Integration Notes

The system is designed for game masters who need quick access to comprehensive game data. All PowerShell functions support:
- Partial name matching with wildcards
- Multi-source content aggregation  
- Flexible output formatting (table vs. detailed list based on result count)
- Consistent parameter naming conventions (aliases like `-t` for type, `-p` for price)

When extending the system, maintain these patterns for consistency with existing workflows.