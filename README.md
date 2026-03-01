# JARVIS — Local AI Assistant (Ollama + Python)

## Overview

**Jarvis** est un assistant IA local capable d’interpréter des commandes en langage naturel et d’exécuter des actions sur un ordinateur.

Le projet repose sur un principe simple :

```
Commande utilisateur → LLM local → Intention structurée → Action système
```

Aucune API externe n’est nécessaire. Tout fonctionne **en local** via Ollama.

Ce dépôt représente le **MVP (Minimum Viable Product)** servant de base pour des évolutions futures :

- reconnaissance vocale
- synthèse vocale
- mémoire conversationnelle
- système de plugins

---

## Features (MVP)

- Exécution locale (offline)
- Interprétation de commandes naturelles
- Conversion des instructions en JSON structuré
- Exécution sécurisée d’actions système
- Architecture extensible

Actions actuellement supportées :

- Ouvrir une application
- Ouvrir un site web
- Créer un fichier
- Éteindre le PC

---

## Architecture

```
User Input (text)
        ↓
Python CLI
        ↓
Ollama LLM
        ↓
JSON Action
        ↓
Action Executor
        ↓
Operating System
```

Le modèle IA **ne lance jamais directement du code**.
Il produit uniquement une intention structurée interprétée par Python.

---

## Requirements

- Python 3.10+
- Ollama installé
- OS : Windows / Linux / macOS

---

## Installation

### 1. Installer Ollama

Installer depuis :

https://ollama.com

Vérifier :

```bash
ollama run llama3
```

---

### 2. Télécharger un modèle

Exemple recommandé :

```bash
ollama pull llama3.2
```

Modèles compatibles :

- llama3.2 (équilibre performance/qualité)
- mistral (rapide)
- phi3 (léger)

---

### 3. Cloner le projet

```bash
git clone <repo-url>
cd jarvis
```

---

### 4. Créer un environnement virtuel

```bash
python -m venv venv
```

Activation :

**Windows**

```bash
venv\Scripts\activate
```

**Linux / macOS**

```bash
source venv/bin/activate
```

---

### 5. Installer les dépendances

```bash
pip install ollama rich
```

---

## Usage

Lancer Jarvis :

```bash
python jarvis.py
```

Exemples de commandes :

```
ouvre notepad
ouvre google.com
cree fichier test.txt
eteins le pc
```

---

## Core Concept

Le LLM transforme une commande en JSON strict :

```json
{
  "action": "open_app",
  "target": "chrome"
}
```

Python valide ensuite la commande avant exécution.

Cette séparation permet :

- plus de sécurité
- contrôle total des actions
- extensibilité simple

---

## Project Structure

```
jarvis/
│
├── jarvis.py        # boucle principale
├── executor.py      # exécution des actions système (future)
├── tools/           # actions disponibles (future)
├── prompts/         # prompts système (future)
└── README.md
```

---

## Security Notes

Le modèle IA peut halluciner.
Les actions doivent toujours être :

- validées
- limitées à une liste autorisée
- exécutées côté Python uniquement

Ne jamais exécuter directement du code généré par le LLM.

---

## Roadmap

### v0 — MVP (actuel)

- Commandes texte
- Actions système basiques
- LLM local via Ollama

### v1

- Système de tools modulaire
- Mémoire conversationnelle
- Validation intelligente des actions

### v2

- Reconnaissance vocale (Speech-to-Text)
- Synthèse vocale (Text-to-Speech)
- Mode assistant continu

### v3

- Plugins dynamiques
- Automatisation multi-étapes
- Agent autonome local

---

## Future Additions

Technologies envisagées :

- faster-whisper → reconnaissance vocale locale
- pyttsx3 / Coqui-TTS → synthèse vocale
- Web UI (FastAPI + Next.js)
- Memory store (SQLite / vector DB)

---

## Philosophy

- Local-first
- Privacy-focused
- Modular design
- Controlled AI execution

Jarvis n’est pas un chatbot.
C’est un **agent système piloté par IA**.

---

## License

MIT License (modifiable selon le projet).

---
