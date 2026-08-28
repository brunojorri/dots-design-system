# Dots Design System — Regras rápidas

Guia de referência curto, pensado para orientar quem (humano ou IA) for montar
novos templates a partir deste repositório. Não substitui olhar o HTML/CSS
diretamente — é um resumo das decisões e convenções que não estão óbvias só
olhando o código.

## Arquivos do repositório

| Arquivo | O que é |
|---|---|
| `dots-design-system.html` | Página principal do sistema de design (marca, cores, tipografia, Dark Mode, White Mode, componentes, fotografia). Layout centralizado (`max-width:1180px`). |
| `templates.html` | Galeria completa de templates de campanha. Layout de ponta a ponta (full-width), diferente da página principal. |
| `template_01.webm` | Asset de vídeo de campanha (VP9, ~2,75 MB), referenciado por caminho relativo nos templates. **Precisa estar na mesma pasta** que `templates.html` no repositório. |
| `poster_template_01.jpg` | Frame estático usado como poster do vídeo (mostrado antes do vídeo carregar, ou se falhar). |

Se novos vídeos de campanha forem adicionados, sigam o mesmo padrão: arquivo
`.webm` real ao lado do HTML, nunca embutido em base64 — deixa o HTML legível
e evita inflar o repositório.

## Cores por tipo de fundo (regra de contraste)

Esta é a regra mais fácil de errar, então fica destacada:

- **Fundo pontilhado claro** (branco + grid de pontos azul) → título sempre em
  **azul Docato inteiro** (`#0057FF` / `var(--azul-docato)`), nunca misturado
  com preto ou azul-escuro, nem parcialmente destacado com `<span>`.
- **Fundo é o próprio vídeo** (full-bleed, sem pontos visíveis) → título
  sempre **branco inteiro** (`#FFFFFF`).
- **Fundo escuro sólido** (navy `#04122A` ou azul Docato sólido, com ou sem
  grid de pontos escuro) → título em branco. Esses casos não seguem as duas
  regras acima porque não são "pontilhado claro" nem "vídeo full-bleed" —
  são uma terceira categoria (fundo sólido escuro).

## Quebra de linha em títulos

Sempre que um título de template tiver vírgula, quebra a linha logo depois
dela, deixando o resto da frase na linha seguinte:

```html
<!-- Correto -->
<h4>Menos tempo de resposta,<br>mais acordos homologados.</h4>

<!-- Incorreto -->
<h4>Menos tempo de resposta, mais acordos homologados.</h4>
```

Títulos sem vírgula ficam numa linha só (ou com quebra manual, se o próprio
conteúdo pedir — ex.: o template "Título" tem três linhas curtas de propósito).

## Nomenclatura das seções (Dark Mode / White Mode)

A seção antes chamada "Liquid Glass" foi renomeada:
- **04 · Dark Mode** (antes "Liquid Glass")
- **05 · White Mode** (antes "Liquid Glass — White Mode")

O nome "Liquid Glass" não deve mais aparecer em nenhum lugar da página — a
identidade visual está migrando para cards de cor sólida.

## Convenção de nomes de classe

Cada família de template usa um prefixo próprio, sempre `artboard-*`:

| Prefixo | Template |
|---|---|
| `.artboard-overlay` | Capa (vídeo full-bleed + overlay de texto) |
| `.artboard-content` | Conteúdo (cards de dado, sem vídeo) |
| `.artboard-title-only` | Título (só grid de pontos + headline) |
| `.artboard-quote` | Encerramento (vídeo em janela pequena + citação) |
| `.artboard-split` | Widescreen dividido (vídeo de um lado, texto do outro, borda a borda) |
| `.artboard-window` | Widescreen janela (vídeo contido/estreito, texto ao lado, sobre o grid de pontos) |
| `.artboard-fullbleed` | Widescreen tela cheia (vídeo ocupa 100%, texto sobreposto) |

Ao criar um template novo, mantenha esse padrão: um prefixo `artboard-*`
próprio, mais os sufixos internos (`-text`, `-video`, `-overlay` etc.) que já
aparecem nos existentes.

## Proporções

- Templates "de post" (retrato): `aspect-ratio: 3/4`
- Templates widescreen (apresentação): `aspect-ratio: 16/9`, equivalente a
  1920×1080

## Próximos passos sugeridos

- Ao subir para o GitHub, manter os três arquivos de asset (`.html`, `.webm`,
  `.jpg`) na mesma pasta — os caminhos usados são relativos, não absolutos.
- Se a galeria crescer bastante, considerar separar os artboards em uma
  pasta própria (`/templates/`) com este arquivo de regras na raiz do
  repositório, para qualquer ferramenta de design/IA encontrar rápido.
