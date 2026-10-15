# 🏛️ Arquitetura Gráfica 3D (Three.js)

Este documento detalha as decisões técnicas, modelos matemáticos e recursos visuais utilizados na construção da **Galeria Neoclássica da Gessy**.

---

## 1. Tela Inicial de Abertura & Contagem Regressiva

- **Cenário Acolhedor (`fundo_abertura.jpg`):**
  - Fundo em alta resolução otimizado para web e LittleFS (~94 KB) com textura têxtil, café, velas e fotografias polaroids.
  - Camada de sobreposição em gradiente escuro translúcido com *backdrop-filter: blur* para garantia de legibilidade e aconchego visual.
- **Tipografia:**
  - `Great Vibes` para o nome cursivo *"Gessy, ♡"*.
  - `Cormorant Garamond` itálico clássico para as citações e mensagens românticas.
  - `Montserrat` com tracking espaçado para rótulos e numerais do cronômetro.
- **Trava de Segurança (Controle de Acesso):**
  - Botão de entrada com estado bloqueado `[ 🔒 Aguardando a data especial... ]` com cursor `not-allowed`.
  - Impede a entrada mesmo com persistência de sessão até a data comemorativa (`2026-10-20`).
  - Desbloqueio transparente ao zerar o cronômetro ou ao anexar o parâmetro `?preview=1` na URL.

---

## 2. Estrutura do Salão (Rotunda Neoclássica 360°)

- **Raio da Rotunda:** $7.5\text{ metros}$.
- **Altura do Pé-Direito:** $4.2\text{ metros}$.
- **Piso:** Mármore nobre de Carrara polido com tapete anelar aveludado bordô ($r \in [2.65\text{ m}, 4.40\text{ m}]$) e filetes duplos em ouro polido.
- **Paredes:** Revestimento clássico marfim fosco com rodapé e cornijas superiores esculpidas em mármore.
- **Óculo Zenital no Teto:** Claraboia circular ($R = 2.6\text{ m}$) emoldurada em ouro com vista para o céu noturno, com lua e halo concentrados exatamente no centro geométrico `(256, 256)`.

---

## 3. Ponto de Spawn e Cena Inicial

- **Spawn:** Câmera posicionada em `(0, 1.70, -3.60)` sobre a passadeira de veludo da entrada.
- **Enquadramento:** `yaw = 0` (voltada para o eixo $-Z$) e `pitch = +0.06`, enquadrando perfeitamente o grande painel comemorativo:
  - *"♥ ♥ ♥"*
  - *"Feliz Aniversário, Gessy!"*
  - *"Cada dia ao seu lado é uma memória inesquecível."*
- **Aparador Neoclássico:**
  - Tampo de mármore branco com moldura de ouro e pernas caneladas.
  - Dois candelabros de ouro com 3 velas acesas que permanecem emitindo luz mesmo no escuro.
  - Vaso ornamental posicionado à direita ($x = +0.50$) com rosas vermelhas botânicas aveludadas e pratinho decorativo à esquerda ($x = -0.50$), garantindo visão 100% desobstruída para a parede.
- **Interruptor 3D de Parede (*Vintage Tumbler Switch*):**
  - Espelho de latão polido gravado *"LUZES 💡 ON / OFF"*.
  - Alavanca móvel com articulação física ($+28^\circ$ ligada, $-28^\circ$ desligada).
  - Gera estalo mecânico via Web Audio API e apaga as luzes gerais do palácio para um clima intimista de velas e céu estrelado.

---

## 4. Canteiro Central, Altar & Presente Flutuante

- **Canteiro Floral:**
  - Mureta cilíndrica de mármore e gradil clássico dourado aberto frontalmente.
  - Solo orgânico de terra fértil e musgo elevado em $y = 0.41\text{ m}$.
  - InstancedMesh com 380 tufos de grama volumétrica em 5 tonalidades botânicas.
  - 44 flores botânicas realistas (24 rosas aveludadas e 20 gérberas multicoloridas).
- **Altar Neoclássico:**
  - Pedestal escalonado em mármore Carrara e aros de ouro maciço ($y = 0.41\text{ m}$ a $0.51\text{ m}$).
  - Mandala dourada radiante procedural girando suavemente no topo.
  - Fonte de luz ascendente (*uplight* âmbar `0xffdd88`) e feixe volumétrico místico sob o presente.
- **Caixa de Presente Flutuante:**
  - Flutuação senoidal suave com partículas douradas orbitando.
  - Laço tridimensional de luxo com nós volumétricos e caudas fluidas.
  - Interativa: ao tocar, revela a Cartinha Secreta 💌.

---

## 5. Otimização e Performance (60 FPS no Celular)

1. **InstancedMesh:** Corações e tufos de grama utilizam geometria instanciada, reduzindo centenas de draw-calls para apenas 2 chamadas de renderização.
2. **Texturas Procedurais:** Mármore, letreiro, óculo celestial e mandala gerados em código via Canvas 2D, eliminando dezenas de megabytes de download de imagens.
3. **Colisão OBB (Oriented Bounding Boxes):** Colisores físicos nos bancos de veludo com resposta de deslizamento suave (*sliding collision*).
4. **Gerenciamento de Modelos GLTF:** Carregamento assíncrono via `GLTFLoader` com cache de templates clonados e normalização de escala por `Box3`.
