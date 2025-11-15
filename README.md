# 🎴 ELEMENTAL NEXUS - Desenvolvimento do Jogo

> **README Técnico para Leigos**: Como transformar as regras documentadas em um aplicativo Android jogável

---

## � OBJETIVO DESTE DOCUMENTO

Este README explica **como o jogo será programado**, não as regras do jogo (que já estão em `docs/`). Aqui você vai entender:

- Como o Flutter transforma ideias em app Android
- Como as cartas viram elementos digitais interativos
- Como a IA toma decisões
- Como tudo se conecta para virar um jogo de verdade

---

## 🧩 COMO FUNCIONA UM JOGO EM FLUTTER (Explicação Simples)

Pense no Flutter como uma **fábrica de aplicativos**. Ele pega suas ideias (código) e transforma em um app que funciona no celular Android (e até iOS!).

### **O que é Flutter?**
É uma ferramenta do Google que permite escrever código **uma vez** e funcionar em **Android e iOS**. Em vez de aprender linguagens diferentes para cada sistema, você aprende **Dart** (a linguagem do Flutter) e ele faz a tradução.

### **Como Flutter constrói um jogo?**

Imagine que você está construindo com **blocos de LEGO**:

1. **Blocos pequenos** (Widgets) = Botões, textos, imagens
2. **Blocos médios** (Components) = Uma carta completa, um contador de recursos
3. **Blocos grandes** (Screens) = Tela inteira do menu, tela do jogo
4. **Instruções** (Logic) = Regras de como os blocos reagem quando você toca neles

O Flutter junta tudo isso e cria a "casa" (aplicativo).

---

## 🏗️ ARQUITETURA DO JOGO (Como Tudo se Conecta)

### **1. MODELOS DE DADOS (Models)** 📦
*"Como as coisas são representadas digitalmente"*

Imagine que você precisa explicar para o computador **o que é uma carta**. Você criaria uma "ficha técnica":

**Exemplo: Carta "Bosque Sussurrante"**
```
Nome: "Bosque Sussurrante"
Tipo: Recurso
Era: I
Custo: [Nada] (é de graça)
Efeito: Ganhe 1 Natureza
Pontos: 0
Arte: arquivo "bosque_sussurrante.png"
Corrente: Conecta com "Floresta Viva"
```

No código, isso vira uma **classe Card** (como uma ficha em branco que você preenche). Criamos 60 "fichas preenchidas" (uma para cada carta).

**Outros modelos que criaremos:**
- **Player** → Guarda recursos, cartas jogadas, pontos do jogador
- **GameState** → Guarda o estado completo do jogo (turno atual, cartas disponíveis, quem está ganhando)
- **Monument** → Informações de cada monumento

### **2. TELAS (Screens)** 🖼️
*"As páginas do aplicativo"*

Cada tela é como uma **página de um livro**. Quando você toca num botão, o Flutter "vira a página".

**Telas que criaremos:**

🏠 **MainMenuScreen** (Menu Principal)
- O que aparece: Logo, botões (Jogar, Coleção, Configurações)
- O que faz: Quando toca em "Jogar", abre a tela de escolha de dificuldade

🎮 **GameScreen** (Tela Principal do Jogo)
- O que aparece: Pirâmide de cartas, área do jogador, área da IA, contadores
- O que faz: Detecta toques nas cartas, atualiza o jogo a cada jogada

📚 **CollectionScreen** (Galeria de Cartas)
- O que aparece: Grid com miniaturas das 60 cartas
- O que faz: Mostra detalhes quando toca numa carta

🏆 **VictoryScreen** (Tela de Vitória/Derrota)
- O que aparece: Resultado da partida, estatísticas
- O que faz: Botão para jogar de novo

### **3. COMPONENTES VISUAIS (Widgets)** 🧩
*"Peças reutilizáveis que aparecem em várias telas"*

Pense neles como **carimbos**: você cria uma vez e usa várias vezes.

**CardWidget** (Componente de Carta)
- Recebe as informações da carta
- Desenha a moldura certa
- Coloca a imagem central
- Mostra ícones de custo
- Adiciona brilho quando você pode jogar
- Anima quando você toca (vira, aumenta)

**PyramidLayout** (Pirâmide de Cartas)
- Organiza 20 cartas em formato de pirâmide
- Detecta quais cartas estão "soltas" (clicáveis)
- Vira cartas automaticamente quando outras são removidas

**ResourceCounter** (Contador de Recursos)
- Mostra os 5 ícones elementais
- Mostra quantos você tem de cada (ex: 🌳 x3)
- Anima quando ganha/perde recursos

**MilitaryTrack** (Barrinha Militar)
- Desenha uma barra horizontal
- Marca sua posição e da IA
- Anima quando alguém ganha poder militar

### **4. LÓGICA DO JOGO (Services/Engine)** 🧠
*"O cérebro que faz tudo funcionar"*

Aqui é onde a **mágica acontece**. É o código que implementa as regras do `docs/gameplay/regras.md`.

**GameEngine** (Motor do Jogo)
- **Função: iniciarJogo()**
  - Embaralha as 20 cartas da Era I
  - Monta a pirâmide
  - Define quem joga primeiro
  
- **Função: podePegarCarta(carta, jogador)**
  - Verifica se a carta está solta na pirâmide
  - Verifica se o jogador tem recursos suficientes
  - Verifica se tem corrente (carta grátis)
  - Retorna: SIM ou NÃO

- **Função: jogarCarta(carta, jogador)**
  - Remove carta da pirâmide
  - Adiciona na área do jogador
  - Aplica o efeito da carta (ganhar recurso, pontos, etc.)
  - Verifica condições de vitória
  - Libera novas cartas na pirâmide
  - Passa o turno

- **Função: verificarVitoria()**
  - Checa se alguém ganhou por militar
  - Checa se alguém ganhou por ciência
  - Checa se alguém ganhou por monumentos
  - Se acabaram as cartas, conta pontos finais

**AIService** (Inteligência Artificial)
- **Nível Aprendiz**: Escolhe cartas aleatórias entre as disponíveis
- **Nível Veterano**: Avalia cada carta com uma "nota" (quanto ela ajuda) e pega a melhor
- **Nível Mestre**: Simula 2 turnos à frente para ver consequências
- **Nível Lendário**: Analisa todas as possibilidades e escolhe a jogada ótima (também bloqueia o jogador)

**CardService** (Gerenciador de Cartas)
- Carrega as 60 cartas do jogo
- Embaralha e distribui cartas
- Gerencia correntes (conexões entre cartas)

### **5. DADOS ESTÁTICOS (Data)** 📊
*"O banco de dados do jogo"*

Aqui ficam todas as **60 cartas** do jogo definidas em código.

```
cards_era_i.dart:
- Lista com as 20 cartas da Era I
- Cada carta tem: nome, custo, efeito, pontos, imagem, corrente

cards_era_ii.dart:
- Lista com as 20 cartas da Era II

cards_era_iii.dart:
- Lista com as 20 cartas da Era III

monuments.dart:
- Lista com os 20 monumentos
```

Baseado na documentação de `docs/cartas/era-I-cartas.md`, transformamos cada descrição em código.

---

## 🔄 FLUXO DE UMA JOGADA (Passo a Passo Técnico)

Vamos seguir o que acontece quando você **toca numa carta**:

### **1. TOQUE NA TELA** 👆
- Flutter detecta que você tocou na posição X, Y da tela
- O **CardWidget** daquela carta recebe o evento de toque

### **2. VALIDAÇÃO** ✅
- O **GameEngine** verifica:
  - A carta está solta? (sem outras em cima)
  - É meu turno?
  - Tenho recursos para pagar?
  - Tenho corrente com essa carta?

### **3. SE VÁLIDO: ANIMAÇÃO** 🎬
- A carta **aumenta de tamanho** (animação de 0.3 segundos)
- Se tem recursos suficientes: borda fica **verde**
- Se não tem: borda fica **vermelha** e não deixa pegar

### **4. SE TOCA DE NOVO: JOGAR** 🃏
- Carta sai da pirâmide (animação de "voar" até sua área)
- **GameEngine.jogarCarta()** é chamado
- Recursos são deduzidos (ícones animam diminuindo)
- Efeito da carta é aplicado (ganhar recurso, pontos, etc.)

### **5. VERIFICAR VITÓRIA** 🏆
- **GameEngine.verificarVitoria()** roda
- Se alguém ganhou: abre **VictoryScreen**
- Se não: continua o jogo

### **6. TURNO DA IA** 🤖
- **AIService.escolherJogada()** é chamado
- IA analisa cartas disponíveis (segundo dificuldade)
- Escolhe uma carta
- Animação mostra a IA pegando a carta
- Mesmas verificações acontecem

### **7. ATUALIZAR INTERFACE** 🔄
- Flutter **redesenha** automaticamente:
  - Pirâmide (sem a carta jogada)
  - Contadores de recursos
  - Área de cartas jogadas
  - Barrinha militar (se mudou)

### **8. PRÓXIMO TURNO** ♻️
- Volta pro passo 1 (espera você tocar outra carta)

---

## 📲 COMO FLUTTER VIRA UM APK ANDROID

### **O que é um APK?**
É o "instalador" do Android. Como um arquivo .exe do Windows, mas para celular.

### **Processo de Transformação:**

**1. VOCÊ ESCREVE CÓDIGO** ✍️
- Código em **Dart** (linguagem do Flutter)
- Organizado em arquivos `.dart`
- Ex: `card.dart`, `game_screen.dart`, etc.

**2. FLUTTER COMPILA** 🔧
- Você roda o comando: `flutter build apk`
- Flutter pega todo seu código
- Otimiza (deixa mais rápido e menor)
- Junta com as imagens do `assets/`
- Transforma em linguagem que o Android entende

**3. GERA O APK** 📦
- Arquivo `app-release.apk` é criado
- Tamanho aproximado: 30-50 MB
- Pronto para instalar em qualquer Android

**4. INSTALAÇÃO NO CELULAR** 📱
- Você transfere o APK pro celular
- Instala (como instalar qualquer app)
- Ícone aparece na tela inicial
- Toca no ícone: jogo abre!

### **Desenvolvimento x Produção**

Durante desenvolvimento:
- Você testa no **emulador** (celular virtual no PC)
- Ou conecta seu celular via USB
- Mudanças no código aparecem **instantaneamente** (Hot Reload)
- Você vê erros e conserta rapidinho

Para publicar:
- Gera APK final otimizado
- Assina digitalmente (Google exige)
- Envia para Google Play Store
- Pessoas baixam e instalam normalmente

---

## 🧪 COMO TESTAR SE ESTÁ FUNCIONANDO

### **Testes Unitários** (Partes Isoladas)
Testamos cada função separadamente:

```
Teste: "Jogador pode pegar carta grátis por corrente?"
- Jogador tem carta "Bosque Sussurrante" 
- Carta "Floresta Viva" está disponível
- Chamar: podePegarCarta("Floresta Viva", jogador)
- Resultado esperado: TRUE (pode pegar de graça)
```

### **Testes de Interface** (Tocar na tela)
Simulamos toques na tela:

```
Teste: "Tocar numa carta disponível a pega?"
- Simular toque na carta "Pedreira das Profundezas"
- Verificar se carta foi para área do jogador
- Verificar se recursos foram atualizados
- Verificar se é turno da IA agora
```

### **Testes de IA** (Comportamento)
Verificamos se IA está jogando bem:

```
Teste: "IA Veterano escolhe carta útil?"
- Dar 10 opções de cartas para a IA
- Uma delas dá pontos, outras não
- IA deve escolher a que dá pontos
```

### **Teste Manual** (Você jogando)
O mais importante! Você joga várias partidas e verifica:
- Animações ficaram bonitas?
- Está fácil entender o que fazer?
- IA está desafiadora mas justa?
- Tem algum bug (carta não aparece, jogo trava)?

---

## 🎨 COMO AS IMAGENS ENTRAM NO JOGO

### **1. PREPARAR ASSETS** 🖼️
Você cria/gera as imagens e coloca em `assets/`:

```
assets/
├── cards/
│   ├── bosque_sussurrante.png    (carta completa)
│   ├── pomar_mistico.png
│   └── ... (58 outras cartas)
├── icons/
│   ├── nature.png                (ícone 🌳)
│   ├── earth.png                 (ícone 🗻)
│   └── ... (outros elementos)
└── ui/
    ├── button_play.png
    └── background_menu.png
```

### **2. REGISTRAR NO PUBSPEC.YAML** 📋
Você diz pro Flutter onde estão as imagens:

```
assets:
  - assets/cards/
  - assets/icons/
  - assets/ui/
```

### **3. USAR NO CÓDIGO** 💻
Quando quer mostrar uma carta:

```
Image.asset('assets/cards/bosque_sussurrante.png')
```

Flutter automaticamente:
- Carrega a imagem da pasta
- Redimensiona pro tamanho certo
- Mostra na tela

### **4. OTIMIZAÇÃO** ⚡
Flutter compila as imagens junto no APK:
- Comprime automaticamente
- Carrega só quando necessário (não carrega 60 cartas de uma vez)
- Usa cache (imagem já usada não recarrega)

---

## 📂 ORGANIZAÇÃO DO PROJETO

```
ELEMENTAL NEXUS/
│
├── 📁 docs/           → Toda documentação do jogo (regras, cartas, design)
├── 📁 game/           → Código do jogo em Flutter (será criado)
├── 📁 assets/         → Imagens finalizadas prontas pro jogo
└── 📁 raw-assets/     → Trabalho em progresso (artes sendo criadas)
```

---

## 🎯 FASES DE PROGRAMAÇÃO (Detalhado)

### **FASE 1: Setup Inicial** (1 semana)
**O que é:** Preparar o ambiente de trabalho

- Instalar Flutter SDK no computador
- Criar projeto novo: `flutter create elemental_nexus`
- Configurar estrutura de pastas (`lib/models/`, `lib/screens/`, etc.)
- Adicionar imagens no `assets/`
- Fazer primeiro teste: app vazio abrindo no emulador

**Resultado:** App em branco abre no celular, mostrando "Hello World"

---

### **FASE 2: Modelos de Dados** (1 semana)
**O que é:** Criar as "fichas" de Card, Player, GameState

- Criar `card.dart` → Define o que é uma carta
- Criar `player.dart` → Define jogador (recursos, cartas, pontos)
- Criar `game_state.dart` → Estado completo do jogo
- Criar `cards_era_i.dart` → Lista das 20 cartas da Era I (baseado em `docs/cartas/era-I-cartas.md`)
- Testar: Criar uma carta no código e imprimir seus dados

**Resultado:** Consegue criar objetos Card, Player no código

---

### **FASE 3: Tela do Menu** (1 semana)
**O que é:** Primeira tela visual do jogo

- Criar `main_menu_screen.dart`
- Adicionar logo do jogo
- Adicionar botões: Jogar, Coleção, Sair
- Fazer botões funcionarem (mudar de tela)
- Polir visual (cores, fontes, layout)

**Resultado:** Menu inicial funcional e bonito

---

### **FASE 4: Componente de Carta** (1 semana)
**O que é:** Como uma carta aparece na tela

- Criar `card_widget.dart`
- Exibir imagem da carta
- Detectar toques na carta
- Adicionar animação de "virar" carta
- Testar: Mostrar várias cartas na tela

**Resultado:** Cartas aparecem bonitas e reagem a toques

---

### **FASE 5: Motor do Jogo Básico** (2 semanas)
**O que é:** Implementar regras fundamentais

- Criar `game_engine.dart`
- Implementar `iniciarJogo()` → Embaralhar e montar pirâmide
- Implementar `podePegarCarta()` → Validar jogadas
- Implementar `jogarCarta()` → Executar jogada
- Implementar sistema de recursos (ganhar/gastar)
- Testar: Conseguir jogar cartas e ver recursos mudando

**Resultado:** Lógica básica funciona (sem IA ainda)

---

### **FASE 6: Tela de Jogo** (2 semanas)
**O que é:** Onde o jogo acontece

- Criar `game_screen.dart`
- Criar `pyramid_layout.dart` → Desenhar pirâmide
- Criar `resource_counter.dart` → Mostrar recursos
- Conectar tudo com GameEngine
- Permitir pegar cartas da pirâmide
- Mostrar cartas jogadas do jogador

**Resultado:** Pode jogar contra "ninguém" (sem IA)

---

### **FASE 7: Inteligência Artificial** (2 semanas)
**O que é:** O oponente que joga contra você

- Criar `ai_service.dart`
- Implementar IA Aprendiz (aleatória inteligente)
- Implementar IA Veterano (avaliação simples)
- Implementar IA Mestre (simulação 2 turnos)
- Implementar IA Lendário (minimax completo)
- Testar: Jogar contra cada nível e ver diferença

**Resultado:** 4 níveis de IA funcionais

---

### **FASE 8: Condições de Vitória** (1 semana)
**O que é:** Detectar quando o jogo acabou

- Implementar vitória militar
- Implementar vitória científica  
- Implementar vitória por monumentos
- Implementar vitória por pontos
- Criar `victory_screen.dart` → Tela de resultado
- Testar: Forçar cada tipo de vitória e verificar

**Resultado:** Jogo termina corretamente e mostra vencedor

---

### **FASE 9: Era II e III** (1 semana)
**O que é:** Adicionar cartas das outras eras

- Criar `cards_era_ii.dart` e `cards_era_iii.dart`
- Implementar transição entre eras
- Adaptar pirâmide para cartas diferentes
- Testar: Jogar partida completa das 3 eras

**Resultado:** Jogo completo com 60 cartas

---

### **FASE 10: Sistema de Correntes** (1 semana)
**O que é:** Cartas grátis por conexão

- Implementar detecção de correntes
- Modificar `podePegarCarta()` para considerar correntes
- Adicionar indicador visual (brilho verde em cartas grátis)
- Testar: Verificar todas as 10 correntes documentadas

**Resultado:** Sistema de correntes funcional

---

### **FASE 11: Monumentos** (1 semana)
**O que é:** Construções especiais

- Criar `monument.dart`
- Criar `monuments.dart` → Lista dos 20 monumentos
- Implementar escolha de monumento durante jogo
- Implementar efeitos dos monumentos
- Testar: Construir cada monumento e verificar efeito

**Resultado:** Sistema de monumentos completo

---

### **FASE 12: Polimento Visual** (2 semanas)
**O que é:** Deixar tudo bonito e suave

- Adicionar animações (cartas voando, recursos brilhando)
- Melhorar transições entre telas
- Adicionar partículas visuais (sparkles, fumaça)
- Ajustar cores e contrastes
- Adicionar feedback tátil (vibração)

**Resultado:** Jogo fluido e visualmente impressionante

---

### **FASE 13: Testes e Bugs** (1 semana)
**O que é:** Encontrar e corrigir problemas

- Jogar 50+ partidas em todos os níveis
- Testar todas as cartas
- Testar todos os monumentos
- Corrigir bugs encontrados
- Ajustar balanceamento (se alguma carta muito forte)

**Resultado:** Jogo estável e balanceado

---

### **FASE 14: Preparação para Lançamento** (1 semana)
**O que é:** Preparar para publicar

- Criar ícone do app
- Criar screenshots para a loja
- Escrever descrição da Google Play
- Compilar APK final otimizado
- Assinar digitalmente o APK
- Criar conta de desenvolvedor Google Play ($25)

**Resultado:** Pronto para publicar!

---

## ⏱️ CRONOGRAMA RESUMIDO

| Fase | Duração | Total Acumulado |
|------|---------|-----------------|
| 1-3: Setup + Menu | 3 semanas | 3 semanas |
| 4-6: Cartas + Engine + Tela | 5 semanas | 8 semanas |
| 7-9: IA + Vitória + Eras | 4 semanas | 12 semanas |
| 10-12: Correntes + Monumentos + Polish | 4 semanas | 16 semanas |
| 13-14: Testes + Lançamento | 2 semanas | **18 semanas** |

**Total: ~4-5 meses** trabalhando 10-15h por semana

---

## 🛠️ FERRAMENTAS E TECNOLOGIAS

### **Desenvolvimento**
- **Flutter SDK** - Framework para criar o app
- **Dart** - Linguagem de programação
- **Android Studio** - IDE e emulador Android
- **VS Code** - Editor de código leve
- **Git** - Controle de versão

### **Arte**
- **Leonardo.ai / Gemini** - Geração de arte com IA
- **Photoshop / Figma** - Montagem final das cartas
- **GIMP** - Alternativa gratuita ao Photoshop

### **Testes**
- **Flutter Test** - Testes unitários
- **Firebase Test Lab** - Testes em vários dispositivos (opcional)

### **Publicação**
- **Google Play Console** - Upload e gerenciamento do app

---

## � CONCEITOS-CHAVE PARA ENTENDER

### **1. Estado (State)**
É como a "memória" do jogo no momento atual.

Exemplo de estado:
- Turno 5
- Jogador tem 3🌳, 2🗻, 1💧
- 12 cartas na pirâmide
- 5 cartas jogadas pelo jogador
- 4 cartas jogadas pela IA
- Barrinha militar em +2 para o jogador

Quando algo muda (jogar carta), o estado atualiza e Flutter redesenha a tela.

### **2. Widget Tree (Árvore de Widgets)**
É como tudo está organizado hierarquicamente.

```
GameScreen
├── PlayerArea
│   ├── ResourceCounter
│   └── CardsPlayed
├── PyramidLayout
│   └── CardWidget (x12)
├── OpponentArea
│   ├── ResourceCounter
│   └── CardsPlayed
└── MilitaryTrack
```

Quando algo muda na árvore, Flutter atualiza só aquela parte (eficiente!).

### **3. Async/Await (Código Assíncrono)**
Para coisas que demoram (IA pensando, animações).

Exemplo:
- Você joga uma carta → animação 0.5s
- Enquanto anima, Flutter não trava (app responde)
- Quando termina animação → IA joga
- IA pensa 1s → animação da jogada dela

Tudo acontece de forma fluida sem travar o app.

### **4. Hot Reload (Recarga Rápida)**
Magia do Flutter!

- Você muda a cor de um botão no código
- Aperta `Ctrl+S` para salvar
- **2 segundos depois**, a mudança aparece no emulador
- Sem precisar recompilar tudo (economiza horas!)

---

## 📊 DESAFIOS TÉCNICOS E SOLUÇÕES

### **Desafio 1: Organizar Pirâmide**
**Problema:** Como posicionar 20 cartas em formato de pirâmide?

**Solução:** Usar coordenadas matemáticas:
- Linha 1: 1 carta no topo (X: centro)
- Linha 2: 2 cartas (X: centro-50, centro+50)
- Linha 3: 3 cartas (X: centro-100, centro, centro+100)
- ...e assim por diante

### **Desafio 2: IA Não Muito Burra, Não Muito Forte**
**Problema:** IA aleatória é chata, IA perfeita é impossível de vencer

**Solução:** 4 níveis com complexidade crescente:
- Aprendiz: 70% aleatório + 30% estratégia básica
- Veterano: Avalia cada carta com pontuação
- Mestre: Simula 2 turnos à frente
- Lendário: Minimax (algoritmo de xadrez adaptado)

### **Desafio 3: Performance (60 Imagens Pesadas)**
**Problema:** Carregar 60 cartas de alta resolução trava o app

**Solução:**
- Carregar apenas cartas visíveis (lazy loading)
- Comprimir imagens (PNG → otimizado)
- Usar cache (carta já mostrada não recarrega)
- Thumbnail pequeno na galeria, imagem grande só quando clicar

### **Desafio 4: Detectar Vitória em Tempo Real**
**Problema:** Verificar condições de vitória a cada jogada pode ser lento

**Solução:**
- Criar "gatilhos" específicos:
  - Militar: Verifica só quando alguém ganha poder militar
  - Científica: Verifica só quando alguém joga carta de ciência
  - Monumentos: Verifica só quando alguém constrói monumento
  - Pontos: Só no final da Era III

---

## 📁 ESTRUTURA DE ARQUIVOS (O Que Vai em Cada Pasta)

```
game/
└── lib/
    ├── main.dart                    ← Ponto de entrada (abre o app)
    │
    ├── models/                      ← "Fichas técnicas" dos objetos
    │   ├── card.dart                   (O que é uma carta)
    │   ├── player.dart                 (O que é um jogador)
    │   ├── game_state.dart             (Estado completo do jogo)
    │   └── monument.dart               (O que é um monumento)
    │
    ├── data/                        ← Banco de dados das cartas
    │   ├── cards_era_i.dart            (20 cartas da Era I)
    │   ├── cards_era_ii.dart           (20 cartas da Era II)
    │   ├── cards_era_iii.dart          (20 cartas da Era III)
    │   └── monuments.dart              (20 monumentos)
    │
    ├── services/                    ← Lógica/regras do jogo
    │   ├── game_engine.dart            (Motor do jogo)
    │   ├── ai_service.dart             (Inteligência artificial)
    │   └── card_service.dart           (Gerenciar cartas)
    │
    ├── screens/                     ← Telas completas
    │   ├── main_menu_screen.dart       (Menu inicial)
    │   ├── game_screen.dart            (Tela de jogo)
    │   ├── collection_screen.dart      (Galeria de cartas)
    │   ├── victory_screen.dart         (Tela de vitória)
    │   └── settings_screen.dart        (Configurações)
    │
    ├── widgets/                     ← Componentes reutilizáveis
    │   ├── card_widget.dart            (Carta visual)
    │   ├── pyramid_layout.dart         (Pirâmide)
    │   ├── resource_counter.dart       (Contador de recursos)
    │   ├── military_track.dart         (Barrinha militar)
    │   └── custom_button.dart          (Botão customizado)
    │
    └── utils/                       ← Utilitários
        ├── constants.dart              (Cores, tamanhos, configurações)
        └── helpers.dart                (Funções auxiliares)
```

---

## � O QUE VOCÊ APRENDE FAZENDO ESTE PROJETO

✅ **Flutter/Dart** - Framework mobile moderno  
✅ **Gerenciamento de Estado** - Como apps mantêm informações  
✅ **Lógica de Jogo** - Implementar regras complexas  
✅ **Algoritmos de IA** - Minimax, heurísticas  
✅ **UI/UX Design** - Criar interfaces intuitivas  
✅ **Animações** - Movimento e feedback visual  
✅ **Otimização** - Performance em dispositivos móveis  
✅ **Publicação de Apps** - Processo completo até a loja  

---

## � PRÓXIMOS PASSOS

1. ✅ Documentação completa (docs/)
2. 🔄 Gerar assets visuais (raw-assets/)
3. ⏳ Montar cartas finais (assets/)
4. ⏳ Começar programação (game/)
5. ⏳ Testes e ajustes
6. ⏳ Publicar na Google Play

---

**Versão Atual**: 0.1.0 - Fase de Design  
**Próxima Meta**: Gerar 60 artes de cartas  
**Início da Programação**: Após assets prontos  

🎴 **Que os Elementos estejam com você!** ✨
