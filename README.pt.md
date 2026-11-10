[English](README.md) · [Español](README.es.md) · **Português** · [Français](README.fr.md) · [Deutsch](README.de.md)

# DisplayTests

Site com ferramentas para testar e diagnosticar telas de celulares, computadores e televisores. É um único arquivo, `index.html`, sem dependências nem etapa de compilação.

## Uso

Abra o `index.html` em um navegador (clique duplo) ou publique-o em qualquer hospedagem estática, por exemplo o GitHub Pages. Toque em uma miniatura para abrir o teste em tela cheia.

Para medir, ajuste o brilho da tela, use tela cheia e, nos testes de preto, um quarto escuro. As cores mostradas são uma aproximação.

## Destaques

**Ferramentas de teste**

| Ferramenta | Categoria | Para que serve |
| --- | --- | --- |
| Barras SMPTE | Cor | Verificar cor, brilho e níveis de preto |
| Escala de cinza | Cor | Ver se os tons escuros e claros se distinguem |
| Pretos baixos | Cor | Barras de 0 a 8 % sobre preto para ver se a TV esmaga as sombras ou eleva o preto (quarto escuro) |
| Escala RGB e CMYK | Cor | Seis escalas de dez passos, uma por cor (vermelho, verde, azul, ciano, magenta e amarelo). Escolha em Escala se quer vê-las todas ou apenas uma |
| Brilho de pico | Cor | Janela branca de 10 a 100 % da área sobre preto, para medir o brilho de pico; faixa SDR ou HDR. HDR exige navegador e tela compatíveis, e o visor explica como ativá-lo |
| Contraste | Cor | Blocos de 5 % a 95 % com nível ajustável |
| Uniformidade cinza | Uniformidade | Cinza de 0 a 100 % com atalhos para preto e branco: manchas, vinheta, vazamento de luz, nuvens e faixas |
| Uniformidade RGB e CMYK | Uniformidade | Uma cor em tela cheia por vez (vermelho, verde, azul, ciano, magenta, amarelo, branco e preto), escolhida manualmente. Também serve para achar pixels mortos |
| Contador de toques | Tátil | Um círculo colorido por ponto de toque; permanecem ao soltar e são apagados ao tocar a tela de novo. Conta os toques simultâneos e o máximo |
| Grade de deslizamento | Tátil | Grade ajustável que pinta os quadrados cruzados pelo dedo ou pelo mouse, com a porcentagem coberta |
| Desentupidor de pixels | Pixels | Grade quadrada adaptável cujos quadrados mudam ao acaso entre RGB, CMYK, branco e preto, cada um no seu tempo; tamanho (4–25 % da largura) e velocidade (1–16, de a cada 10 s a a cada 0,1 s) ajustáveis |
| Atenuação local | Movimento | Estrelas de vários tamanhos em movimento sobre preto para detectar halos e atenuação local (local dimming); velocidade e densidade ajustáveis; tamanho das estrelas ajustável |
| Smearing (VA) | Movimento | Uma barra branca se move sobre fundos escuros para mostrar o rastro escuro ou claro dos painéis VA; velocidade e fundo ajustáveis, com pausa |
| Texto em movimento | Movimento | Linhas de texto que rolam em sentidos opostos. Em painéis VA o texto em movimento borra ou deixa rastro; compare a nitidez parado e em movimento. Velocidade ajustável, com pausa |
| Ângulos de visão | Uniformidade | Cinzas, cores ou tons escuros para ver como mudam ao olhar dos lados, de cima ou de baixo; escolha o padrão na opção Visão |
| Nitidez do texto | Nitidez | Texto em vários tamanhos, com serifa, monoespaçado e colorido, sobre branco e sobre preto, para verificar a nitidez em telas de pixel branco (como W-OLED) |
| Ghosting | Movimento | Rastros por tempo de resposta lento; passagem de 2 a 6 s |
| Overscan e margens | Nitidez | Quadros a 0, 2, 5 e 10 % das bordas para ver se a imagem é cortada (principalmente em TVs) |
| Linhas finas | Nitidez | Linhas de um pixel real para detectar escalonamento, borrão e moiré |
| Geometria | Nitidez | Grade, círculo e diagonais para proporções e foco |
| Geometria e calibração | Nitidez | O mesmo, com uma caixa central dentro do círculo que reúne barras SMPTE, escala de cinza, escala RGB e CMYK e contraste, e mostra resolução, densidade e escala da tela; com a diagonal informada calcula os ppp |

**Site**

- **Responsivo:** 2 colunas no celular, 3 em tablets, 4 no computador com filtros em uma barra lateral e 5 em TVs com texto maior.
- **Visor em tela cheia:** cada teste se adapta à proporção real da tela. Os controles são ocultados com `H` ou tocando na tela, para não contaminar os testes de uniformidade.
- **Várias entradas:** teclado, mouse, telas sensíveis ao toque, controles remotos de TV, gamepads e joysticks. As dicas de controle do visor se adaptam à entrada detectada, e as teclas aparecem dentro de uma caixa para se destacar. Veja a seção Controles.
- **Tema automático:** segue o modo claro ou escuro do sistema no Android, iPhone, Windows, macOS e Linux. Com o sistema no escuro, usa o tema escuro cinza, ou preto puro se você marcar a opção no menu de tema. Se o dispositivo não informar, usa o tema claro.
- **Menu de tema:** um único ícone no cabeçalho abre um menu com Automático, Claro, Escuro e Preto puro, e o ícone mostra o estado. Claro, Escuro e Preto puro fixam o tema e desativam o acompanhamento do sistema. Abaixo, a caixa **Usar preto puro no modo escuro** faz o tema escuro usar preto puro, o melhor para telas OLED. A preferência fica salva no navegador.
- **Idiomas:** inglês, espanhol, português, francês e alemão. O idioma é escolhido automaticamente pelo idioma do sistema; se não for compatível ou não puder ser detectado, usa inglês. O ícone de globo, à esquerda do tema, permite trocar manualmente.
- **Filtros por categoria:** Cor, Uniformidade, Pixels, Movimento, Nitidez e Tátil.
- **Segurança:** aviso para pessoas fotossensíveis, movimento sem flashes e um desentupidor de pixels que começa pausado, com mudanças de cor aleatórias e independentes por quadrado. A partir da velocidade 13 (mais de 3 mudanças por segundo) a grade tem pelo menos 8 colunas e um aviso é exibido.

## Controles

O site detecta a última entrada usada e muda as dicas do visor de acordo.

| Ação | Teclado | Toque | Controle remoto | Gamepad ou joystick |
| --- | --- | --- | --- | --- |
| Trocar de teste | `←` `→` | Deslizar para os lados, ou botões Anterior e Próximo | `◀` `▶`, `CH+` `CH−` | `◀` `▶`, `LB` `RB` |
| Ir aos controles | `↓` (e `↑` para voltar) | Tocar no controle | `▼` (e `▲` para voltar) | `▼` (e `▲` para voltar) |
| Ajustar um controle | `←` `→` em um deslizador | Arrastar | `◀` `▶` | `◀` `▶` ou analógico esquerdo |
| Mostrar ou ocultar o painel | `H` | Tocar na tela | `OK` ou `Info` | `Start` |
| Iniciar ou pausar | `Espaço` | Botão Pausar/Iniciar entre Anterior e Próximo | `⏯` | `X` |
| Aceitar | `Enter` | Tocar | `OK` | `A` |
| Fechar | `Esc` | Deslizar para baixo | `Voltar` | `B` |

No teste de grade de deslizamento, os gestos não trocam de teste nem fecham o visor, e tocar não oculta o painel, para que você possa pintar livremente. Use o botão Fechar, `Esc` ou `H` nesse teste.

Na página inicial, controles remotos e gamepads se movem entre botões, filtros e miniaturas com as setas (navegação espacial). Em TVs com Tizen, webOS, Android TV, Fire TV e similares, o site começa com as dicas de controle remoto. Os gamepads são detectados ao pressionar qualquer botão.

## Compatibilidade

Navegadores atuais no Android, iPhone, Windows, macOS e Linux, e navegadores de TVs inteligentes com suporte moderno a CSS e JavaScript.

## Colaborar

Veja [AGENTS.pt.md](AGENTS.pt.md) para a estrutura, as convenções e como adicionar uma nova ferramenta.

## Licença

GNU GPL v3. Veja [LICENSE](LICENSE).
