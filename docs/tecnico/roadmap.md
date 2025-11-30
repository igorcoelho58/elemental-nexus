# Roadmap de Implementação - ELEMENTAL NEXUS

## 🚀 Visão Geral

Cronograma estimado: **3-4 meses** para versão 1.0

---

## 📅 FASE 1 - ARTE E ASSETS (2-3 semanas)

### Objetivos
Criar todas as artes das cartas, monumentos e interface.

### Tarefas

**Semana 1: Setup e Templates**
- [ ] Configurar Leonardo.ai / Gemini
- [ ] Criar 5 cartas template (1 de cada tipo)
- [ ] Refinar prompts e estilo visual
- [ ] Documentar pipeline de geração

**Semana 2: Cartas Principais (30 cartas)**
- [ ] Gerar todas as cartas de Recurso (19 cartas)
- [ ] Gerar Legiões principais (11 cartas)
- [ ] Primeira revisão de qualidade

**Semana 3: Cartas Especiais e Monumentos**
- [ ] Gerar Estruturas (15 cartas)
- [ ] Gerar Mercado e Grimórios (13 cartas)
- [ ] Gerar Artefatos (2 cartas)
- [ ] Gerar 12 Monumentos iniciais
- [ ] Revisão final e aprovação

**Entregáveis:**
- ✅ 60 artes de cartas finalizadas
- ✅ 12 artes de monumentos finalizadas
- ✅ Ícones dos 5 elementos
- ✅ Ícones dos 4 símbolos científicos
- ✅ Assets de UI (botões, backgrounds, etc.)

---

## 📅 FASE 2 - PROGRAMAÇÃO CORE (3-4 semanas)

### Objetivos
Implementar mecânicas fundamentais do jogo.

### Tarefas

**Semana 1: Estrutura de Dados**
- [ ] Setup do projeto Unity/C#
- [ ] Criar ScriptableObjects para `Card`, `Monument`
- [ ] Criar classes C# para `Player`, `GameState`
- [ ] Sistema de serialização (JSON para save games)
- [ ] Criar os 60 assets de `CardData` via ScriptableObjects

**Semana 2: Lógica de Jogo**
- [ ] Sistema de recursos e produção
- [ ] Sistema de construção de cartas
- [ ] Lógica de custos (comprar recursos do oponente)
- [ ] Sistema de chains (correntes)
- [ ] Validação de ações

**Semana 3: Sistemas de Vitória**
- [ ] Trilha militar (15 espaços, checkpoints)
- [ ] Sistema científico (símbolos, vitória por 6)
- [ ] Contagem de pontos
- [ ] Sistema de monumentos (construção e vitória)
- [ ] Detector de vitória

**Semana 4: Fluxo de Partida**
- [ ] Seleção de monumentos (draft)
- [ ] Montagem de pirâmide por Era
- [ ] Alternância de turnos
- [ ] Transição entre Eras
- [ ] Tela de fim de jogo (resultados)

**Entregáveis:**
- ✅ Jogo funcionando em modo "manual" (2 humanos)
- ✅ Todas as regras implementadas
- ✅ 4 formas de vitória funcionando
- ✅ Sem bugs críticos

---

## 📅 FASE 3 - INTELIGÊNCIA ARTIFICIAL (2-3 semanas)

### Objetivos
Criar os 4 níveis de IA jogáveis.

### Tarefas

**Semana 1: IA Básica**
- [ ] Implementar IA Aprendiz (Nível 1)
  - Heurística simples
  - Testes de comportamento
- [ ] Implementar IA Veterano (Nível 2)
  - Reconhecimento de chains
  - Bloqueio probabilístico (30%)
  - Testes de competência

**Semana 2: IA Avançada**
- [ ] Implementar IA Mestre (Nível 3)
  - Detecção de win conditions
  - Planejamento 3 turnos à frente
  - Adaptação estratégica
  - Testes de dificuldade

**Semana 3: IA Suprema e Balanceamento**
- [ ] Implementar IA Lendário (Nível 4)
  - Algoritmo MinMax simplificado
  - Vantagem inicial (+3 Essência)
  - Bloqueio agressivo (80%)
- [ ] Balancear dificuldades
- [ ] Testes extensivos (50+ partidas por nível)
- [ ] Ajustar heurísticas baseado em dados

**Entregáveis:**
- ✅ 4 níveis de IA funcionais
- ✅ Curva de dificuldade balanceada
- ✅ IA não trapaceia (justa)
- ✅ Tempos de resposta otimizados

---

## 📅 FASE 4 - UI/UX E INTERFACE (2 semanas)

### Objetivos
Criar interface polida e intuitiva.

### Tarefas

**Semana 1: Telas Principais**
- [ ] Tela de Menu Principal
  - Logo do jogo
  - Botões (Jogar, Conquistas, Configurações)
  - Animações de entrada
- [ ] Tela de Seleção de Dificuldade
  - 4 botões (Aprendiz, Veterano, Mestre, Lendário)
  - Descrição de cada nível
- [ ] Tela de Seleção de Monumentos
  - Grid de monumentos disponíveis
  - Preview de efeitos
  - Sistema de escolha (jogador → IA)

**Semana 2: Tela de Jogo**
- [ ] Layout da pirâmide de cartas
  - Cartas viradas para cima/baixo
  - Highlight de cartas livres
  - Zoom ao tocar
- [ ] Área do jogador
  - Cartas construídas
  - Recursos disponíveis
  - Monumentos construídos
  - Essência atual
- [ ] Área da IA
  - Mesmas informações (visíveis)
- [ ] Trilha militar central
  - Marcador animado
  - Checkpoints destacados
- [ ] Indicadores de turno
  - De quem é o turno
  - Timer (opcional)

**Elementos de UI:**
- [ ] Botões de ação (Construir, Descartar, Monumento)
- [ ] Modal de confirmação
- [ ] Histórico de ações (últimas 5)
- [ ] Contador de cartas restantes por Era

**Entregáveis:**
- ✅ Interface completa e funcional
- ✅ Todas as telas navegáveis
- ✅ Feedback visual claro
- ✅ Responsivo (diferentes tamanhos de tela Android)

---

## 📅 FASE 5 - PROGRESSÃO E META-JOGO (1-2 semanas)

### Objetivos
Implementar sistemas de retenção e progressão.

### Tarefas

**Semana 1: Sistema de Desbloqueio**
- [ ] Salvar progresso local (PlayerPrefs ou JSON)
- [ ] Rastreamento de vitórias
  - Por nível de IA
  - Por tipo de vitória
  - Sequências de vitórias
- [ ] Sistema de XP (opcional)
- [ ] Desbloqueio de monumentos
  - Condições específicas por monumento
  - Animação de "novo monumento desbloqueado"
- [ ] Histórico de partidas
  - Últimas 10 partidas
  - Estatísticas (vitórias, derrotas, pontuação média)

**Semana 2: Conquistas**
- [ ] Definir 30-40 conquistas
  - Vitórias gerais
  - Vitórias por tipo
  - Desafios especiais
  - Coleção de monumentos
- [ ] Tela de Conquistas
  - Grid de conquistas
  - Progresso de cada uma
  - Recompensas
- [ ] Notificações de conquista desbloqueada

**Extras (Opcionais):**
- [ ] Daily login bonus (moeda fictícia)
- [ ] Desafios diários
- [ ] Leaderboard local (melhor pontuação)

**Entregáveis:**
- ✅ Sistema de progressão completo
- ✅ 30+ conquistas implementadas
- ✅ 8 monumentos desbloqueáveis funcionando
- ✅ Histórico e estatísticas salvando

---

## 📅 FASE 6 - POLISH E LANÇAMENTO (1-2 semanas)

### Objetivos
Refinar, testar e preparar para lançamento.

### Tarefas

**Semana 1: Polish**
- [ ] Efeitos sonoros
  - Som de construir carta
  - Som de ganhar Essência
  - Som de checkpoint militar
  - Som de vitória/derrota
- [ ] Música de fundo
  - Menu (calma)
  - Jogo (épica mas não intrusiva)
  - Opção de mutar
- [ ] Animações
  - Cartas sendo construídas (flip/scale)
  - Movimento do marcador militar
  - Transição entre Eras
  - Partículas de vitória
- [ ] Tutorial interativo
  - 5-7 passos guiados
  - Explica cada tipo de carta
  - Explica formas de vitória
  - Pulável (para rejogadores)

**Semana 2: Testes e Correções**
- [ ] Testes em múltiplos dispositivos
  - Telas pequenas (5")
  - Telas médias (6")
  - Telas grandes (7"+)
  - Diferentes resoluções
- [ ] Performance otimizada
  - 60 FPS constante
  - Carregamento rápido (<3s)
  - Tamanho do APK <150MB
- [ ] Bug fixing
  - Testar todas as 60 cartas
  - Testar todos os monumentos
  - Testar edge cases
  - Garantir vitórias funcionam 100%
- [ ] Tradução (se aplicável)
  - PT-BR (principal)
  - EN (opcional para futuro)

**Preparação de Lançamento:**
- [ ] Criar ícone do app (512x512px)
- [ ] Screenshots para Play Store (6-8 imagens)
- [ ] Vídeo promocional (30-60s)
- [ ] Descrição da loja otimizada (ASO)
- [ ] Política de Privacidade
- [ ] Termos de Serviço

**Entregáveis:**
- ✅ Jogo polido e completo
- ✅ Tutorial funcional
- ✅ Todos os bugs críticos corrigidos
- ✅ Assets da loja prontos
- ✅ APK release assinado

---

## 📅 PÓS-LANÇAMENTO

### Versão 1.1 (1-2 meses após v1.0)
- [ ] Analisar feedback de jogadores
- [ ] Ajustes de balanceamento baseado em dados
- [ ] Correção de bugs reportados
- [ ] 4 novos monumentos desbloqueáveis (grátis)
- [ ] Melhorias de UX baseadas em usabilidade

### Versão 1.2 (3-4 meses após v1.0)
- [ ] **DLC Premium:** Pacote "Maravilhas Antigas" ($0.99)
  - 4 monumentos temáticos
- [ ] Modo Campanha (série de desafios)
- [ ] Conquistas adicionais (10-15)
- [ ] Melhorias de IA baseadas em análise

### Versão 2.0 (6-12 meses após v1.0)
- [ ] Expansão de conteúdo:
  - 20 novas cartas (expansão "Sombras do Vazio")
  - 8 novos monumentos
  - Nova mecânica de jogo (ex: Eventos aleatórios)
- [ ] Modo PvP online (multiplayer)
- [ ] Leaderboard global
- [ ] Torneios semanais

---

## 📊 Métricas de Sucesso

### Técnicas
- ✅ 0 crashes críticos
- ✅ Carregamento <3 segundos
- ✅ 60 FPS em dispositivos mid-range
- ✅ Tamanho do app <150MB

### Retenção (Primeiros 30 dias)
- 🎯 D1 (dia 1): 40% de retenção
- 🎯 D7 (dia 7): 15% de retenção
- 🎯 D30 (dia 30): 5% de retenção

### Engajamento
- 🎯 Duração média de sessão: 15-20 minutos
- 🎯 Sessões por usuário/dia: 2-3
- 🎯 Taxa de completar tutorial: >70%

### Monetização (Se aplicável)
- 🎯 Taxa de conversão para Premium: 2-5%
- 🎯 ARPU (receita por usuário): $0.20-0.50
- 🎯 Avaliação na Play Store: >4.0 ⭐

---

## 🛠️ Stack Tecnológico

### Desenvolvimento
- **Motor:** Unity 2022 LTS (ou superior)
- **Linguagem:** C# 10
- **IDE:** Visual Studio / JetBrains Rider
- **Controle de Versão:** Git + GitHub (com Git LFS)

### Bibliotecas Principais
- **Animações:** DOTween (opcional, para tweens via código)
- **UI:** Unity UI (nativo)
- **Persistência:** PlayerPrefs ou sistema de serialização JSON customizado

### Ferramentas
- **Design:** Figma (wireframes)
- **Arte:** Leonardo.ai / Gemini
- **Testes:** Unity Test Runner (Edit Mode e Play Mode)
- **CI/CD:** GitHub Actions (futuro)
- **Analytics:** Unity Analytics (pós-lançamento)

---

## 💰 Orçamento Estimado

### Custos de Desenvolvimento

| Item | Custo | Nota |
|------|-------|------|
| Leonardo.ai (1 mês) | $12 | Para artes premium |
| Google Play Developer | $25 | Único, vitalício |
| Domínio (opcional) | $10/ano | Para site |
| **Total Mínimo** | **$37** | **Viável!** |

### Custos Opcionais
- Adobe Illustrator (UI assets): $20/mês (pode usar alternativas gratuitas)
- Figma Pro: $12/mês (versão gratuita funciona)
- Áudio (compra de SFX/Música): $0-50 (pode usar assets gratuitos)
- DOTween Pro: ~$15 (opcional, a versão gratuita é suficiente)

### Receita Potencial (Ano 1, Otimista)
```
Downloads: 10.000
Conversão Premium (3%): 300 usuários
Receita Premium: 300 × $2.99 = $897

DLC Sales (2% dos usuários): 200
Receita DLC: 200 × $0.99 = $198

Total Receita Ano 1: ~$1.095
Lucro (após Google 30%): ~$767
ROI: ~2.000%
```

**Realista:** Receita será menor, mas projeto é viável financeiramente e pode crescer organicamente.

---

## ✅ Checklist de Lançamento

### Obrigatórios
- [ ] Jogo completo e jogável (60 cartas + 12 monumentos)
- [ ] 4 níveis de IA funcionando
- [ ] Tutorial completo
- [ ] 0 crashes críticos
- [ ] Testado em 5+ dispositivos diferentes
- [ ] Ícone e screenshots da loja
- [ ] Política de privacidade
- [ ] APK assinado e otimizado

### Desejáveis
- [ ] 30+ conquistas
- [ ] Sistema de progressão completo
- [ ] Efeitos sonoros e música
- [ ] Animações polidas
- [ ] 8 monumentos desbloqueáveis
- [ ] Estatísticas de partida

### Pós-Lançamento
- [ ] Analytics configurado
- [ ] Sistema de feedback
- [ ] Roadmap de updates
- [ ] Comunidade (Discord/Reddit)

---

## 🎯 Próximos Passos Imediatos

1. **HOJE:** Finalizar documentação
2. **Esta Semana:** Começar geração de artes (Fase 1)
3. **Semana 2:** Setup do projeto Unity
4. **Semana 3:** Primeiras cartas jogáveis
5. **Mês 1 Completo:** Arte + Estrutura básica
6. **Mês 2:** Mecânicas + IA
7. **Mês 3:** UI/UX + Polish
8. **Mês 4:** Testes + Lançamento

---

**Sucesso do projeto = Execução consistente + Paixão pelo que está criando! 🚀🎮**
