# Padel Expert Lab — MCP server (padel rackets)

[Padel Expert Lab](https://padelexpertlab.com/) is a free padel racket comparator for France and Belgium. This repository documents its **remote, read-only MCP server**: an AI assistant can search the racket catalogue, read brand specifications and get picks for a player profile. Answers are in French.

> 🇫🇷 Version française plus bas : [Français](#français).

## Connect

| | |
|---|---|
| **Endpoint** | `https://padelexpertlab.com/api/mcp/` (keep the trailing slash) |
| **Transport** | Streamable HTTP |
| **Authentication** | none: no account, no key |
| **Registry name** | [`com.padelexpertlab/raquettes`](https://registry.modelcontextprotocol.io/v0.1/servers?search=com.padelexpertlab) |
| **Documentation** | https://padelexpertlab.com/connecteur-ia/ |

**Claude** (Settings → Connectors → add a custom connector) and **ChatGPT** (developer mode, where OpenAI offers it): paste the endpoint above.

**Claude Code**:

```bash
claude mcp add --transport http padel-expert-lab https://padelexpertlab.com/api/mcp/
```

**Cursor, VS Code and other clients** (`mcp.json`):

```json
{
  "mcpServers": {
    "padel-expert-lab": { "url": "https://padelexpertlab.com/api/mcp/" }
  }
}
```

## Tools

All three are read-only (`readOnlyHint: true`, `destructiveHint: false`, `openWorldHint: false`).

| Tool | What it does |
|---|---|
| `recommander_raquettes` | Up to 3 rackets ranked by fit to a profile: level (required), style, weight, how often you play, budget. Same engine as the site's quiz. |
| `chercher_raquettes` | Search by name (brand, model, player) or by criteria: brand, level, shape, price range, weight, women or junior range. 10 results per page. |
| `voir_raquettes` | Specifications of 1 to 4 rackets (shape, level, weight, balance, core, face), other versions and alternatives; a side-by-side table for 2 to 4. |

Example prompts: [examples/prompts.md](examples/prompts.md).

## What the data is

- **Specifications** come from the brands' official product pages.
- **Prices** are the last ones collected **by hand** on the brands' official stores. They are not offers and **may have changed**: check the racket page before buying. How and how often they are collected: https://padelexpertlab.com/methode/#mise-a-jour
- The catalogue covers the racket pages that are complete on the site (267 rackets from 21 brands on 9 November 2026). It is not exhaustive.
- Every answer ends with a link to a page of padelexpertlab.com (racket page or comparator) to see photos and compare visually. **No shop link, no affiliate link.**

## What it does not do

- It never asks about your arm or your health; such a criterion is refused.
- It does not rate rackets. A recommendation shows a percentage of fit with your profile, not a quality score.
- It asks nothing about you: no account, no name, no email.
- It writes nothing. Only an anonymous counter of calls (day, tool, client family) is kept, with no IP address and no arguments. Details: https://padelexpertlab.com/confidentialite/

Bulk or systematic extraction of the catalogue through the server is not allowed without written consent (§ 8 of the [terms of use](https://padelexpertlab.com/conditions-utilisation/)). Your assistant rephrases the answers and can be wrong.

## Contact

contact@padelexpertlab.com · Report an error: https://padelexpertlab.com/signaler-une-erreur/

This repository holds documentation only. The server runs on padelexpertlab.com; its code and the catalogue are not published here.

---

## Français

Padel Expert Lab est un comparateur de raquettes de padel gratuit, pour la France et la Belgique. Ce serveur MCP **en lecture seule** donne à ton assistant IA trois outils sur le catalogue du site : recommander jusqu'à 3 raquettes selon ton profil (niveau, style, poids, fréquence de jeu, budget ; même moteur que le quiz), chercher des raquettes par nom ou par critères, et voir les caractéristiques de 1 à 4 raquettes côte à côte.

- **Adresse** : `https://padelexpertlab.com/api/mcp/` (avec la barre oblique à la fin), sans compte ni clé.
- **Documentation complète** : https://padelexpertlab.com/connecteur-ia/
- **Caractéristiques** : celles des fiches officielles des marques.
- **Prix** : le dernier prix relevé à la main sur la boutique officielle de la marque. Ce n'est pas une offre, et il peut avoir changé.
- Aucun lien de boutique ni lien d'affiliation : chaque réponse renvoie vers une page de padelexpertlab.com.
- Aucune question sur le bras ni la santé, aucune note, aucun compte.

Pourquoi : Bryan, qui publie le site, joue au padel en débutant et a eu du mal à choisir sa raquette.
