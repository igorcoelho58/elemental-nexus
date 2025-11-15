# Sistema de IA - ELEMENTAL NEXUS

## 🤖 Visão Geral

O jogo possui **4 níveis de dificuldade de IA**, cada um com personalidade e estratégia distintas. A IA deve ser **desafiadora mas justa** - nunca trapaceira.

---

## 🎯 NÍVEL 1 - APRENDIZ

### Descrição
IA passiva e previsível, ideal para tutorial e primeiras partidas.

### Características
- **Personalidade:** Cautelosa, básica
- **Vantagem inicial:** Nenhuma
- **Taxa de bloqueio:** 0% (nunca bloqueia intencionalmente)
- **Planejamento:** 0 turnos à frente (joga no imediato)

### Heurística de Decisão

**Prioridades (em ordem):**
1. Construir cartas **grátis** (custo 0)
2. Construir **Recursos** baratos
3. Construir **Estruturas** que dão mais pontos
4. Construir **Legiões** se tiver recursos sobrando
5. Descartar por Essência se não puder construir nada

**Fórmula de Avaliação:**
```
ValorCarta = Pontos + (Recursos_produzidos × 0.5) + (Escudos × 1)
```

**Construção de Monumentos:**
- Constrói quando tiver recursos exatos + 3 Essência de reserva
- Escolhe o monumento mais barato disponível
- Nunca visa Vitória por Monumentos estrategicamente

### Nível de Ameaça
⭐☆☆☆☆ - Extremamente fácil

### Uso Recomendado
- Tutorial interativo
- Primeiras 3-5 partidas
- Jogadores iniciantes absolutos

---

## 🎯 NÍVEL 2 - VETERANO

### Descrição
IA competente que entende o jogo, mas não é opressiva.

### Características
- **Personalidade:** Equilibrada, adaptável
- **Vantagem inicial:** Nenhuma
- **Taxa de bloqueio:** 30% (às vezes nega cartas importantes)
- **Planejamento:** 1 turno à frente

### Heurística de Decisão

**Prioridades:**
1. **Reconhece chains** - Pega cartas que têm chain para próxima Era
2. **Bloqueio básico** - 30% de chance de pegar carta que o jogador precisa
3. **Balanceia** - Constrói mix de Recursos, Estruturas e Legiões
4. **Economia** - Mantém 5+ Essência de reserva sempre que possível

**Fórmula de Avaliação:**
```
ValorCarta = Pontos + (Recursos × 1.5) + (Escudos × 2) + (Símbolos_científicos × 3)

Se carta tem Chain:
  ValorCarta += 3

Se jogador precisa dessa carta (detecta):
  ValorCarta += 2 (30% de chance de bloquear)
```

**Construção de Monumentos:**
- Constrói monumentos que combinam com sua estratégia atual
- Se está forte em militar → Escolhe monumentos militares
- Nunca tenta Vitória por Monumentos (não é agressiva o suficiente)

**Estratégia:**
- Tenta acumular pontos (vitória por Pontos)
- Defende-se militarmente mas não ataca
- Ignora vitória científica (muito arriscada)

### Nível de Ameaça
⭐⭐☆☆☆ - Fácil/Médio

### Uso Recomendado
- Partidas casuais
- Jogadores que entendem as regras mas não dominam
- Testar novas estratégias sem pressão

---

## 🎯 NÍVEL 3 - MESTRE

### Descrição
IA inteligente que planeja estratégias e bloqueia ativamente o jogador.

### Características
- **Personalidade:** Estratégica, oportunista
- **Vantagem inicial:** Nenhuma
- **Taxa de bloqueio:** 60% (bloqueia frequentemente)
- **Planejamento:** 3 turnos à frente

### Heurística de Decisão

**Prioridades:**
1. **Detecta win conditions** - Se jogador está perto de vitória, bloqueia
   - 5 símbolos científicos → Bloqueia Grimórios
   - Marcador militar em +6 → Constrói defesa/Legiões
   - 2 monumentos construídos → Tenta atrasar 3º monumento

2. **Planejamento multi-turno:**
   - Avalia cartas que estarão livres nos próximos 2-3 turnos
   - Constrói chains propositalmente
   - Guarda Essência para cartas específicas futuras

3. **Adapta estratégia:**
   - Reconhece se jogador está focando em (militar/ciência/pontos)
   - Muda sua estratégia para counter
   - Exemplo: Se jogador foca militar → IA prioriza Estruturas + defesa

**Fórmula de Avaliação:**
```
ValorBase = Pontos + (Recursos × 2) + (Escudos × 3) + (Símbolos × 4)

Modificadores situacionais:
+ Chain para próxima Era: +5
+ Bloqueia win condition do jogador: +10
+ Sinergia com cartas existentes: +3
+ Ativa monumento: +4
+ Carta que falta para chain: +6

Se jogador tem 60% chance de pegar:
  ValorCarta × 1.6 (aumenta urgência)
```

**Construção de Monumentos:**
- Constrói 2-3 monumentos estrategicamente
- Escolhe monumentos sinérgicos com cartas adquiridas
- Considera Vitória por Monumentos se viável (3º monumento)

**Estratégias Múltiplas:**
- **Rush Militar:** Se pega 2+ Legiões cedo → Pressiona militar agressivamente
- **Científica Oportunista:** Se pega 3 Grimórios → Tenta vitória científica
- **Econômica:** Se sem estratégia clara → Acumula pontos
- **Monumentos:** Se economia forte → Vai para 3 monumentos

### Nível de Ameaça
⭐⭐⭐⭐☆ - Difícil

### Uso Recomendado
- Jogadores experientes
- Desafio competitivo
- Treinar habilidades avançadas

---

## 🎯 NÍVEL 4 - LENDÁRIO

### Descrição
IA brutal que usa todas as ferramentas possíveis, incluindo **vantagem inicial** e algoritmo avançado.

### Características
- **Personalidade:** Implacável, predatória
- **Vantagem inicial:** +3 Essência (começa com 10 ao invés de 7)
- **Taxa de bloqueio:** 80-90% (quase sempre bloqueia)
- **Planejamento:** 4-5 turnos à frente (algoritmo MinMax)

### Heurística de Decisão

**Algoritmo MinMax Simplificado:**
```
Para cada carta livre:
  Simula construir essa carta
  Avalia estado do jogo resultante
  Simula próximos 3-4 turnos (alternando jogador/IA)
  Calcula "utilidade" final (quão perto de vitória)
  
Escolhe a carta que maximiza utilidade da IA E minimiza do jogador
```

**Detecção Avançada:**
- **Padrões do jogador:** IA "aprende" tendências
  - Se jogador sempre pega Natureza → IA compete por Natureza
  - Se jogador ignora militar → IA rush militar
- **Leitura de estratégia:**
  - Detecta em 3-4 turnos qual win condition o jogador busca
  - Counter-strategy ativa imediatamente

**Fórmula de Avaliação:**
```
ValorIA = Utilidade de construir para IA
ValorJogador = Utilidade de bloquear jogador

Score_Final = ValorIA + (ValorJogador × 0.8)

Utilidade considera:
- Progressão para vitória (qualquer via)
- Estado militar relativo
- Economia (Essência e recursos)
- Pontos projetados no final
- Ameaça de vitória do oponente
```

**Construção de Monumentos:**
- Planeja monumentos desde seleção inicial
- Escolhe monumentos que combo entre si
- Agressiva em buscar Vitória por Monumentos se viável
- Timing perfeito (constrói 3º monumento no momento ideal)

**Estratégias Especializadas:**

**1. Rush Militar Agressivo:**
- Se detecta fraqueza militar do jogador
- Constrói todas Legiões + monumentos militares
- Força vitória militar na Era II

**2. Lock Científico:**
- Pega TODOS os Grimórios (mesmo sem usar)
- Nega vitória científica completamente ao jogador
- Vence por pontos/militar

**3. Economic Lock:**
- Pega todas cartas de Mercado
- Força jogador a gastar Essência comprando recursos
- Sufoca economicamente

**4. Monumento Rush:**
- Foca em recursos variados
- Constrói monumentos baratos rapidamente
- Vai para vitória por 3 monumentos (Era III)

### Nível de Ameaça
⭐⭐⭐⭐⭐ - Muito Difícil

### Uso Recomendado
- Jogadores veteranos
- Desafio extremo
- Conteúdo "end-game"
- Desbloqueia após vencer IA Mestre 3+ vezes

---

## 🧠 Implementação Técnica

### Estrutura de Código (Dart)

```dart
abstract class AIPlayer {
  AILevel level;
  GameState gameState;
  
  // Método principal de decisão
  Card chooseCard(List<Card> availableCards);
  
  // Avaliação de carta
  double evaluateCard(Card card, GameState state);
  
  // Detectar ameaças
  bool detectThreat(Player opponent);
  
  // Escolher ação (construir/descartar/monumento)
  Action chooseAction();
}

class ApprenticeAI extends AIPlayer {
  @override
  double evaluateCard(Card card, GameState state) {
    return card.points + (card.resources.length * 0.5) + card.shields;
  }
}

class VeteranAI extends AIPlayer {
  @override
  double evaluateCard(Card card, GameState state) {
    double value = card.points 
                 + (card.resources.length * 1.5) 
                 + (card.shields * 2)
                 + (card.symbols.length * 3);
    
    if (card.chain != null) value += 3;
    if (shouldBlock(card)) value += 2;
    
    return value;
  }
  
  bool shouldBlock(Card card) {
    return Random().nextDouble() < 0.3; // 30% chance
  }
}

class MasterAI extends AIPlayer {
  @override
  double evaluateCard(Card card, GameState state) {
    double base = calculateBaseValue(card);
    double situational = calculateSituationalBonus(card, state);
    double blocking = calculateBlockingValue(card, state.opponent);
    
    return base + situational + blocking;
  }
  
  @override
  Card chooseCard(List<Card> availableCards) {
    // Simula 3 turnos à frente
    Map<Card, double> projections = {};
    for (Card card in availableCards) {
      projections[card] = simulateFuture(card, 3);
    }
    return projections.entries.reduce((a, b) => 
      a.value > b.value ? a : b
    ).key;
  }
}

class LegendaryAI extends AIPlayer {
  @override
  Card chooseCard(List<Card> availableCards) {
    // Algoritmo MinMax com poda alfa-beta
    return minimaxDecision(availableCards, depth: 4);
  }
  
  Card minimaxDecision(List<Card> cards, {int depth = 4}) {
    double bestValue = double.negativeInfinity;
    Card bestCard = cards.first;
    
    for (Card card in cards) {
      double value = minValue(
        gameState.applyAction(Action.construct(card)),
        depth - 1,
        double.negativeInfinity,
        double.infinity
      );
      if (value > bestValue) {
        bestValue = value;
        bestCard = card;
      }
    }
    return bestCard;
  }
}
```

### Balanceamento de Tempo

| Nível | Tempo de Resposta | Complexidade Computacional |
|-------|-------------------|----------------------------|
| Aprendiz | Instantâneo (0.1s) | O(n) - Linear |
| Veterano | Rápido (0.3s) | O(n log n) |
| Mestre | Moderado (0.5-1s) | O(n²) - Quadrático |
| Lendário | Pensando (1-2s) | O(n⁴) - MinMax limitado |

**Nota:** Delays artificiais podem ser adicionados para "humanizar" (IA muito rápida parece robótica).

---

## 📊 Estatísticas de Vitória Esperadas

Assumindo jogador mediano:

| Nível IA | Taxa de Vitória do Jogador | Partidas até Dominar |
|----------|----------------------------|----------------------|
| Aprendiz | 90-95% | 2-3 partidas |
| Veterano | 60-70% | 10-15 partidas |
| Mestre | 35-45% | 30-50 partidas |
| Lendário | 15-25% | 100+ partidas |

---

## 🎯 Conquistas Relacionadas à IA

- **"Primeiros Passos"** - Vença o Aprendiz
- **"Veterano de Guerra"** - Vença o Veterano 5 vezes
- **"Mestre do Nexus"** - Vença o Mestre 10 vezes
- **"Lenda Imortal"** - Vença o Lendário 1 vez
- **"Dominador Absoluto"** - Vença o Lendário 10 vezes
- **"Invencível"** - Sequência de 10 vitórias seguidas contra Mestre
- **"Deus do Nexus"** - Vença o Lendário sem perder nenhum checkpoint militar

---

**Próximo documento:** [Roadmap e Implementação](roadmap.md)
