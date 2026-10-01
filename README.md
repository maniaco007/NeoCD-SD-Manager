# NeoCD SD Manager

**[English](README.en.md)**

**Aplicativo para Windows que deixa o cartão SD do Neo Geo CD (Neo CD SD Loader — BR Edition) pronto em poucos cliques: instala o menu, dá o nome certo a cada jogo e gera a capa de cada um.**

Um projeto do blog **[Maniaco Game Room](https://www.maniacogameroom.com.br/)**.

![Lista de jogos com a capa ao lado](imagens/menu-lista-capa.png)

## Como funciona

Você coloca o cartão SD no PC, com os jogos já nele, abre o aplicativo e clica em **Preparar cartão**. Ele:

1. **instala o menu BR Edition** no cartão (copia o arquivo de atualização e confere a cópia);
2. **organiza o nome dos jogos:** identifica cada pasta pelo nome (e, se você quiser, pelo conteúdo do disco, comparando com o banco Redump) e renomeia com o título certo, por exemplo `metal_slug_2 [!]` → `Metal Slug 2`;
3. **gera a capa de cada jogo** (`bg.bmp`), pronta para o console, usando as suas imagens ou baixando da internet.

![Aplicativo](imagens/app-preparar.png)

| | |
|---|---|
| ![Jogos e capas](imagens/app-jogos.png) | ![Capa no console](imagens/menu-capa.png) |

**O menu no console:**

| | | |
|---|---|---|
| ![Menu principal](imagens/menu-principal.png) | ![Configurações](imagens/menu-configuracoes.png) | ![Créditos](imagens/menu-creditos.png) |

- **Nada é apagado:** os nomes antigos podem ser restaurados (botão **Desfazer último**) e o que for substituído no cartão vai para a pasta `_neocd-manager`.
- **Prévia fiel:** ao clicar num jogo, você vê a capa como o console vai mostrar (cores reduzidas, mesmas paletas).
- **Português ou inglês:** menu **Idioma / Language**, com temas de cor para a janela.

## Como usar

1. Baixe o **`NeoCD-SD-Manager.exe`** na página de **[Releases](../../releases)**.
2. Coloque o cartão no PC (formatado em **FAT32**), com cada jogo em uma pasta que tenha o arquivo `.cue`.
3. Abra o aplicativo, escolha o cartão e clique em **Preparar cartão**.
4. Coloque o cartão no console e ligue.

Passo a passo completo, com todas as opções: **[Manual do aplicativo](MANUAL.md)**.

## Requisitos

- Neo Geo CD com o **Neo CD SD Loader** instalado (kit do Furrtek).
- Windows 10 ou 11.
- Cartão SD em **FAT32**, com até **200 jogos** (limite do menu).
- Internet na primeira vez (bancos de nomes e capas são baixados e ficam guardados no PC).

## Aviso

Este projeto **não fornece jogos nem BIOS**. O arquivo de atualização do menu incluído (`NSDL0014.WAD`) é software livre (GPL) baseado no Neo CD SD Loader de Furrtek e contém apenas os patches do loader, sem a BIOS do console; o código-fonte está em [NeoCDSDLoader-BR-Edition](https://github.com/maniaco007/NeoCDSDLoader-BR-Edition). Este projeto não é afiliado à SNK nem a Furrtek. Use por sua conta e risco.

## Créditos

- Neo CD SD Loader (hardware, firmware e menu originais): **Furrtek** — [furrtek.org/sdloader](http://www.furrtek.org/sdloader/)
- Capas: [libretro-thumbnails](https://github.com/libretro-thumbnails)
- Bancos de jogos (Redump): [libretro-database](https://github.com/libretro/libretro-database)

## Licença

**Freeware — uso gratuito. © 2026 Maniaco Game Room. Todos os direitos reservados** (exceto o arquivo de atualização do menu, que é GPL). Veja a [licença](LICENCA.md) e os [componentes de terceiros](TERCEIROS.md).

Encontrou um problema? Abra uma [Issue](../../issues).
