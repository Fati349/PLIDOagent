# PLIDOagent

**Initiation pratique à l'IA agentique, avec des notebooks Jupyter.**

PLIDOagent est une série de travaux pratiques pour découvrir pas à pas comment fonctionnent les **agents IA** : des programmes qui interrogent des LLM, appellent des outils, gardent une mémoire et coopèrent entre eux. Chaque notebook part d'un scénario concret (un professeur qui corrige des copies, un assistant de cours, un conseiller d'orientation…) et ajoute une notion à chaque étape.

Les supports sont en **français**. La plupart ont une version **anglaise** (fichiers `*-eng.ipynb`).

---

## Parcours

Suivez les notebooks dans cet ordre :

| # | Notebook | Scénario | Notions abordées |
|---|----------|----------|------------------|
| 1 | [Prof_philo.ipynb](Prof_philo.ipynb) · [EN](Prof_philo-eng.ipynb) | Un professeur de philosophie donne un sujet à plusieurs « élèves IA », puis fait noter leurs copies par un autre LLM. | Clés d'API, interface OpenAI-compatible, rôles `system` / `user` / `assistant`, comparaison de modèles (Université de Rennes, Gemini, Ollama), boucle évaluateur / correcteur |
| 2 | [Prof_reseau.ipynb](Prof_reseau.ipynb) · [EN](Prof_reseau-eng.ipynb) | Un assistant répond aux questions des étudiants sur le livre *Programmer l'Internet des Objets*. | SDK `openai-agents` (`Agent`, `Runner`), traces, interface de chat avec Gradio, agents en parallèle avec `asyncio`, outils (`@function_tool`), notifications Pushover, agents utilisés comme outils, garde-fous |
| 3 | [Eleve_TAF.ipynb](Eleve_TAF.ipynb) · [EN](Eleve_TAF-eng.ipynb) | Des agents conseillent les étudiants de l'IMT Atlantique dans le choix de leur TAF (et mettent en avant la TAF IoT). | **MCP** (Model Context Protocol) : mémoire persistante, système de fichiers, recherche web Brave, sortie JSON structurée, agents secondaires |
| 4 | [smolagents-eng.ipynb](smolagents-eng.ipynb) *(EN uniquement)* | Un agent qui raisonne en écrivant et en exécutant du code Python. | Framework `smolagents` de Hugging Face, boucle réflexion → code → observation, outils de recherche, imports autorisés |

Le dossier [PLIDOagent-mini/](PLIDOagent-mini/) contient une version courte du notebook TAF, avec un exemple de résultat dans `sandbox/TAF.md`.

---

## Prérequis

- **Python 3.12 ou plus**
- **[uv](https://docs.astral.sh/uv/)** pour gérer l'environnement Python
- **Node.js / `npx`** pour lancer les serveurs MCP (notebook 3)
- **[Ollama](https://ollama.com/)** *(facultatif)* pour faire tourner un modèle en local, par exemple `ollama pull mistral`

## Installation

```bash
git clone https://github.com/Fati349/PLIDOagent.git
cd PLIDOagent

# Installer uv (si besoin)
curl -LsSf https://astral.sh/uv/install.sh | sh

# Créer l'environnement et installer les dépendances
uv sync

# Lancer Jupyter
uv run jupyter lab
```

> Pour le notebook `smolagents`, installez en plus le paquet : `uv add smolagents`.

## Configuration des clés d'API

Créez un fichier `.env` à la racine du dépôt. Vous n'avez besoin que des clés des services que vous utilisez :

```dotenv
# LLM de l'Université de Rennes (RAGaRenn), utilisé par défaut
RENNES_API_KEY=...

# Google Gemini (gratuit) : https://aistudio.google.com/apikey
GOOGLE_API_KEY=...

# OpenAI (payant), utile pour consulter les traces des agents
OPENAI_API_KEY=...

# Notifications sur téléphone (notebook 2) : https://pushover.net
PUSHOVER_TOKEN=...
PUSHOVER_USER_ID=...

# Recherche web via MCP (notebook 3) : https://brave.com/search/api/
BRAVE_API_KEY=...

# Hugging Face (notebook smolagents)
HF_TOKEN=...
```

**Ne versionnez jamais le fichier `.env`.** Ajoutez-le à votre `.gitignore`.

### Fournisseurs de LLM

Les notebooks passent tous par l'**API compatible OpenAI**. Pour changer de fournisseur, il suffit de modifier l'URL et le nom du modèle :

| Fournisseur | Exemple de modèle | Coût |
|-------------|-------------------|------|
| Université de Rennes ([RAGaRenn](https://ragarenn.eskemm-numerique.fr/sso/ch@t/app/auth)) | `mistralai/Mistral-Small-3.1-24B-Instruct-2503` | Gratuit (compte IMT Atlantique) |
| Google Gemini | `gemini-2.0-flash` | Gratuit |
| Ollama (local) | `mistral:latest` | Gratuit, tourne sur votre machine |
| OpenAI | `gpt-4.1-mini` | Payant |

---

## Structure du dépôt

```
PLIDOagent/
├── Prof_philo(-eng).ipynb     # 1. Premiers appels aux LLM
├── Prof_reseau(-eng).ipynb    # 2. Agents, outils, Gradio
├── Eleve_TAF(-eng).ipynb      # 3. Serveurs MCP et mémoire
├── smolagents-eng.ipynb       # 4. Agents qui écrivent du code
├── PLIDOagent-mini/           # Version courte du notebook TAF
├── PLIDO_BOOK_en.pdf          # Livre utilisé comme base de connaissances
├── images/                    # Illustrations et captures d'écran
└── pyproject.toml             # Dépendances (uv)
```

## Ressources

- [OpenAI Agents SDK](https://openai.github.io/openai-agents-python/)
- [Model Context Protocol](https://modelcontextprotocol.io/)
- Annuaires de serveurs MCP : [mcp.so](https://mcp.so), [glama.ai/mcp](https://glama.ai/mcp), [smithery.ai](https://smithery.ai/)
- [smolagents (Hugging Face)](https://huggingface.co/docs/smolagents)
- [Gradio](https://www.gradio.app/)
