# VIGU Sinuca Arena 🎱

Jogo de sinuca com regras inspiradas em 8-ball feito em **HTML, CSS e JavaScript puro**, sem frameworks e sem dependências externas. Foi pensado para rodar diretamente no navegador e ser publicado gratuitamente no **GitHub Pages**.

## Recursos

- Mesa de sinuca renderizada em `<canvas>`.
- Física de bolas, colisões, atrito, bordas e caçapas.
- Mira com mouse e toque.
- Tacada por gesto: segure, puxe o taco para trás e solte.
- A força é proporcional à distância puxada.
- CPU com quatro níveis:
  - Fácil
  - Médio
  - Difícil
  - HARDCORE
- O HARDCORE só é desbloqueado depois de vencer uma partida em cada um dos três níveis iniciais.
- Progresso salvo no `localStorage` do navegador.
- Interface responsiva para computador, tablet e celular.
- Efeitos sonoros próprios para tacada, colisão, tabela, caçapa, vitória e derrota.
- Projeto 100% estático, ideal para GitHub Pages.

## Controles

- **Desktop:** mova o mouse para mirar. Clique e segure na mesa, arraste na direção oposta à mira para puxar o taco e solte para disparar.
- **Celular/tablet:** toque na direção em que deseja mirar, mantenha o dedo pressionado, arraste para trás e solte.
- Um clique/toque curto apenas ajusta a mira e não dispara acidentalmente.

## Como jogar localmente

Basta abrir `index.html` no navegador.

Para evitar restrições de alguns navegadores, você também pode rodar um servidor local:

```bash
python3 -m http.server 8080
```

Depois acesse `http://localhost:8080`.

## Publicar no GitHub Pages

1. Crie um repositório no GitHub, por exemplo `vigu-sinuca-arena`.
2. Envie os arquivos deste projeto para a branch `main`.
3. No repositório, abra **Settings → Pages**.
4. Em **Build and deployment**, selecione **Deploy from a branch**.
5. Selecione a branch `main` e a pasta `/ (root)`.
6. Clique em **Save**.
7. Depois de alguns instantes, o GitHub mostrará a URL pública do jogo.

## Observação sobre as regras

O jogo segue uma versão simplificada das regras de 8-ball, adequada para partidas rápidas contra a CPU:

- A primeira bola válida encaçapada define lisas/listradas.
- Depois de limpar seu grupo, você deve encaçapar a bola 8.
- Encaçapar a bola 8 antes da hora causa derrota.
- Encaçapar a bola branca causa falta e ela é recolocada automaticamente.

## Estrutura

```text
vigu-sinuca-arena/
├── index.html
├── style.css
├── script.js
├── sounds/
│   ├── cue.wav
│   ├── collision.wav
│   ├── rail.wav
│   ├── pocket.wav
│   ├── ui.wav
│   ├── win.wav
│   └── lose.wav
└── README.md
```

## Licença

Você pode usar, modificar e publicar este projeto no seu GitHub.

## Ajuste de física da V5

- Tacadas em 100% agora preservam muito mais energia em percursos longos.
- O atrito de rolamento foi recalibrado para não fazer a bola branca "morrer" antes de atravessar a mesa.
- O critério de parada usa velocidade visual compensada pela proporção da mesa, mantendo o comportamento consistente em qualquer ângulo.
- A potência máxima recebeu um pequeno reforço sem alterar o gesto de puxar e soltar o taco.


## V6 — modo mobile horizontal

A gameplay em celular foi otimizada para paisagem:

- Ao iniciar uma dificuldade em um dispositivo touch, o jogo tenta entrar em tela cheia e solicitar orientação `landscape`.
- Em navegadores que permitem `screen.orientation.lock("landscape")`, a rotação acontece após o toque que inicia a partida.
- Se o navegador não permitir bloqueio automático de orientação, aparece uma tela orientando o jogador a girar o aparelho; ao virar o celular, a partida é liberada automaticamente.
- Durante a partida em paisagem, a barra superior é ocultada e HUD, mesa e controles são compactados para ocupar praticamente todo o viewport.
- O `manifest.webmanifest` define `orientation: landscape` para uso quando o jogo for instalado como web app/PWA.

> Observação: navegadores móveis não permitem que uma página comum force rotação de tela no carregamento sem interação do usuário. Por isso a V6 usa fullscreen + Screen Orientation API quando disponível e um fallback visual quando não estiver.


## V7 — correção definitiva da puxada no touch

- A mira não gira mais quando o jogador toca no taco para puxá-lo.
- O toque na região atrás da bola branca, onde o taco está desenhado, preserva a direção atual.
- Durante a puxada, o ângulo fica completamente travado.
- Movimento lateral involuntário do dedo é ignorado para a direção da tacada.
- Tocar em outra região da mesa continua permitindo escolher uma nova direção.
- Mouse/desktop mantém o comportamento anterior.


## V8 — turnos corretos e celulares compactos

### Turnos
- Se o jogador encaçapar uma bola válida sem cometer falta, ele continua jogando.
- A CPU só recebe a vez quando o jogador não encaçapa uma bola válida ou comete uma falta.
- A mesma regra vale para a CPU.
- É possível encaçapar todas as bolas em sequência sem o adversário jogar, desde que não haja erro.
- A validação da primeira colisão agora usa o estado da mesa no início da tacada, evitando faltas falsas logo após a definição de lisas/listradas.
- Encaçapar a última bola do grupo e a bola 8 na mesma tacada não conta como finalização válida; o jogador precisa já estar na bola 8 antes da tacada.

### Mobile compacto
- HUD forçado para uma única linha durante gameplay horizontal.
- Correção do conflito com o breakpoint de 640px que aumentava a altura do HUD.
- Layout específico para telas próximas de 568×320 e 640×360.
- Controles laterais mais estreitos e compactos.
- Melhor respeito às safe areas e ao viewport disponível.


## V9 FINAL — responsividade universal e gameplay mais rápida

### Responsividade
- O painel de força não depende mais de breakpoints de modelos específicos.
- Em landscape mobile, "FORÇA DA TACADA" vira automaticamente "FORÇA".
- O medidor de potência usa o espaço vertical restante, em vez de uma altura fixa.
- O layout usa `VisualViewport` para respeitar o espaço realmente disponível quando o navegador/Android mantém barras visíveis.
- Em painéis extremamente estreitos, os botões preservam os ícones e ocultam o texto antes de cortar o layout.
- O canvas usa DPR reduzido em dispositivos touch para melhorar desempenho em celulares mais simples.

### Ritmo da partida
- O atrito agora é dinâmico: tacadas fortes preservam alcance, enquanto movimentos finais muito lentos param rapidamente.
- O próximo turno é liberado assim que o movimento deixa de ser perceptível.
- O tempo de decisão visual da CPU foi reduzido.
- A simulação passou de 180 Hz para 120 Hz, mantendo estabilidade de colisão e reduzindo carga de CPU em mobile.
