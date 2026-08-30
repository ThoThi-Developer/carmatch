# Site MatchMotors

`carmatch.thothi.app` hoje, `matchmotorsbr.com` quando o DNS estiver de pé.
Projeto Vercel **`carmatch`** (`prj_A6p5zlBfbwbMk5ZyYXPcDOnHhWRQ`), ligado a este
repositório. **Push em `main` publica em produção** — trabalhe em branch.

## Arquivos

| Arquivo | O que é |
|---|---|
| `index.html` | A página inteira, um arquivo só. CSS embutido, sem build. |
| `termos.html` | Termos de Uso. **Link obrigatório da App Store** — ver abaixo. |
| `privacidade.html` | Política de Privacidade (LGPD). Também obrigatória. |
| `favicon.svg` | Placa chapada, 1 cor, moldura reforçada (cópia de `docs/marca/`). |
| `index-full-site.html.bak` | O site CarMatch anterior. Histórico — não é servido. |
| `vercel.json` | Reescreve `/dashboard` para o painel web. |

## A marca não é decoração

Os tokens vêm de `CarMatch/docs/marca/brand-tokens.css`, no repo do app. Três
regras que quebram o logo se forem ignoradas:

1. **A rampa de cromo é exata.** A quebra escura em 44–57% é o que faz o metal
   parecer metal. Suavizar aquilo deixa a placa branca e chapada.
2. **Abaixo de 60pt, cromo vira ruído.** A navegação e o rodapé usam a versão
   chapada de propósito; só o herói é cromado.
3. **`#C42019` é a vermelha DA MARCA**, sobre fundo escuro. Tipo vermelho sobre
   fundo claro usa `#8E1D18` — a outra não tem contraste suficiente.

A proporção da placa é 1.538:1 e não se distorce.

## O que a App Store exige desta página

A versão 2.10 foi **rejeitada** pela diretriz 3.1.2: assinatura com renovação
automática sem link funcional para os Termos de Uso nos metadados. Por isso:

- O bloco de assinatura em `#planos` traz nome, periodicidade, faixa de preço,
  condição de renovação e como cancelar. **Não enxugue esse parágrafo.**
- Os links de Termos e Privacidade têm de responder **200** no domínio que
  estiver na App Store. Antes de trocar de domínio, confira:

```bash
curl -sI https://matchmotorsbr.com/termos.html | head -1
```

- Os mesmos dois links vivem no app em `LegalLinks.swift`, num lugar só.
  Trocar de domínio é uma linha lá e uma aqui.

## Rodar local

```bash
python3 -m http.server 4321 --directory /Users/thomascrosara/Developer/carmatch-site
```

## Nada aqui pode prometer o que o app não faz

Cada afirmação desta página foi conferida contra o código antes de entrar.
Duas não sobreviveram e **não devem voltar**:

- **“Criptografia ponta a ponta”** — não é o que a arquitetura faz.
- **Plano gratuito** — não existe. A oferta é **Pro** (assinatura, 3 a 10
  vendedores) ou **Corporativo** (sob consulta, acima disso ou com mais de uma
  loja no grupo). O Corporativo usa o **azul da placa Mercosul** (`#003399`, a
  mesma tarja do campo de placa do app) — é o plano que sai da loja de
  aplicativos e vira conversa.

  ⚠️ Eu já errei isto uma vez: montei um card “Sem plano · R$ 0/mês” a partir do
  enum `starter` do app. Mas o próprio código diz que `starter` **não é mais
  vendido** — é o estado “ainda não assinou / assinatura expirou”, e o rótulo
  dele no app é “Sem plano” por isso. Estado degradado não é plano, e não vai
  na tabela de preços. O que acontece sem assinatura ativa está no rodapé do
  bloco de planos, em uma linha, porque o lojista precisa saber — não porque é
  oferta.

### ⚠️ O trial são 14 dias, e o número mora no ASC

O **app não escreve esse número**: `PaywallSheet.freeTrialText` deriva do
StoreKit em runtime, então ele acompanha o ASC sozinho. **Só o site escreve à
mão**, em 4 lugares (linha fina do herói, card do Pro, bloco legal e FAQ) —
todos marcados com um comentário `<!-- TRIAL -->` no HTML. Mudou no ASC, mude
nos quatro.

Já saiu errado: o site antigo dizia **7 dias** em 4 lugares e eu carreguei esse
número para cá sem conferir. São 14.

### ⚠️ O `.storekit` NÃO é fonte para afirmação comercial

`Configuration.storekit` mostra `introductoryOffer: null` nos 8 SKUs. **Isso não
significa que o trial não existe** — o arquivo é fixture de teste local e não
espelha o App Store Connect. O trial de **7 dias existe** desde 21-jun-2026,
confirmado por Thomas direto no ASC (“Free for the first week”).

Este erro já foi cometido duas vezes (commit `b3d16ec` e de novo em 30-ago-2026,
por mim). Para preço, trial e qualquer promessa comercial, **a fonte é o App
Store Connect** — nunca o fixture.
