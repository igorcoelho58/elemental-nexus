# 🎴 ELEMENTAL NEXUS - Desenvolvimento do Jogo

> **README Técnico para Leigos**: Como transformar as regras documentadas em um jogo multiplataforma com a Unity

---

## 🎯 OBJETIVO DESTE DOCUMENTO

Este README explica **como o jogo será programado**, não as regras do jogo (que já estão em `docs/`). Aqui você vai entender:

- Como a Unity transforma ideias em um jogo funcional
- Como as cartas viram elementos digitais interativos
- Como a IA toma decisões
- Como tudo se conecta para virar um jogo de verdade

---

## 🧩 COMO FUNCIONA UM JOGO EM UNITY (Explicação Simples)

Pense na Unity como uma **oficina de criação de jogos**. Ela fornece todas as ferramentas e um espaço de trabalho visual para construir mundos e experiências interativas que funcionam em Android, iOS, Windows, e muitas outras plataformas.

### **O que é Unity?**
É um motor de jogo profissional que permite criar jogos 2D e 3D. Você usa uma linguagem de programação chamada **C# (C Sharp)** para dar vida aos objetos e implementar a lógica do jogo. A grande vantagem é escrever o código **uma vez** e poder publicar em **múltiplas plataformas**.

### **Como Unity constrói um jogo?**

Imagine que você está montando uma **peça de teatro**:

1. **Atores (GameObjects)** = Qualquer objeto em cena (uma carta, um botão, o tabuleiro).
2. **Roteiros (Scripts C#)** = Instruções que dizem aos atores como se comportar. Um script pode fazer uma carta brilhar ou outra aplicar seu efeito.
3. **Cenários (Scenes)** = Cada tela do jogo (o menu principal, a tela de jogo, a tela de vitória).
4. **Adereços reutilizáveis (Prefabs)** = "Modelos" de atores que você pode replicar facilmente. Por exemplo, você cria um modelo de carta (Prefab) e o usa para criar todas as 60 cartas do jogo, apenas mudando os detalhes (arte, texto, etc.).

A Unity junta tudo isso e renderiza o "espetáculo" (o jogo).

---

## 🏗️ ARQUITETURA DO JOGO (Como Tudo se Conecta)

### **1. DADOS DO JOGO (ScriptableObjects)** 📦
*"Como as coisas são representadas digitalmente de forma organizada"*

Para ensinar ao computador **o que é uma carta**, criamos um "molde" de dados chamado **ScriptableObject**. Pense nele como uma ficha catalográfica superpoderosa que vive dentro do editor da Unity.

**Exemplo: Carta "Bosque Sussurrante"**
```csharp
// ScriptableObject que define a estrutura de uma carta
[CreateAssetMenu(fileName = "Nova Carta", menuName = "Elemental Nexus/Carta")]
public class CardData : ScriptableObject
{
    public string nome;
    public CardType tipo;
    public Era era;
    public ResourceCost[] custo;
    public string efeito;
    public int pontos;
    public Sprite arte;
    public CardData corrente;
}
```
No editor da Unity, criamos 60 "assets" a partir deste molde, um para cada carta, preenchendo os campos visualmente.

**Outros dados que criaremos:**
- **PlayerData** → Guarda recursos, cartas jogadas, pontos do jogador.
- **GameState** → Guarda o estado completo do jogo (turno atual, cartas disponíveis, etc.).
- **MonumentData** → Informações de cada monumento, também como ScriptableObjects.

### **2. CENAS (Scenes)** 🖼️
*"As diferentes telas do aplicativo"*

Cada cena é um arquivo que contém um conjunto de objetos e configurações.

**Cenas que criaremos:**
- **MainMenu.unity**: Logo, botões (Jogar, Coleção, Configurações).
- **Game.unity**: Onde a partida acontece. Contém a pirâmide, a UI do jogador e da IA.
- **Collection.unity**: Galeria de cartas.
- **EndGame.unity**: Tela de vitória/derrota.

### **3. MODELOS DE OBJETOS (Prefabs)** 🧩
*"Peças reutilizáveis que aparecem em várias cenas"*

**Card_Prefab**
- Um objeto base que contém a moldura, espaço para a arte, textos para nome e descrição.
- Possui um script `CardController.cs` que recebe o `CardData` e atualiza sua aparência.
- Gerencia animações, brilhos e interações de clique.

**PyramidLayout_Prefab**
- Um objeto que contém a lógica para organizar as cartas em formato de pirâmide.
- Script `PyramidController.cs` que sabe quais cartas estão "soltas" e pode ser pegas.

**ResourceCounter_Prefab**
- UI para mostrar os 5 ícones elementais e a quantidade de cada um.
- Script `UIResourceDisplay.cs` que atualiza os valores.

### **4. LÓGICA DO JOGO (Scripts C#)** 🧠
*"O cérebro que faz tudo funcionar"*

**GameManager.cs** (Motor do Jogo)
- **Função: StartGame()**
  - Carrega os `CardData` da Era I.
  - Instancia os `Card_Prefab` na pirâmide.
  - Define quem joga primeiro.
- **Função: bool CanPlayCard(CardData card, Player player)**
  - Verifica se a carta está solta, se o jogador tem recursos, etc.
- **Função: PlayCard(CardData card, Player player)**
  - Aplica o efeito da carta.
  - Atualiza o `GameState`.
  - Verifica condições de vitória.
- **Função: CheckVictory()**
  - Verifica todas as condições de vitória e encerra o jogo se necessário.

**AIManager.cs** (Inteligência Artificial)
- Implementa os 4 níveis de dificuldade.
- **Função: ChooseMove()** analisa o `GameState` e retorna a melhor jogada possível para a IA.

**CardDatabase.cs** (Gerenciador de Cartas)
- Carrega todos os `ScriptableObjects` de cartas do projeto.
- Fornece acesso fácil a qualquer carta por nome ou ID.

---

## 🔄 FLUXO DE UMA JOGADA (Passo a Passo Técnico)

### **1. TOQUE NA TELA** 👆
- Unity detecta um clique/toque através do seu **EventSystem**.
- Um **Raycast** é disparado da câmera para o ponto do clique.
- O Raycast atinge o **Collider** do `Card_Prefab`.

### **2. VALIDAÇÃO** ✅
- O script `CardController.cs` no prefab da carta notifica o `GameManager.cs`.
- O `GameManager.cs` chama `CanPlayCard()` para verificar:
  - A carta está solta?
  - É o turno do jogador?
  - O jogador tem recursos?

### **3. SE VÁLIDO: ANIMAÇÃO** 🎬
- O `CardController.cs` ativa uma animação (usando o sistema **Animator** da Unity) para fazer a carta brilhar ou aumentar de tamanho.
- A cor da borda pode mudar para verde (pode jogar) ou vermelho (não pode).

### **4. SE TOCA DE NOVO: JOGAR** 🃏
- `GameManager.cs` chama `PlayCard()`.
- A carta é movida da pirâmide para a área do jogador (animação via **Animator** ou **DOTween**).
- Recursos são deduzidos, e o `GameState` é atualizado.

### **5. VERIFICAR VITÓRIA** 🏆
- `GameManager.cs` chama `CheckVictory()`.
- Se alguém ganhou, a cena `EndGame.unity` é carregada.

### **6. TURNO DA IA** 🤖
- `GameManager.cs` chama `AIManager.cs`.
- O `AIManager.cs` executa sua lógica e escolhe uma carta.
- A jogada da IA segue os mesmos passos de validação e execução.

### **7. ATUALIZAR INTERFACE** 🔄
- Scripts de UI (`UIResourceDisplay.cs`, etc.) estão "escutando" por mudanças no `GameState`.
- Quando o estado muda, eles atualizam automaticamente os textos e imagens na tela.

---

## 📲 COMO UNITY VIRA UM APK ANDROID (ou um .exe, etc.)

### **O que é um Build?**
É o processo de compilar seu projeto da Unity em um executável para uma plataforma específica (APK para Android, .exe para Windows, etc.).

### **Processo de Transformação:**

**1. VOCÊ CRIA O JOGO NA UNITY** ✍️
- Monta cenas com GameObjects.
- Escreve lógica em scripts C#.
- Importa artes, sons e modelos.

**2. UNITY COMPILA** 🔧
- Você vai em `File > Build Settings`.
- Escolhe a plataforma (ex: Android).
- Clica em `Build`.
- Unity pega tudo (cenas, scripts, assets), compila o código C#, otimiza os assets e empacota tudo no formato da plataforma.

**3. GERA O ARQUIVO FINAL** 📦
- Um arquivo `ElementalNexus.apk` (ou `.exe`, etc.) é criado.
- Pronto para instalar ou distribuir.

### **Desenvolvimento x Produção**

- **No Editor:** Você testa o jogo em tempo real clicando no botão "Play". Pode pausar, inspecionar variáveis e fazer mudanças ao vivo.
- **Em Dispositivos:** Com o **Unity Remote**, você pode espelhar o jogo no seu celular conectado via USB para testar os controles de toque diretamente.

---

## 🧪 COMO TESTAR SE ESTÁ FUNCIONANDO

### **Testes Unitários e de Integração**
A Unity possui uma ferramenta chamada **Test Runner** (`Window > General > Test Runner`).

- **Edit Mode Tests:** Testam a lógica pura (funções em scripts) sem precisar rodar o jogo. São super rápidos.
- **Play Mode Tests:** Rodam como uma cena especial, permitindo testar interações que dependem do motor do jogo (física, animações, etc.).

### **Teste Manual** (Você jogando)
O mais importante. Você joga e verifica:
- As animações estão fluidas?
- A UI é intuitiva?
- A IA é desafiadora, mas justa?

---

## 🎨 COMO AS IMAGENS ENTRAM NO JOGO

### **1. IMPORTAR ASSETS** 🖼️
- Você simplesmente arrasta e solta suas imagens (PNG, JPG) na janela de `Project` da Unity, dentro da pasta `Assets`.
- A Unity as importa e cria metadados para elas.

### **2. CONFIGURAR SPRITES** 🎨
- Para jogos 2D, você seleciona as imagens importadas e muda o "Texture Type" para **"Sprite (2D and UI)"**.
- Isso otimiza as imagens para renderização 2D.

### **3. USAR NO JOGO** 💻
- **Em um Prefab:** Você arrasta o Sprite para o campo `Sprite Renderer` de um GameObject ou para um `Image` da UI.
- **Via Código:** Você pode carregar e atribuir Sprites dinamicamente.
  ```csharp
  public Image cardArtImage;
  public Sprite newArt;

  void ChangeArt() {
      cardArtImage.sprite = newArt;
  }
  ```

---

## 📂 ORGANIZAÇÃO DO PROJETO (Estrutura de Pastas na Unity)

```
ELEMENTAL NEXUS/ (Pasta do projeto Unity)
│
├── 📁 Assets/         → Pasta principal de tudo que vai no jogo
│   ├── 📁 _Project/      → Nossos scripts, cenas e prefabs
│   │   ├── 📁 Scenes/       (MainMenu, Game, etc.)
│   │   ├── 📁 Scripts/
│   │   │   ├── Data/          (ScriptableObjects: CardData, MonumentData)
│   │   │   ├── Gameplay/      (GameManager, PlayerController)
│   │   │   ├── AI/            (AIManager, AI Levels)
│   │   │   └── UI/            (UI-related scripts)
│   │   ├── 📁 Prefabs/      (Card_Prefab, PyramidLayout_Prefab)
│   │   └── 📁 ScriptableObjects/
│   │       ├── 📁 Cards/        (60 assets de CardData)
│   │       └── 📁 Monuments/    (20 assets de MonumentData)
│   │
│   ├── 📁 Art/          → Imagens, texturas, ícones
│   │   ├── 📁 Cards/
│   │   └── 📁 UI/
│   │
│   ├── 📁 Audio/        → Músicas e efeitos sonoros
│   └── 📁 Plugins/       → Pacotes de terceiros (ex: DOTween)
│
├── 📁 Packages/       → Pacotes da Unity (Test Runner, etc.)
└── 📁 ProjectSettings/ → Configurações do projeto
```

---

## 🎯 FASES DE PROGRAMAÇÃO (Detalhado com Unity)

- **FASE 1: Setup Inicial** (1 semana)
  - Instalar Unity Hub e a versão LTS recomendada.
  - Criar projeto 2D.
  - Configurar estrutura de pastas em `Assets/`.
  - Importar as primeiras imagens.
  - Fazer uma cena de teste com um cubo que gira via script C#.

- **FASE 2: Modelos de Dados e Cartas** (2 semanas)
  - Criar os `ScriptableObjects` (`CardData`, `MonumentData`).
  - Criar os 60 assets de `CardData` no editor e preenchê-los.
  - Criar o `Card_Prefab` básico que mostra a arte e o nome de um `CardData`.

- **FASE 3: Lógica Central do Jogo** (3 semanas)
  - Criar o `GameManager.cs`.
  - Implementar a lógica de turnos, recursos e custos.
  - Implementar o layout da pirâmide e a lógica de quais cartas estão livres.
  - Permitir que o jogador pegue uma carta e a adicione à sua área.

- **FASE 4: IA e Condições de Vitória** (3 semanas)
  - Implementar o `AIManager.cs` com os níveis de dificuldade.
  - Conectar a IA ao `GameManager`.
  - Implementar a verificação de todas as condições de vitória (militar, ciência, etc.).
  - Criar as cenas de Menu e Fim de Jogo.

- **FASE 5: UI e Polimento** (2 semanas)
  - Construir a UI completa (contadores, trilha militar).
  - Adicionar animações com o Animator e/ou DOTween.
  - Adicionar efeitos sonoros e música.

- **FASE 6: Testes e Build** (1 semana)
  - Escrever testes no Test Runner.
  - Jogar extensivamente para encontrar bugs.
  - Fazer o build para Android e testar no dispositivo.

**Total: ~3-4 meses**

---

## 🛠️ FERRAMENTAS E TECNOLOGIAS

- **Motor de Jogo:** **Unity 2022 LTS** (ou mais recente)
- **Linguagem:** **C#**
- **IDE:** **Visual Studio** ou **JetBrains Rider**
- **Arte:** Leonardo.ai / Gemini, Photoshop / Figma
- **Controle de Versão:** Git + GitHub (com Git LFS para assets grandes)
- **Animação (Opcional):** [DOTween](http://dotween.demigiant.com/) para animações via código.

---

## 💡 CONCEITOS-CHAVE DA UNITY

- **GameObject:** O objeto fundamental. Tudo em uma cena é um GameObject.
- **Component:** Peças de funcionalidade que você anexa a um GameObject. Um `Sprite Renderer` é um componente para exibir uma imagem 2D. Um script C# também é um componente.
- **Prefab:** Um "molde" de um GameObject, incluindo seus componentes e configurações. Salva tempo e garante consistência.
- **Scene:** Um nível ou tela do seu jogo. Contém uma coleção de GameObjects.
- **ScriptableObject:** Um container de dados que não precisa estar atrelado a uma cena. Perfeito para definir cartas, itens, etc., de forma reutilizável.

---

**Versão Atual**: 0.2.0 - Fase de Design (Tecnologia redefinida para Unity)
**Próxima Meta**: Gerar 60 artes de cartas e iniciar o setup do projeto Unity.

🎴 **Que os Elementos estejam com você!** ✨