[English](AGENTS.md) · [Español](AGENTS.es.md) · **Português** · [Français](AGENTS.fr.md) · [Deutsch](AGENTS.de.md)

# AGENTS.md

Guia para agentes de IA e colaboradores que modifiquem este repositório.

## O que é

Site estático de uma única página para testar e diagnosticar telas (celular, computador e TV). Tudo fica em `index.html`: HTML, CSS e JavaScript sem dependências, sem bundler e sem rede.

## Estrutura

- `index.html`: o site completo.
- `README.md` (e `README.es.md`, `README.pt.md`, `README.fr.md`, `README.de.md`): descrição e recursos para usuários.
- `AGENTS.md` (e `AGENTS.es.md`, `AGENTS.pt.md`, `AGENTS.fr.md`, `AGENTS.de.md`): guia para colaboradores. Mantenha todas as versões de idioma sincronizadas ao alterar uma.
- `LICENSE`: GPL v3.

Dentro de `index.html`, o script tem estas partes: helpers, núcleo de idioma (`DICT`, `tr`, `applyLang`), ferramentas (`TOOLS`), grade e filtros, visor em tela cheia, teclado e entradas, página inicial, menus de tema e idioma, favicon e inicialização.

## Executar e testar

Não há build. Abra `index.html` em um navegador ou sirva a pasta com `python3 -m http.server`.

Antes de enviar alterações, verifique pelo menos:

- Não há erros no console.
- Celular (~390 px), computador (~1280 px) e TV (~1920 px) sem rolagem horizontal.
- Tema claro, escuro, preto puro e automático. Com o automático desativado, o tema fixo se mantém.
- Um navegador sem `matchMedia` usa o tema claro.
- Cada ferramenta abre em tela cheia, seus controles respondem e `Esc` fecha.
- Geometria, modo calibração: a caixa fica centralizada dentro do círculo em celular, computador e TV, e mostra resolução, densidade e escala (com `H` ocultando o painel para leitura).
- Idiomas: com o sistema em um idioma não compatível, o site usa inglês; o menu lista inglês primeiro, depois o idioma do sistema e depois os demais; a escolha se mantém ao recarregar.
- As entradas funcionam e as dicas mudam: teclado, toque (deslizar), controle remoto de TV (`ChannelUp`, `Info`, `GoBack`, e eventos somente com código 37–40/13 com User Agent de TV), gamepad (pode ser simulado substituindo `navigator.getGamepads`).
- Grade de deslizamento: arrastar pinta quadrados e não troca de teste nem fecha o visor.

O Playwright com Chromium ajuda a automatizar essas verificações.

## Convenções

- Um único arquivo, sem dependências externas nem requisições de rede. Deve abrir com um clique duplo.
- Texto da interface com `tr(texto)`. A chave é o texto em espanhol, em minúsculas exceto nomes próprios e siglas, e sem pontos de exclamação. As traduções ficam em `DICT` (uma tabela por idioma). Se faltar uma tradução, aparece o espanhol. Para adicionar um idioma: inclua-o em `SUP`, `NATIVE` e `DICT`, com todas as chaves, e adicione seu README e AGENTS.
- Cores e tema com variáveis CSS em `:root`. Nunca use cores fixas na interface; os padrões de teste usam cores exatas, porque são o produto.
- Temas: claro, escuro (cinza), preto puro (`data-theme="black"`, fundo #000) e automático. O automático com sistema escuro usa o tema escuro cinza; a caixa **Usar preto puro no modo escuro** do menu de tema troca o escuro por preto puro (`dt-oled` em `localStorage`). Não há API web para detectar OLED, então a escolha é do usuário.
- O tema padrão é claro. O modo automático depende de `prefers-color-scheme`, com `data-theme="light|dark|black"` em `<html>` somente quando o usuário fixa o tema.
- Os padrões estáticos são desenhados em SVG com `viewBox` e recebem largura e altura (`W`, `H`) para se adaptar à proporção real da tela. A miniatura usa 160×90.
- Os padrões animados (`kind:"cv"`) são desenhados em `canvas` com `init` e `frame`, e a miniatura é um SVG estático (`thumb`).
- Acessibilidade: botões reais, `aria-pressed` nos seletores, foco visível, `aria-label` nas miniaturas e respeito a `prefers-reduced-motion`.
- Persistência com `localStorage` sempre dentro de `try/catch`; o site deve funcionar sem ela. Guardam o tema (`dt-theme`) e o idioma (`dt-lang`, `auto` ou um código).
- Idioma: o automático segue `navigator.languages`, com inglês como alternativa. Os elementos estáticos usam `data-i18n`, `data-i18n-aria` e `data-i18n-title`. Ao trocar de idioma, chama-se `applyLang()`.
- Os ícones são SVG inline com `currentColor`. Não use fontes de ícones nem imagens externas: o site é um arquivo só e deve parecer igual ao ser aberto com clique duplo.
- O tema é escolhido em um menu suspenso de um ícone (`#themeBtn`, `#themeMenu`) com `role="menu"`, teclado (setas, Esc) e o ícone reflete o modo. O menu de idioma (`#langBtn`, `#langMenu`) funciona da mesma forma.
- O rodapé foi removido de propósito. Não o recoloque.
- Testes de toque: o contador de toques cria um círculo por ponto e apaga os anteriores ao tocar de novo; a grade de deslizamento pinta os quadrados cruzados pelo dedo ou pelo mouse. Na grade, os gestos de deslizar (navegar, fechar) e tocar para mostrar ou ocultar o painel estão desativados de propósito.
- Brilho de pico: o modo HDR usa `color(rec2100-pq 1 1 1)` somente se `CSS.supports` aceitar; caso contrário, mostra um aviso e branco SDR. O campo `help` de uma ferramenta (aqui `HDR_HELP`) aparece em uma seção recolhível do visor (`#vhelp`).
- `colorScale(x,y,w,h,noGray)` desenha as linhas de cor; com `noGray` omite a faixa de cinzas. O teste RGB e CMYK tem um seletor `Escala` que usa `ramp1` para mostrar uma única escala.
- Pausar/iniciar: o botão fica na linha `#vnav`, entre Anterior e Próximo (classe `playbtn`), e não no painel de controles. `clickPlay()` o procura ali.
- O cabeçalho não tem navegação por categorias; os filtros são uma linha de botões acima da grade em qualquer tamanho, sem barra lateral. Não os coloque de volta.
- Início automático: `AUTO` (`dt-auto` em `localStorage`) decide se os testes da categoria Movimento começam reproduzindo (`showTool` define `p.play`). O desentupidor de pixels fica de fora e sempre começa pausado.
- Painel do visor: `kick()` oculta `#vc` após 5 s sem entrada, exceto na grade de deslizamento. Qualquer tecla ou movimento do mouse o mostra de novo.
- Controles condicionais: um controle com `when:{k,v}` aparece só quando `p[k]===v`. Uma opção com `rb:true` reconstrói o painel ao mudar; é assim que funcionam os modos.
- Helpers compartilhados de padrões: `smpteSvg`, `grayStrip`, `colorScale`, `contrastSvg`, `geoBase`, `screenInfo`, `starCount` e `newStar`. Reutilize-os em vez de duplicar o desenho.
- Todas as entradas (teclado, mouse, toque, controle remoto, gamepad e joystick) passam pelo despachante `act(ação, nativo)`, com as ações `left`, `right`, `up`, `down`, `confirm`, `back`, `next`, `prev`, `toggle` e `playpause`. Para suportar um dispositivo novo, mapeie-o para essas ações; não adicione manipuladores soltos.
- `INPUT` guarda a última entrada detectada (`keyboard`, `mouse`, `touch`, `remote`, `gamepad`) e é refletida em `data-input` no `<html>`. As dicas do visor (`hintHtml`) dependem desse valor. Se adicionar uma ação, adicione a dica para todas as entradas.
- Teclas do controle remoto: `keyAction` aceita o nome (`ArrowLeft` ou `Left`) e também o código numérico (37–40, 13). Algumas TVs enviam só o código; não remova esse recurso de reserva.
- Aviso de fotossensibilidade: o geral fica acima da grade. Os testes de movimento ou mudança de cor têm `warn` e o exibem no visor (`#vwarn`) com a mesma classe `.warn` da página inicial.
- Botões do visor (`#vc .btn`), botão de pausa e botões selecionados: azul dos controles deslizantes `#85b7eb` com texto preto (os demais, brancos com texto preto). As teclas de dica (`kbd`) são brancas com texto preto e planas, sem relevo inferior.
- Favicon: ícone de monitor igual ao do cabeçalho. `setFav()` o regenera como `data:` conforme `prefers-color-scheme` (preto no claro, branco no escuro) e o atualiza quando o sistema muda. Não use `media` nos links de ícone: os navegadores não o aplicam de forma confiável.
- As teclas nas dicas são escritas com `<kbd>` (classes `r` para controle remoto e `g` para gamepad) para ficarem dentro de uma caixa.
- A navegação espacial (`spatial`) só é ativada com foco em um elemento (teclado e mouse) ou sempre (controle remoto e gamepad), para não tirar a rolagem com setas de quem usa teclado.

## Regras de segurança

- Sem flashes nem piscar automático. O movimento é moderado e o aviso de fotossensibilidade deve continuar visível.
- A velocidade do ghosting fica limitada a 2–6 s por passagem. Não desça abaixo de 2 s.
- O desentupidor de pixels começa pausado. Cada quadrado muda de cor ao acaso e por conta própria, com intervalo médio de 10 s a 0,1 s (velocidades 1–16) e variação de ±40 %; os quadrados são reprogramados ao mudar a velocidade para nunca mudarem juntos. Acima de 3 mudanças por segundo (velocidade 13 ou mais) são forçadas pelo menos 8 colunas, para que o piscar não se concentre em poucos quadrados, e o rótulo marca "rápido". Não remova esse limite nem aumente a velocidade sem avisar o dono do projeto.
- O teste de ghosting e smearing (`respuesta`) começa pausado e mostra o aviso de fotossensibilidade.
- Os controles do visor devem poder ser ocultados, para não contaminar os testes de uniformidade.

## Adicionar uma ferramenta

1. Adicione um objeto a `TOOLS` com `id`, `name`, `cat`, `desc`, `p` (parâmetros padrão), `ctl` (controles, opcional) e `draw(p, W, H, live)` que retorna o SVG. Se for animada, use `kind:"cv"` com `init`, `frame` e `thumb`.
2. Se for uma categoria nova, adicione-a a `CATS`.
3. Os controles podem ser `range` (`min`, `max`, `step`, `fmt`), `choice` (`opts`), `preset` (atalhos para um valor) ou `play` (iniciar e pausar).
4. Adicione cada texto visível em espanhol a todos os idiomas de `DICT`, e atualize a tabela de ferramentas de `README.md` e suas traduções.
5. Revise o site com a lista de testes acima.

## Commits

Mensagens curtas em espanhol ou inglês, no imperativo, com uma linha de resumo. Uma mudança por commit quando possível.
