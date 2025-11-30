# Arquitetura do Jogo (Unity)

Este documento descreve a arquitetura técnica do jogo **ELEMENTAL NEXUS** na engine Unity.

## 🏗️ Visão Geral da Arquitetura

A arquitetura seguirá o padrão **Component-Based** da Unity, com uma clara separação entre **Dados (Data)**, **Lógica (Logic)** e **Visualização (View)**.

- **View (Visualização):** Cenas da Unity, Prefabs, componentes de UI (Canvas, Image, Text), e Renderers. Responsável por mostrar o jogo ao jogador.
- **Logic (Lógica):** Scripts C# que controlam o fluxo do jogo (`GameManager`), o comportamento da IA (`AIManager`), e as interações do jogador (`InputManager`, `CardController`).
- **Data (Dados):** `ScriptableObjects` para definir os dados estáticos de cartas e monumentos, e classes C# simples para representar o estado dinâmico do jogo (`GameState`, `PlayerData`).

## 📂 Estrutura de Pastas (Assets/_Project)

```
_Project/
├── 📁 Scenes/       (Cenas como MainMenu, Game, etc.)
├── 📁 Scripts/      (Todo o código C#)
│   ├── Data/         (Definições de ScriptableObjects e classes de estado)
│   ├── Gameplay/     (Scripts centrais como GameManager)
│   ├── AI/           (Scripts relacionados à Inteligência Artificial)
│   ├── UI/           (Scripts para controlar elementos da interface)
│   └── Controllers/  (Scripts para controlar objetos específicos do jogo, como cartas)
├── 📁 Prefabs/      (Modelos de GameObjects, como Card_Prefab)
├── 📁 ScriptableObjects/
│   ├── 📁 Cards/       (Assets de dados para cada uma das 60 cartas)
│   └── 📁 Monuments/  (Assets de dados para cada monumento)
└── 📁 Art/          (Sprites, Ícones, etc.)
```

## 🧠 Componentes Principais

### **GameManager.cs**
- **Singleton** que orquestra todo o jogo.
- Gerencia turnos, estado do jogo (`GameState`), e condições de vitória.
- Comunica-se com o `AIManager`, `UIManager` e `InputManager`.

### **CardData.cs (ScriptableObject)**
- Define todos os atributos de uma carta (nome, custo, efeito, arte, etc.).
- Permite que designers de jogo criem e editem cartas no editor da Unity sem precisar mexer no código.

### **CardController.cs**
- Script anexado ao `Card_Prefab`.
- Recebe um `CardData` e atualiza a aparência do prefab (arte, textos).
- Gerencia interações do usuário (cliques, arrastar) e animações.

### **GameState.cs**
- Uma classe C# simples (não é `MonoBehaviour`) que contém todas as informações dinâmicas do jogo: turno atual, recursos de cada jogador, cartas na pirâmide, etc.
- Facilita o salvamento/carregamento do jogo e a simulação de jogadas pela IA.

### **AIManager.cs**
- Contém a lógica para os 4 níveis de IA.
- Recebe o `GameState` atual, analisa as jogadas possíveis e retorna a ação escolhida.

## 🔄 Fluxo de Dados e Eventos

Usaremos um sistema de **eventos** (C# Events ou UnityEvents) para comunicação desacoplada entre os componentes.

- **Exemplo:** Quando uma carta é jogada, o `GameManager` dispara um evento `OnCardPlayed`.
- O `UIManager` escuta esse evento e atualiza a interface.
- O `AudioManager` escuta e toca um som.
- O `AIManager` escuta e inicia seu turno.

Isso evita que o `GameManager` precise ter referências diretas a todos os outros sistemas.

---
*(Este documento é um esboço inicial e será detalhado conforme o desenvolvimento avança.)*
