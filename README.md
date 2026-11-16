# Mapa interativo de manual

Página web que transforma um manual em um mapa mental navegável. O tema central fica no meio, os capítulos saem dele como ramos e cada seção mostra seu texto ao ser clicada.

O conteúdo que acompanha o projeto é um **texto de exemplo fictício**, um manual psicopedagógico sobre aplicação de jogos, criado só para demonstrar o funcionamento. Ele deve ser substituído pelo manual real.

## Recursos

- **Ramos que abrem e fecham:** clique em um capítulo para mostrar ou esconder suas seções.
- **Painel de detalhes:** ao clicar em um tópico, o texto correspondente aparece ao lado (ou embaixo, no celular), com o caminho até ele e atalhos para as seções filhas.
- **Busca:** procura no título e no texto de todos os tópicos, ignora acentos e maiúsculas, abre os ramos onde há resultados e esmaece o restante. A busca começa a partir de 2 caracteres, e a tecla Enter abre o primeiro resultado.
- **Zoom e movimento:** arraste para mover o mapa, use a roda do mouse ou os botões `+` e `−` para o zoom, e `⤢` para ajustar tudo à tela.
- **Expandir tudo / Recolher:** abre ou fecha todos os ramos de uma vez.
- **Acessível pelo teclado:** os nós recebem foco com `Tab` e são ativados com `Enter` ou `Espaço`.
- **Modo claro e escuro:** segue a preferência do sistema.
- **Responsivo:** funciona em telas de computador e de celular.

## Como usar

Não há instalação nem etapa de build. O projeto é um único arquivo:

```
mapa-manual-psicopedagogico.html
```

Abra o arquivo em qualquer navegador moderno (Chrome, Edge, Firefox ou Safari) ou hospede-o em qualquer serviço que sirva arquivos estáticos.

> A fonte **Nunito** é carregada do Google Fonts. Sem conexão com a internet, a página usa a fonte padrão do sistema e continua funcionando normalmente.

## Como trocar o conteúdo

Todo o conteúdo está no objeto `DATA`, no início do bloco `<script>`. Cada nó tem três campos:

| Campo  | Função                                              |
| ------ | --------------------------------------------------- |
| `t`    | Título exibido no nó                                |
| `d`    | Texto mostrado no painel de detalhes                |
| `kids` | Lista de nós filhos (opcional)                      |

Exemplo:

```js
var DATA = {
  t: "Título do manual",
  d: "Resumo do manual.",
  kids: [
    {
      t: "Capítulo 1",
      d: "Introdução ao capítulo.",
      kids: [
        { t: "Seção 1.1", d: "Texto da seção." },
        { t: "Seção 1.2", d: "Texto da seção." }
      ]
    }
  ]
};
```

### Limites da estrutura atual

- O mapa tem **três níveis**: tema central, capítulos e seções. Nós abaixo das seções não são desenhados.
- As cores dos ramos vêm das variáveis `--b0` a `--b4`, ou seja, **cinco capítulos** têm cor própria. Para usar mais, acrescente `--b5`, `--b6` e assim por diante nos dois blocos de cores (claro e escuro) no CSS.
- Títulos curtos funcionam melhor. Eles quebram em linhas automaticamente, mas títulos muito longos deixam os nós largos e podem encostar uns nos outros.

## Personalização

### Cores

Os tons ficam no início do CSS, em `:root`, e são repetidos para o modo escuro.

| Variável         | Uso                              |
| ---------------- | -------------------------------- |
| `--bg`           | Fundo da página                  |
| `--surface`      | Fundo do painel e dos botões     |
| `--ink`          | Texto principal e nó central     |
| `--b0` … `--b4`  | Cor de cada capítulo             |

### Distâncias do mapa

No começo do script:

```js
var R1 = 215;   // distância dos capítulos ao centro
var R2 = 440;   // distância das seções ao centro
var STEP = .43; // espaçamento angular entre seções do mesmo capítulo (radianos)
```

Aumente `R2` ou `STEP` se as seções ficarem apertadas.

## Estrutura do código

O arquivo se divide em três partes:

1. **CSS:** tokens de cor, estilo dos nós e do painel, e ajustes para celular.
2. **`DATA`:** o conteúdo do manual.
3. **Script:** calcula o layout radial, desenha o mapa em SVG, e trata clique, arraste, zoom, busca e painel.

## Compatibilidade

Navegadores atuais com suporte a SVG, `color-mix()` e Pointer Events.

## Licença

Defina aqui a licença do projeto.
