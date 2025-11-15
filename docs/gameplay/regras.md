# Regras do Jogo - ELEMENTAL NEXUS

## 🎯 Objetivo

Seja o primeiro a alcançar uma das **4 formas de vitória** ou tenha a maior pontuação ao final da Era III.

## 🎲 Componentes do Jogo

### Cartas
- **60 cartas** divididas em 3 Eras (20 cartas por Era)
- **5 tipos de carta** + 1 especial (Artefatos)

### Monumentos
- **Pool de monumentos disponíveis** (varia conforme desbloqueio)
- Cada jogador escolhe **3 monumentos** antes da partida
- Pode construir **2-3 monumentos** durante o jogo

### Trilha Militar
- **15 espaços** (-7 a +7, com 0 no centro)
- Marcador neutro começa no centro
- Move conforme diferença de poder militar

### Tabuleiro Virtual
- Área de cartas em pirâmide
- Área de construção de cada jogador
- Indicadores de recursos, essência, pontos

## 🚀 Preparação da Partida

### 1. Seleção de Monumentos
1. O jogo sorteia **6 monumentos** do pool desbloqueado
2. Jogador escolhe **3 monumentos** primeiro
3. IA escolhe **3 monumentos** dos restantes
4. Ambos começam com 0 monumentos construídos

### 2. Configuração Inicial
- Cada jogador começa com **7 Essência** (moeda)
- Marcador militar no centro (posição 0)
- Embaralhar cartas de cada Era separadamente

### 3. Montagem da Pirâmide (Era I)
As 20 cartas da Era I são dispostas em pirâmide:

```
        [?]                    <- Topo (1 carta virada para baixo)
       [?] [?]                 <- (2 cartas viradas para baixo)
      [C] [?] [C]              <- (3 cartas: 2 viradas para cima, 1 para baixo)
     [C] [C] [C] [C]           <- (4 cartas viradas para cima)
    [C] [?] [C] [?] [C]        <- (5 cartas: 3 viradas para cima, 2 para baixo)
   [C] [C] [C] [C] [C] [C]     <- Base (6 cartas viradas para cima)
```

**Legenda:**
- `[C]` = Carta visível (virada para cima)
- `[?]` = Carta oculta (virada para baixo)

**Regra:** Cartas viradas para baixo são reveladas automaticamente quando ficam "livres" (sem cartas sobre elas).

## 🎮 Mecânica de Jogo

### Estrutura de Uma Era

1. **Turnos Alternados**: Jogador → IA → Jogador → IA...
2. **Cartas Livres**: Só pode pegar cartas que não têm outras cartas sobre elas
3. **Fim da Era**: Quando todas as 20 cartas forem adquiridas ou descartadas
4. **Próxima Era**: Monta nova pirâmide com cartas da próxima Era

### Ações Possíveis no Turno

Cada turno, você deve escolher **UMA** das seguintes ações:

#### 1. 🏗️ Construir Carta
- Pegue uma carta livre da pirâmide
- Pague o **custo em recursos** indicado
- A carta vai para sua área de jogo
- Seus recursos são **permanentes** (não se gastam, apenas devem existir)

**Exemplo:**
- Carta custa: 2 Natureza + 1 Terra
- Você precisa ter cartas que produzem 2 Natureza e 1 Terra
- Após construir, você continua tendo esses recursos

**Custo em Essência:**
- Se não tiver os recursos exatos, pode **comprar do oponente**
- Custo: **2 Essência + 1 por recurso do tipo que o oponente produz**
- Exemplo: Precisa de 1 Fogo, oponente tem 2 cartas de Fogo → Custa 2 + 2 = 4 Essência

#### 2. 💰 Descartar por Essência
- Pegue uma carta livre da pirâmide
- Descarte-a (vai para pilha de descarte)
- Ganhe **2 Essência + 1 por carta amarela (Mercado) que você possui**
- Útil para negar cartas ao oponente ou acumular Essência

#### 3. 🏛️ Construir Monumento
- Escolha um dos seus 3 monumentos ainda não construídos
- Pague o **custo em recursos** do monumento
- Coloque-o na sua área de jogo
- Seu efeito ativa imediatamente e permanece ativo
- **Atenção:** Construir monumento **não** usa uma carta da pirâmide

**Vitória Especial:**
- Se você construir seu **3º monumento** antes do fim da Era III = **Vitória por Monumentos!**

### ⛓️ Sistema de Chains (Correntes)

Algumas cartas têm um símbolo de **Chain** (corrente):

**Como funciona:**
- Se você construiu a carta "A" na Era I
- E a carta "B" na Era II tem chain ligado à carta "A"
- Você pode construir a carta "B" **gratuitamente** (sem pagar recursos)

**Exemplo:**
- **Bosque Sussurrante** (Era I) → Chain para → **Jardim Selvagem** (Era II)
- Se você construiu Bosque Sussurrante, pode construir Jardim Selvagem de graça

**Bloqueio:**
- Se o oponente pegar a carta de destino do chain, você perde a oportunidade
- Draft strategy importante: pegar cartas para negar chains do oponente

## ⚔️ Sistema Militar

### Trilha Militar
- **15 posições**: -7, -6, -5, -4, -3, -2, -1, **0**, +1, +2, +3, +4, +5, +6, +7
- Marcador começa em **0** (centro)
- Move conforme a **diferença de poder militar** entre jogadores

### Cálculo de Movimento
Ao final de cada turno onde uma carta militar foi jogada:

1. **Some os Escudos** de todas suas cartas militares (Legiões)
2. **Compare com o oponente**
3. **Mova o marcador** na direção do jogador mais forte

**Exemplo:**
- Você: 5 escudos
- Oponente: 2 escudos
- Diferença: 3 a seu favor → Marcador em +3

### Checkpoints Militares

| Posição | Efeito |
|---------|--------|
| **±3** | Jogador dominante escolhe: +2 Essência OU Roubar 1 Essência do oponente |
| **±6** | Jogador dominante ganha +3 Essência E oponente perde 2 Essência |
| **±8** | **VITÓRIA MILITAR IMEDIATA** |

**Atenção:** Checkpoints ativam **uma única vez** quando o marcador cruza pela primeira vez.

### Defesas Especiais
Algumas cartas/monumentos podem:
- Impedir derrota militar temporariamente
- Dar escudos extras sob condições
- Mover o marcador como "Sabotagem" (sem escudos)

## 🔬 Sistema Científico (Grimórios)

### Os 4 Símbolos Arcanos

| Símbolo | Nome | Representa |
|---------|------|------------|
| 🔮 | **Místico** | Cristais, magia intuitiva |
| ⚗️ | **Alquimia** | Transmutação, experimentos |
| 📜 | **Conhecimento** | Textos antigos, sabedoria |
| 🌟 | **Iluminação** | Insight divino, revelação |

### Formas de Vitória Científica

Alcance **qualquer uma** destas condições:

1. **6 símbolos quaisquer** (pode repetir)
   - Exemplo: 🔮🔮⚗️⚗️📜🌟 = Vitória!

2. **3 pares de símbolos iguais**
   - Exemplo: 🔮🔮 + ⚗️⚗️ + 📜📜 = Vitória!

3. **Enciclopédia Arcana** (carta especial Era III)
   - Se construir esta carta E já tiver 2+ símbolos diferentes = Vitória imediata!

**Estratégia:**
- Cartas de Grimório são escassas (6 cartas no jogo total)
- Vitória científica requer foco total
- Oponente pode bloquear pegando cartas científicas

## 📊 Sistema de Pontuação

### Fontes de Pontos

1. **Cartas de Estrutura** (azul claro)
   - Pontos fixos indicados na carta
   - Variam de 2 a 13 pontos

2. **Cartas de Legião** (vermelho)
   - Algumas dão pontos além de escudos
   - Geralmente 1-3 pontos

3. **Cartas de Mercado** (amarelo)
   - Algumas dão 1-4 pontos
   - Maioria foca em efeitos econômicos

4. **Cartas de Grimório** (roxo)
   - Geralmente 1-4 pontos
   - Podem ter bônus de efeitos especiais

5. **Monumentos**
   - Pontos base (3-8 pontos)
   - Alguns têm efeitos multiplicadores

6. **Artefatos Ancestrais** (Era III)
   - Pontos base + bônus condicional
   - Exemplo: "5 pontos + 1 por Legião"

7. **Essência Residual**
   - 1 ponto a cada **3 Essência** restante

8. **Penalidades Militares** (se perdeu checkpoints)
   - Pode ter perdido pontos/essência durante o jogo

### Cálculo Final (Se ninguém venceu antes)

```
PONTOS TOTAIS = 
  + Pontos de Cartas
  + Pontos de Monumentos (base)
  + Bônus de Monumentos (multiplicadores)
  + Pontos de Artefatos (base)
  + Bônus de Artefatos (multiplicadores)
  + Essência Residual ÷ 3 (arredondado para baixo)
```

**Exemplo:**
```
Cartas de Estrutura: 45 pontos
Cartas de Legião: 8 pontos
Cartas de Grimório: 12 pontos
Monumento A: 6 pontos
Monumento B: 5 pontos + (2 por Legião) = 5 + 8 = 13 pontos
Artefato: 5 pontos + (1 por símbolo científico) = 5 + 4 = 9 pontos
Essência residual: 8 Essência ÷ 3 = 2 pontos

TOTAL: 45 + 8 + 12 + 6 + 13 + 9 + 2 = 95 pontos
```

## 🏆 Condições de Vitória (Detalhadas)

### 1. ⚔️ Vitória Militar
- **Condição:** Marcador militar alcança **±8**
- **Quando verifica:** Imediatamente após movimento militar
- **Vitória:** Instantânea, jogo termina
- **Defesas:** Algumas cartas impedem esta vitória temporariamente

### 2. 🔬 Vitória Científica
- **Condição:** Coletar símbolos suficientes (ver seção Sistema Científico)
- **Quando verifica:** Imediatamente após construir carta de Grimório
- **Vitória:** Instantânea, jogo termina
- **Dificuldade:** Requer foco e sorte no draft

### 3. 🏛️ Vitória por Monumentos ⭐ NOVA
- **Condição:** Construir **todos os 3 monumentos** escolhidos
- **Quando verifica:** Ao terminar construção do 3º monumento
- **Vitória:** Instantânea, se ocorrer antes do fim da Era III
- **Estratégia:** Requer economia forte e sacrifícios

### 4. 📊 Vitória por Pontos
- **Condição:** Maior pontuação ao final da Era III
- **Quando verifica:** Após processar a última carta da Era III
- **Vitória:** Por comparação, pode empatar (desempate: mais Essência)
- **Comum:** A forma mais comum de vitória

## 🔄 Fluxo de Uma Partida Completa

```
INÍCIO
  ↓
Seleção de Monumentos (cada jogador escolhe 3)
  ↓
Distribuição inicial: 7 Essência cada
  ↓
┌─────────────────────────────────────┐
│ ERA I - FUNDAÇÃO (20 cartas)        │
│  - Monta pirâmide Era I             │
│  - Turnos alternados                │
│  - Verificação de vitórias a cada   │
│    carta militar/científica         │
│  - Checkpoints militares ativam     │
└─────────────────────────────────────┘
  ↓
┌─────────────────────────────────────┐
│ ERA II - EXPANSÃO (20 cartas)       │
│  - Monta pirâmide Era II            │
│  - Chains começam a ativar          │
│  - Jogadores têm mais recursos      │
│  - Pressão militar aumenta          │
└─────────────────────────────────────┘
  ↓
┌─────────────────────────────────────┐
│ ERA III - APOGEU (20 cartas)        │
│  - Monta pirâmide Era III           │
│  - Artefatos Ancestrais aparecem    │
│  - Corrida final pelas vitórias     │
│  - Última chance de virar o jogo    │
└─────────────────────────────────────┘
  ↓
Fim da Era III
  ↓
Verificação de Vitórias Alternativas
  ↓
Se nenhuma: Contagem de Pontos
  ↓
VENCEDOR DECLARADO
  ↓
Tela de Resultados
  - XP ganho
  - Conquistas desbloqueadas
  - Novo monumento desbloqueado (se aplicável)
```

## ⚠️ Regras Especiais e Exceções

### Compra de Recursos
- **Custo base:** 2 Essência por recurso
- **Penalidade:** +1 Essência para cada carta **do mesmo tipo** que o oponente possui
- **Exemplo:** Precisa de 1 Fogo, oponente tem 3 cartas de Fogo → Custa 2 + 3 = 5 Essência

### Cartas Grátis
1. Via **Chain** (corrente da Era anterior)
2. Via **Efeito especial** de alguma carta/monumento
3. **Primeira carta** de alguns monumentos

### Construir Monumento
- **Não gasta** uma carta da pirâmide
- Pode ser feito **a qualquer momento** no seu turno
- Conta como sua ação do turno (não pode construir carta no mesmo turno)

### Empate
- Se pontos finais forem iguais:
  1. **Desempate 1:** Quem tem mais Essência restante
  2. **Desempate 2:** Quem tem mais Monumentos construídos
  3. **Desempate 3:** Vitória da IA (para evitar exploits)

### Cartas com Efeitos Imediatos
Algumas cartas têm efeitos que ativam **ao serem construídas**:
- "Ao construir, ganhe +5 Essência"
- "Ao construir, roube 1 recurso do oponente"
- "Ao construir, mova o marcador militar 2 casas a seu favor"

Esses efeitos resolvem imediatamente antes do próximo turno.

### Ordem de Resolução
Quando múltiplos efeitos acontecem simultaneamente:

1. Efeitos da carta construída
2. Atualização de recursos permanentes
3. Recálculo de poder militar (se aplicável)
4. Verificação de vitórias alternativas
5. Passa o turno

## 📚 Glossário de Termos

- **Chain (Corrente):** Conexão entre cartas de Eras diferentes que permite construção gratuita
- **Draft:** Processo de escolher cartas da pirâmide
- **Essência:** Moeda do jogo, usada para comprar recursos ou pagar custos
- **Escudo:** Unidade de poder militar
- **Carta Livre:** Carta que não tem outras cartas sobre ela na pirâmide
- **Checkpoint:** Posições especiais na trilha militar que dão bônus
- **Símbolo:** Ícone de Grimório usado para vitória científica
- **Multiplicador:** Efeito que dá pontos baseado em outras cartas
- **Artefato Ancestral:** Tipo especial de carta que só aparece na Era III

---

**Próximo documento:** [Recursos e Elementos](recursos-elementos.md)
