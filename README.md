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
Três não sobreviveram à conferência e **não devem voltar**:

- **“7 dias grátis”** — não existe oferta introdutória em nenhum dos 8 SKUs.
- **“Criptografia ponta a ponta”** — não é o que a arquitetura faz.
- **“Comece de graça”** como chamada — sem assinatura não há match entre lojas,
  que é o produto. A página diz isso com todas as letras.
