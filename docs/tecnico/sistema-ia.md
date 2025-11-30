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

### Estrutura de Código (C# / Unity)

```csharp
// Usando UnityEngine para acesso a MonoBehaviour e outras funções da Unity
using UnityEngine;
using System.Collections.Generic;
using System.Linq;

// A classe base para todos os níveis de IA. Herda de MonoBehaviour para poder ser um componente em um GameObject.
public abstract class AIPlayer : MonoBehaviour
{
    public AILevel level;
    protected GameState gameState; // Referência ao estado atual do jogo

    // Método principal que o GameManager chamará para obter a decisão da IA
    public abstract CardData ChooseCard(List<CardData> availableCards);

    // Método para avaliar o valor de uma única carta
    protected abstract float EvaluateCard(CardData card, GameState state);

    // Método para determinar a ação a ser tomada
    public virtual GameAction ChooseAction(List<CardData> availableCards)
    {
        CardData cardToPlay = ChooseCard(availableCards);
        // Lógica adicional pode ser inserida aqui para decidir entre construir, descartar, etc.
        return new GameAction(ActionType.Construct, cardToPlay);
    }
}

// Exemplo da IA Aprendiz
public class ApprenticeAI : AIPlayer
{
    public override CardData ChooseCard(List<CardData> availableCards)
    {
        if (availableCards.Count == 0) return null;

        // Encontra a carta com a maior avaliação
        return availableCards.OrderByDescending(card => EvaluateCard(card, gameState)).First();
    }

    protected override float EvaluateCard(CardData card, GameState state)
    {
        // Lógica de avaliação simples, como no documento
        return card.pontos + (card.recursosProduzidos.Length * 0.5f) + card.escudos;
    }
}

// Exemplo da IA Veterano com bloqueio
public class VeteranAI : AIPlayer
{
    public override CardData ChooseCard(List<CardData> availableCards)
    {
        if (availableCards.Count == 0) return null;
        
        return availableCards.OrderByDescending(card => EvaluateCard(card, gameState)).First();
    }

    protected override float EvaluateCard(CardData card, GameState state)
    {
        float value = card.pontos
                    + (card.recursosProduzidos.Length * 1.5f)
                    + (card.escudos * 2f)
                    + (card.simbolosCientificos.Length * 3f);

        if (card.chain != null) value += 3f;
        if (ShouldBlock(card, state)) value += 2f;

        return value;
    }

    // Simples chance de 30% de identificar uma carta como "necessária" para bloqueio
    private bool ShouldBlock(CardData card, GameState state)
    {
        // Uma lógica mais avançada aqui iria verificar o estado do oponente
        return Random.value < 0.3f; // Random.value retorna um float entre 0.0 e 1.0
    }
}

// Estrutura para a IA Lendária usando Minimax (simplificado)
public class LegendaryAI : AIPlayer
{
    public override CardData ChooseCard(List<CardData> availableCards)
    {
        if (availableCards.Count == 0) return null;
        
        // Retorna a melhor jogada encontrada pelo algoritmo Minimax
        return MinimaxDecision(availableCards, depth: 4);
    }

    protected override float EvaluateCard(CardData card, GameState state)
    {
        // A avaliação direta é menos importante aqui, pois o Minimax avalia estados futuros
        // Mas ainda é usada como a função de avaliação final na profundidade máxima
        float value = card.pontos; // ... e outros fatores
        return value;
    }

    private CardData MinimaxDecision(List<CardData> cards, int depth)
    {
        CardData bestCard = null;
        float bestValue = float.NegativeInfinity;

        foreach (var card in cards)
        {
            // Simula a jogada e avalia o estado resultante
            GameState futureState = gameState.SimulatePlay(card, this.gameObject);
            float value = MinValue(futureState, depth - 1, float.NegativeInfinity, float.PositiveInfinity);

            if (value > bestValue)
            {
                bestValue = value;
                bestCard = card;
            }
        }
        return bestCard;
    }

    // Função Min do algoritmo Minimax com poda Alfa-Beta
    private float MinValue(GameState state, int depth, float alpha, float beta)
    {
        if (depth == 0 || state.IsGameOver())
        {
            return state.Evaluate(); // Avalia o estado final do jogo
        }

        float value = float.PositiveInfinity;
        // ... (lógica para encontrar as jogadas possíveis do oponente e chamar MaxValue)
        return value;
    }

    // Função Max do algoritmo (não mostrada para brevidade)
    private float MaxValue(GameState state, int depth, float alpha, float beta) 
    {
        // ...
        return 0f;
    }
}

// Exemplo de como um CardData seria (usando ScriptableObject)
// [CreateAssetMenu(fileName = "Nova Carta", menuName = "Elemental Nexus/Carta")]
// public class CardData : ScriptableObject
// {
//     public string nome;
//     public int pontos;
//     public Resource[] recursosProduzidos;
//     public int escudos;
//     public ScienceSymbol[] simbolosCientificos;
//     public CardData chain;
//     // ... outros campos
// }
```

### Balanceamento de Tempo

| Nível | Tempo de Resposta | Complexidade Computacional |
|-------|-------------------|----------------------------|
| Aprendiz | Instantâneo (<0.1s) | O(n) - Linear |
| Veterano | Rápido (0.1-0.2s) | O(n log n) |
| Mestre | Moderado (0.3-0.5s) | O(n²) - Quadrático (simulação) |
| Lendário | Pensando (0.5-1.5s) | O(b^d) - MinMax (b=ramificação, d=profundidade) |

**Nota:** A performance em C# compilado na Unity (via IL2CPP) é geralmente muito alta. Delays artificiais podem ser adicionados via Coroutines para "humanizar" a IA, fazendo-a parecer que está "pensando".

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
