# Cidade Elemental — dados da cidade principal

`city_elemental.json` é a "Cidade Elemental" extraída do `town.otbm` que você
mandou (feito no Remere's Map Editor com os assets do Revendawn).

## Importante: por que o visual não é pixel-a-pixel igual ao que você desenhou

O `town.otbm` guarda, para cada tile, **IDs de servidor** (da tabela
`items.otb` do Revendawn) — não o índice real do `tibia.dat`. Sem o
`items.otb` (ou `items.xml`) do Revendawn pra traduzir "ID do mapa → sprite
do cliente", não dá pra saber com certeza qual sprite cada ID do mapa deveria
usar (testei — sem essa tradução, o chão mais comum do seu mapa vira um
ícone de escudo, os "pilares" do templo viram pedras preciosas etc, tudo
errado). Você confirmou que não tem esse arquivo.

Por isso, ao invés de adivinhar sprite por sprite (o que ia inventar visual
que não é a estética Tibia/Revendawn), eu preservei a **estrutura real** do
seu mapa (formato da cidade, posição exata do templo, dos pilares, do
teleporte) e apliquei por cima um pequeno conjunto de tiles **reais e já
validados** do `tibia.dat` (os mesmos do atlas em
`../tilesets/tibia_tileset_atlas.png`):

- Chão principal da cidade → tile 2656 (pedra de praça)
- Chão secundário/prédios → tile 796
- Chão do templo (e das outras salas que usavam o mesmo piso) → tile 1408
- Pilares/tochas do templo (id 22280–22291 do mapa, confirmados visualmente
  como um padrão simétrico ao redor do centro) → tile 628 (tocha), bloqueia
  passagem
- Ponto de spawn (id 407 do mapa, exatamente 1 tile, no centro do templo) →
  marcado como `"s":"spawn"` em `(1044, 1051)`
- Teleporte (item real do OTBM com atributo de teleporte, id 17868, a 3 tiles
  do templo) → tile 1000 (azul), marcado como `"s":"teleport"` em
  `(1044, 1048)`

Se um dia você conseguir o `items.otb`/`items.xml` do Revendawn, eu refaço
esse arquivo com o visual exato que você desenhou no editor, sem perder nada
da lógica (spawn/teleporte/hunts) que for construída em cima disso.

## Formato

```jsonc
{
  "meta": {
    "minX":988,"maxX":1076,"minY":1008,"maxY":1094, "z":5,
    "spawn": {"x":1044,"y":1051},
    "teleport": {"x":1044,"y":1048},
    "atlasImage":"tibia_tileset_atlas.png",
    "atlasManifest":"tibia_tileset_atlas_manifest.json",
    "tileSizePx":32
  },
  "tiles": [
    {"x":988,"y":1008,"g":796}',            // só chão
    {"x":1042,"y":1046,"g":1408,"d":[628],"b":1}, // chão + tocha, bloqueado
    {"x":1044,"y":1051,"g":1408,"s":"spawn"},     // spawn do jogador
    {"x":1044,"y":1048,"g":1000,"s":"teleport"}   // teleporte azul
  ]
}
```

`g` = id do tile de chão (procurar em `tibia_tileset_atlas_manifest.json`
pelo retângulo dentro do atlas). `d` = lista de ids de decoração empilhados
por cima (mesma lógica). `b:1` = tile bloqueado (não anda). `s` = papel
especial do tile (`spawn` ou `teleport`).

`city_preview.png` é um render de conferência (não é pra usar no jogo).
