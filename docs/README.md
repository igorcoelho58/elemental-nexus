# ELEMENTAL NEXUS
### Jogo de Cartas Estratégico para Mobile

---

## 📋 Visão Geral

**ELEMENTAL NEXUS** é um jogo de cartas estratégico para dois jogadores (Jogador vs IA) inspirado em 7 Wonders Duel, mas com temática de fantasia elemental/mágica. O jogo combina gestão de recursos, construção de civilização e múltiplas vias de vitória em partidas rápidas de 10-15 minutos.

## 🎮 Conceito Principal

Dois reinos elementais competem por supremacia através do domínio dos 5 elementos fundamentais:
- 🌳 **Natureza** - Florestas, vida, crescimento
- 🗻 **Terra** - Montanhas, pedra, estruturas sólidas
- 💧 **Água** - Rios, oceanos, fluxo místico
- 🔥 **Fogo** - Vulcões, forjas, energia destrutiva
- ✨ **Essência** - Magia pura, moeda universal

## 🎯 Objetivos do Projeto

- **Público-alvo**: Jogadores casuais e entusiastas de jogos de tabuleiro
- **Plataforma**: Mobile (Android, iOS) e Desktop (Windows/Linux/Mac) com Unity
- **Modo**: Single-player offline (vs IA com 4 níveis de dificuldade)
- **Duração da partida**: 10-15 minutos
- **Inspiração**: 7 Wonders Duel, mas com mecânicas e temática únicas

## 📊 Características Principais

### Estrutura do Jogo
- **3 Eras** de progressão (Fundação, Expansão, Apogeu)
- **60 Cartas** balanceadas (20 por era)
- **5 Tipos de Carta** + 1 especial (Artefatos Ancestrais na Era III)
- **20+ Monumentos Lendários** (12 iniciais + desbloqueáveis)
- **4 Formas de Vitória** distintas

### Inovações
- Sistema de **Monumentos como foco** central (diferencial do 7 Wonders Duel)
- **Artefatos Ancestrais** - novo tipo de carta especial na Era III
- Temática **Elemental/Mágica** coesa e única
- Sistema de **progressão e desbloqueio** de conteúdo
- **4 níveis de IA** com diferentes personalidades

## 📁 Estrutura da Documentação

```
docs/
├── README.md (este arquivo)
├── conceito-geral.md
│
├── gameplay/
│   ├── regras.md
│   ├── recursos-elementos.md
│   ├── sistema-cientifico.md
│   ├── sistema-militar.md
│   └── formas-de-vitoria.md
│
├── cartas/
│   ├── visao-geral-cartas.md
│   ├── era-I-cartas.md
│   ├── era-II-cartas.md
│   ├── era-III-cartas.md
│   └── monumentos.md
│
├── arte-design/
│   ├── guia-visual.md
│   ├── paleta-cores.md
│   ├── prompts-ia.md
│   └── estrategia-criacao-arte.md
│
└── tecnico/
    ├── arquitetura-unity.md
    ├── sistema-ia.md
    ├── balanceamento.md
    ├── roadmap.md
    └── monetizacao.md
```

## 🎨 Diretrizes Visuais

As cartas são geradas usando IA (Leonardo.ai, Gemini) com estilo **fantasia épica**, iluminação dramática e paleta de cores elementais vibrante.

Referência visual criada: "Floresta Encantada" - moldura celta integrada, arte centralizada, texto decorativo.

## 🚀 Estado Atual

- [x] Conceito e temática definidos
- [x] Sistema de cartas completo (60 cartas balanceadas)
- [x] Sistema de monumentos desenhado (20+ monumentos)
- [x] Regras e mecânicas finalizadas
- [x] Análise de balanceamento completa
- [x] Sistema de IA especificado (4 níveis)
- [x] **Documentação completa** - Todas as 60 cartas documentadas
- [ ] **PRÓXIMO**: Criação de arte das cartas
- [ ] Implementação em Unity/C#
- [ ] Testes e ajustes de balanceamento
- [ ] Lançamento versão 1.0

## 💰 Modelo de Negócio

**Base Gratuita:**
- Jogo completo jogável
- 12 Monumentos iniciais
- IA até Nível 3
- Ads opcionais

**Premium ($2.99):**
- Remove ads
- IA Nível 4 (Lendário)
- 4 Monumentos exclusivos

**DLCs de Monumentos ($0.99 - $3.99):**
- Novos monumentos temáticos
- Sistema de desbloqueio progressivo

## 📅 Cronograma Estimado

- **Fase 1 - Arte**: 2-3 semanas (60 cartas + 20 monumentos)
- **Fase 2 - Programação Core**: 3-4 semanas
- **Fase 3 - IA**: 2-3 semanas
- **Fase 4 - UI/UX**: 2 semanas
- **Fase 5 - Progressão**: 1-2 semanas
- **Fase 6 - Polish**: 1-2 semanas

**Total estimado**: 11-16 semanas (~3-4 meses)

## 🔗 Links Rápidos

- [Conceito Geral Detalhado](conceito-geral.md)
- [Regras do Jogo](gameplay/regras.md)
- [Todas as 60 Cartas](cartas/visao-geral-cartas.md)
- [Sistema de Monumentos](cartas/monumentos.md)
- [Guia de Arte Visual](arte-design/guia-visual.md)
- [Roadmap Técnico](tecnico/roadmap.md)

---

**Versão da Documentação**: 1.0  
**Última Atualização**: Novembro 2025  
**Status**: Em Desenvolvimento
