# TP6 – Agentic RAG (Retrieval-Augmented Generation)

## 📌 Description

Ce projet consiste à concevoir et implémenter un système **Agentic RAG (Retrieval-Augmented Generation)** permettant d'interroger une base documentaire contenant des rapports d'analystes et des documents relatifs aux initiatives en Intelligence Artificielle des entreprises.

Contrairement à un système RAG classique, l'approche Agentic RAG intègre un agent intelligent capable de décider quand utiliser un outil de recherche documentaire pour répondre aux questions de l'utilisateur.

Le système combine **LangChain, LangGraph, ChromaDB et Ollama** afin de fournir des réponses pertinentes, contextualisées et fondées sur les documents disponibles.

## 🎯 Objectifs

- Charger et exploiter des documents PDF.
- Extraire et découper les documents en segments (*chunks*).
- Générer des représentations vectorielles à l'aide de modèles d'embeddings.
- Stocker les vecteurs dans une base de données ChromaDB.
- Effectuer une recherche sémantique pour récupérer les informations pertinentes.
- Développer un agent intelligent avec LangGraph.
- Intégrer un LLM local via Ollama pour générer des réponses contextualisées.
- Tester le fonctionnement du système Agentic RAG.

## 🛠️ Technologies utilisées

| Technologie | Utilisation |
|---|---|
| Python | Langage de programmation |
| LangChain | Construction du pipeline RAG |
| LangGraph | Orchestration de l'agent intelligent |
| ChromaDB | Stockage vectoriel |
| Hugging Face | Modèles d'embeddings |
| Sentence Transformers | Représentation vectorielle des textes |
| Ollama | Exécution du LLM local |
| Llama 3.1 (8B) | Génération des réponses |
| PyPDF | Chargement des documents PDF |

## 🏗️ Architecture du projet

Le système repose sur les étapes suivantes :

1. **Document Loading :** chargement des fichiers PDF depuis le dossier `resources/`.
2. **Text Splitting :** découpage des documents en chunks de 1000 tokens avec un chevauchement de 200 tokens.
3. **Embedding Generation :** transformation des chunks en vecteurs avec `all-mpnet-base-v2`.
4. **Vector Database :** stockage des embeddings dans ChromaDB.
5. **Semantic Retrieval :** récupération des 10 chunks les plus pertinents par recherche de similarité.
6. **Agent Creation :** création d'un agent avec LangGraph capable de décider d'utiliser l'outil de recherche documentaire.
7. **LLM Integration :** utilisation de Llama 3.1 (8B) via Ollama pour générer les réponses.
8. **Response Generation :** génération de réponses basées sur les informations récupérées dans les documents.

## 📂 Structure du projet

```text
TP6-Agentic-RAG/
│
├── resources/
│   └── *.pdf                 # Documents sources
│
├── Tp6_RAG_Agentique.ipynb   # Notebook principal
│
└── README.md
```

## ⚙️ Installation et configuration

### 1. Cloner le dépôt

```bash
git clone <YOUR_REPOSITORY_URL>
cd TP6-Agentic-RAG
```

### 2. Installer les dépendances

```bash
pip install -U \
    langchain \
    langchain-text-splitters \
    langchain-community \
    langchain-huggingface \
    langchain-ollama \
    pypdf \
    chromadb \
    langgraph \
    sentence-transformers \
    tiktoken
```

### 3. Installer et configurer Ollama

Installer Ollama depuis son site officiel :

https://ollama.com/

Télécharger le modèle utilisé dans le projet :

```bash
ollama pull llama3.1:8b
```

Démarrer le serveur Ollama :

```bash
ollama serve
```

### 4. Ajouter les documents PDF

Placer les documents PDF à analyser dans le dossier `resources/` à la racine du projet.

### 5. Exécuter le notebook

Ouvrir `Tp6_RAG_Agentique.ipynb` dans Jupyter Notebook ou Google Colab et exécuter les cellules dans l'ordre.

**Remarque :** Ollama doit être installé et son serveur doit être accessible pour utiliser le LLM. Sur Google Colab, son installation et son démarrage doivent être effectués dans l'environnement Colab.

## 🧪 Tests et expérimentations

Le notebook comprend plusieurs expérimentations :

- Test de la recherche sémantique avec une question sur les projets IA de NVIDIA.
- Vérification des documents et chunks récupérés.
- Intégration de l'outil `retriever_tool` dans l'agent.
- Construction et visualisation du graphe LangGraph.
- Test final de l'agent avec une requête portant sur les initiatives de recherche en IA de NVIDIA et Google.

## 🔄 Fonctionnement de l'agent

L'agent suit un workflow cyclique :

```text
        User Query
             |
             v
        Agent Node
             |
             v
     Should use a tool?
          /     \
        Yes      No
         |        |
         v        v
     Tools Node   END
         |
         v
     Agent Node
         |
         v
    Final Response
```

L'agent peut ainsi décider d'appeler le retriever pour récupérer des informations pertinentes, puis exploiter ces informations afin de produire une réponse contextualisée.

## 👨‍💻 Auteur

**Hamza Elazaar**

Master 2 – Artificial Intelligence & Digital Computing (AIDC)

Faculté des Sciences et Techniques de Béni Mellal (FSTBM)

---

*Academic project – TP6: Agentic Retrieval-Augmented Generation (RAG).*
