# assets/ravendawn/

Dump organizado dos assets oficiais do cliente Ravendawn (extraidos da pasta
`RAVENDAWN/data` do OTClient), importados em 2026-09-04 para reaproveitar na
Elemental Online. Tudo aqui é referencia/matéria-prima — nada foi conectado
ainda ao código do jogo (server.js / world-prototype.html / character-select.html).

## icons/
- `abilitybar/` (711 png) — um icone por habilidade/pocao/item de acao (nome
  do arquivo = nome da skill/item, ex: `fireball.png`, `bloodlust.png`).
- `archetypes/` (100 png) — os 10 arquetipos/classes do Ravendawn (archery,
  ballistics, holy, naturalist, protection, shadow, spiritual, warfare,
  witchcraft, wizardry), em 5 tamanhos (20x20 ate 175x175) + versao
  `_disabled`. Ideal pra tela de criacao de personagem / selecao de classe.
- `channeling/` (21 png) — icones de "cast" de magias especificas
  (bladestorm, blizzard, meteor strike, rain of arrows, holy force, etc).
- `status/` (301 png) — icones de buff/debuff. Muitos tem o nome da criatura
  no arquivo (ex: `berserk_dire_bear.png`, `bullrush_boar_runt.png`,
  `hex_bone_gazer.png`) — cruzam direto com os monstros já usados em
  `huntEngine.js`.

## items/
- `ui_icons/` (1126 png) — icones de item, nomeados por ID numerico do item
  (precisa cruzar com items.xml/items.otb pra saber o nome de cada um).
- `ui_misc/` (9 png) — icones genericos de UI de item (slot vazio, etc).

## ui/
- `windows/` (6961 arquivos, 82 subpastas) — HUD/telas completas do jogo:
  `character/`, `crafting/`, `achievements/`, `arena/`, `dialogue/`, `chat/`,
  `trade/`, `guild/`, `spelltree/` (arvore de habilidades, pesado ~159MB),
  `ravencards/` (arte das cartas colecionaveis, ~324MB), `house/`,
  `professions/`, `worldmap/`, etc. Cada subpasta = uma janela/funcionalidade.
- `ravencards/` (344 png) — versao "resumo" dos ravencards (fora da pasta
  windows).
- `pets/` (66 png), `portraits/` (3 png — bandit, lord shopan),
  `bars/` (22 png — barras de vida/mana), `buttons/`, `checkbox/`,
  `dropdown/`, `loading/` (telas de carregamento), `misc/`.

## game/
- `adornments/` — molduras/efeitos cosmeticos de perfil (battleborn,
  cinderskull, exalted_wings, etc — 10 conjuntos).
- `bars/`, `targetselector/` — elementos de HUD de combate.

## styles/
Arquivos `.otui` — os layouts de UI reais do OTClient (posicao, tamanho,
anchors de cada elemento). Nao sao imagem, sao texto/markup. Uteis como
referencia de como a Ravendawn organiza a propria interface.

## fonts/
333 arquivos de fonte usados no cliente.

## particles/
`particle.png` + `particles.otps` (definicao de efeitos de particula do
OTClient).

## raw_textures/
Texturas grandes ainda **comprimidas em formato KTX** (nao abrem direto como
imagem normal — precisam de conversao, ex: via `ktx2ktx2`/`toktx` ou uma lib
tipo `three.js` KTX loader antes de virarem PNG usavel na web):
- `floor8..15_l/_m.ktx` — texturas de piso por andar.
- `minimap_l/_m.ktx`, `aether_rift*.ktx`, `guild_wars.ktx`,
  `tutorial_p1/p2_l/_m.ktx` — telas/backgrounds grandes.
- `background.mp4` — video de fundo do launcher/tela de login.
- `client_icon*.png`, `ravenquest_full.png`, `ravenquest_sword.png`,
  `rq_client_icon*.png` — logos/icones do launcher.

## cursors/
5 arquivos de cursor do mouse (formato nativo do OTClient/Windows).

---
**Tamanho total: ~1GB** (a maior parte em `raw_textures/` e
`ui/windows/ravencards|spelltree`). Antes de dar push, vale considerar se
esses dois pesos grandes (ravencards art + texturas KTX) realmente precisam
ir pro repositorio agora ou se dá pra deixar de fora numa primeira leva.
