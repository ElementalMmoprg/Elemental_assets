# Tibia Classic Tileset — atlas de chão/cenário

`assets/tilesets/tibia_tileset_atlas.png` + `tibia_tileset_atlas_manifest.json`
(na raiz do `Elemental_assets/assets/tilesets/`).

## O que é

Todos os items do `tibia.dat` cujo ID está entre **100 e 3199** — a faixa que,
ao inspecionar visualmente, corresponde a chão, água, grama, paredes de
caverna, pontes, tendas de mercado, tochas, teias, plantas etc. (a mesma
convenção de ordenação de IDs que a Tibia clássica sempre usou). A partir do
ID ~3200 o conteúdo vira equipamento/roupa/comida, que não interessa pro
"novo visual do mapa".

De cada um desses ~3.100 items, decodifiquei os pixels reais de dentro do
`tibia.spr` (RLE + alpha) e montei a imagem final de cada um — inclusive os
que ocupam mais de 1×1 tile (ex: árvores 2×2), respeitando a forma como a
Tibia empilha essas peças (ancoradas no canto inferior direito, crescendo
para cima/esquerda). Quando um item tem variações (ex: 4 rotações de uma
quina de parede), cada variação virou uma sub-imagem separada no atlas
(`_v0`, `_v1`, ...). Para items animados (água, lava, tocha), só a **primeira
fase** da animação foi usada — as demais fases já estão mapeadas em
`tibia_data.json` (`fg.sprites`) caso queira animar depois.

Tudo isso foi empacotado num único PNG (atlas) de 2048×5536 em vez de ~4.800
arquivos soltos — mais rápido de carregar no jogo (uma requisição só) e mais
rápido de eu conseguir escrever na sua máquina (escrever milhares de
arquivinhos petalados por pasta sincronizada é extremamente lento).

## Formato do manifest

```jsonc
{
  "103": { "x": 0, "y": 96, "w": 64, "h": 32 },
  "104_v2": { "x": 64, "y": 96, "w": 32, "h": 64 },
  ...
}
```

Chave = `<itemId>` (ou `<itemId>_v<N>` quando o item tem múltiplas variações
de padrão). `x,y,w,h` = retângulo dentro do `tibia_tileset_atlas.png` de onde
recortar aquele sprite (em pixels, já na escala 1:1, sem upscaling).

Pra desenhar no canvas:
```js
const rect = tibiaAtlasManifest[itemId];
ctx.drawImage(tibiaAtlasImage, rect.x, rect.y, rect.w, rect.h, destX, destY, rect.w, rect.h);
```

## Limpeza pendente (preciso da sua ajuda aqui)

Numa tentativa anterior eu tentei copiar os ~4.800 PNGs soltos direto pra sua
pasta do GitHub antes de decidir usar o atlas — isso travou no meio do
caminho (escrever muitos arquivos pequenos numa pasta sincronizada é lento) e
sobraram pastas incompletas e inúteis dentro de
`Elemental_assets/assets/tilesets/`:

- `tiles_full/` (pasta com PNGs soltos, incompleta)
- `tibia-classic/` (pasta com PNGs soltos, incompleta)
- `tiles_full.zip`

Pedi permissão pra apagar isso automaticamente, mas o sistema bloqueou a
ação de exclusão em lote por segurança. Pode apagar essas três coisas
manualmente (Explorer → `Elemental_assets\assets\tilesets\` → seleciona as
duas pastas e o zip → Delete)? O atlas (`tibia_tileset_atlas.png` +
`tibia_tileset_atlas_manifest.json`) já está completo e correto, essas
pastas são só lixo da tentativa anterior.
