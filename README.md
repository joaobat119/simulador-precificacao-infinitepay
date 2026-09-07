# Simulador de Preço de Venda — InfinitePay

Página principal proposta para o teste técnico de Growth da InfinitePay.

**URL de produção pretendida:** `infinitepay.io/calculadoras/precificacao`

---

## O que é

Ferramenta gratuita que calcula o preço de venda de um produto ou serviço a partir do custo de material, tempo de trabalho, rateio de custos fixos, margem desejada, taxa da maquininha e imposto.

Duas páginas HTML, sem dependências, sem build. Abrir `index.html` no navegador.

---

## Por que esta ferramenta

Resumo da análise — o detalhamento está no documento de estratégia.

| Critério | Cluster precificação | Cluster trabalhista (alternativa) |
|---|---|---|
| Volume/mês | 61.740 (núcleo comercial: 33.770) | 216.900 |
| KD médio | **5,5** | 45,7 |
| `is_commercial` | **33.770 de 61.740 em volume** | 0 de 7 keywords |
| Referring domains dos líderes | **0 a 29** — a líder tem **1** | 72 a 160 |
| Formato que ranqueia | Artigo domina o topo | Calculadora (ocupado) |

**A tese: híbrido vence artigo puro.** Existem três formatos-ferramenta no cluster e todos perdem — a calculadora do vendamais está em #9 com 7 visitas/mês (rd=29), enquanto artigos ocupam #1 a #5. O motivo é intenção: só 1.610 buscas são de intenção instrumental — 2,6% do cluster; o resto é informacional ou aplicado por profissão. Ferramenta pura atende a fatia pequena.

Esta página é híbrida: simulador acima da dobra para a intenção instrumental, conteúdo abaixo para a informacional, satélites para a aplicada por profissão.

*Limitação declarada: não existe página híbrida no cluster para comparar. É extrapolação, e o critério de kill existe por causa dela.*

**ICP:** as keywords de cauda longa são *quanto cobrar por unha, por bolo, por corte de cabelo, por marmita, por hora*. Manicure, confeiteiro, barbeiro, entregador — o cliente declarado da InfinitePay.

**Dor comprovada fora do dataset** (permitido pelo enunciado para justificar fit):
- 89% dos empreendedores não se sentem confiantes na formação de preço — Preço Certo, 10 mil empresas, citado pelo Sebrae
- 76% tiveram aumento de custos e apenas 9% repassaram integralmente — Sebrae/IBGE, Pesquisa Pulso, 6 mil respondentes

---

## Estrutura do silo

Apenas a página principal foi desenvolvida, conforme o enunciado. As demais estão desenhadas e linkadas.

```
/calculadoras/                                  hub
└── /calculadoras/precificacao                  ★ index.html — "precificacao" (14.800)
    ├── /calculadoras/quanto-cobrar-por-unha    ★ construída — (3.100)
    ├── /calculadoras/quanto-cobrar-por-bolo            (2.400)
    ├── /calculadoras/quanto-cobrar-por-corte-de-cabelo (2.200)
    ├── /calculadoras/quanto-cobrar-por-hora            (1.600)
    └── /calculadoras/quanto-cobrar-por-marmita         (1.400)
```

**Duas páginas foram construídas:** a principal e um satélite.

O satélite existe para provar que o padrão não é conteúdo duplicado. Satélite que só troca valores padrão e title é *doorway page* — o Google pune isso explicitamente. A diferença precisa estar no conteúdo.

O que a página de unha tem de próprio:

| | Página principal | Satélite unha |
|---|---|---|
| Campos | Material, unidades vendidas | Material, **cabine**, atendimentos |
| Interação | — | **Seletor de serviço** com material e duração reais |
| Métricas | Markup, margem real | **Ganho por hora real**, faturamento no mês |
| Conteúdo | Markup vs margem, custos fixos | **Rateio de esmalte e alicate**, cabine vs domicílio, taxa de ocupação |
| FAQ | Genérica de precificação | **MEI com DAS fixo**, alongamento vs esmaltação, reajuste de tabela |

Os outros quatro satélites exigem a mesma pesquisa de custo real de cada setor. Estão desenhados, linkados e priorizados por volume no roadmap — fazer mal seria pior que não fazer.

---

## Decisões de SEO

**URL `/calculadoras/precificacao`** — keyword exata, sem stopword, em diretório que comunica a categoria. Silo novo, deliberadamente fora de `/materiais/`, onde as ferramentas atuais da InfinitePay estão em posição 23–67. Começar limpo evita herdar passivo e permite medir o experimento isolado.

**Title ≠ H1** — o title é otimizado para clique na SERP (inclui "grátis" e o ano). O H1 é otimizado para clareza na página.

**Ferramenta acima da dobra** — a intenção da busca é instrumental: a pessoa quer o número, não o ensaio. Enterrar o simulador sob parágrafos de introdução gera bounce, e bounce em página que disputa o topo é fatal.

**Resultado linha a linha** — o card mostra material, tempo, rateio, custo total, taxa, imposto, markup e margem real. Não só o preço final. É o formato que um LLM consegue extrair e citar.

**HTML estático** — todo o conteúdo existe no HTML da primeira resposta, incluindo os valores iniciais do resultado. O JavaScript apenas recalcula. Crawler e assistente de IA leem a página inteira sem executar script.

**Zero requisição externa** — sem framework, sem CDN, sem fonte bloqueante. Uma única requisição HTML de ~31 KB. Em produção, a fonte da marca seria self-hosted com `font-display: swap`.

**Canonical autorreferencial** — um simulador gera variação por query string; sem canonical isso vira duplicação.

**HTML semântico** — `<table>` real para a equivalência markup/margem, `<h2>`/`<h3>` reais, `<details>` nativo no FAQ. É o que um LLM extrai.

### Schema

| Tipo | Função |
|---|---|
| `WebApplication` | Faz o Google entender que é **ferramenta**, não artigo |
| `FAQPage` | Alvo de People Also Ask e de retrieval por assistentes de IA |
| `BreadcrumbList` | Comunica a arquitetura de silo ao crawler |

### Formato AEO

Pergunta como heading, resposta direta nas duas primeiras frases, números explícitos no corpo do texto, tabela em HTML real. É o bloco que ChatGPT, Perplexity, Gemini e o AI Overview conseguem recuperar e citar.

---

## O que foi deliberadamente deixado de fora

**Os cinco satélites.** Uma página excelente vale mais que seis medianas, e o enunciado pede a principal.

**Lógica tributária completa.** O enunciado é explícito de que o peso não está na ferramenta. Cálculo simplificado comunica o valor; cada hora em regime tributário é uma hora não gasta na estrutura que ranqueia.

**Captura de e-mail antes do resultado.** Ferramenta gratuita com paywall tem bounce alto. O resultado aparece sem cadastro.

**Calculadoras de outro tema no mesmo diretório.** Misturar IMC ou geradores genéricos diluiria a coerência temática do silo.

---

## A conexão com produto

A taxa da maquininha é um campo do cálculo, não um banner. Mudar a taxa muda o preço necessário para manter a mesma margem — com os valores padrão, sair de 3,15% para 0% (Pix) derruba o preço de R$ 103,53 para R$ 98,44 sem alterar a margem de 30%.

O CTA é consequência do cálculo, não enxerto: se a taxa da pessoa está alta, a InfinitePay tem resposta para isso.

---

## Qualidade

- Responsivo até 390px, sem overflow horizontal
- Contraste auditado: nenhum elemento abaixo de 4.5:1
- Foco de teclado visível
- `prefers-reduced-motion` respeitado
- Sem `localStorage` — nada dos dados do usuário sai do navegador

---

## Cálculo

Método markup divisor:

```
custo_total = material + (horas × valor_hora) + (custos_fixos ÷ volume_mensal)
percentuais = margem_desejada + taxa_maquininha + imposto
preço       = custo_total ÷ (1 − percentuais ÷ 100)
```

A divisão é o que garante a margem *depois* dos descontos. Somar uma porcentagem sobre o custo — o erro mais comum — produz margem menor que a planejada, porque taxa e imposto incidem sobre o preço final, não sobre o custo.

Quando os percentuais somam 100% ou mais, não existe preço possível e a ferramenta avisa em vez de exibir um número sem sentido.

---

*Página de demonstração para processo seletivo. Os cálculos são simplificados e servem como estimativa.*
