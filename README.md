# mAInd - Backend (API de Diagnóstico Mental com IA)

API desenvolvida em **Python** com **Flask** para alimentar o chatbot "mAInd". O sistema utiliza um modelo de Machine Learning (KNN) para realizar triagem prévia de condições de saúde mental (Ansiedade, Depressão, Estresse, Solidão) baseado em respostas do usuário.

Projeto apresentado na **FETIN (Feira Tecnológica do Inatel)**.

## 🧠 Tecnologias & Arquitetura

- **Framework:** Flask (Python)
- **ML Algorithm:** K-Nearest Neighbors (KNN) via Scikit-learn
- **Serialização:** Pickle (Carregamento do modelo treinado)
- **Sessão:** Gerenciamento de estado de conversa por usuário via UUID
- **CORS:** Habilitado para integração com Frontend externo

## ⚙️ Fluxo da Aplicação

```mermaid
sequenceDiagram
    participant User
    participant Frontend
    participant API (Flask)
    participant Model (KNN)

    User->>Frontend: Clica em "Iniciar"
    Frontend->>API: POST /mAInd/start
    API-->>Frontend: Retorna Session_ID + Pergunta 1
    
    loop Chat Loop
        User->>Frontend: Responde "Sim" ou "Não"
        Frontend->>API: POST /mAInd (com Session_ID)
        API->>API: Armazena resposta no estado
        API-->>Frontend: Retorna Próxima Pergunta
    end

    API->>Model: Envia vetor de respostas
    Model-->>API: Retorna Predição
    API-->>Frontend: Retorna Diagnóstico Final
