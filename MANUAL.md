# Manual do NeoCD SD Manager

**[English version](MANUAL.en.md)**

O NeoCD SD Manager deixa o cartão SD do seu **Neo Geo CD com Neo CD SD Loader (BR Edition)** pronto em poucos cliques: instala o menu, organiza os nomes dos jogos e gera a capa de cada um.

Um projeto do blog **[Maniaco Game Room](https://www.maniacogameroom.com.br/)**.

---

## Sumário

1. [Antes de começar](#1-antes-de-começar)
2. [A janela do aplicativo](#2-a-janela-do-aplicativo)
3. [Preparar cartão](#3-preparar-cartão)
4. [Jogos e capas](#4-jogos-e-capas)
5. [No console](#5-no-console)
6. [O que fica em cada pasta do cartão](#6-o-que-fica-em-cada-pasta-do-cartão)
7. [Problemas e soluções](#7-problemas-e-soluções)
8. [Créditos](#8-créditos)

---

## 1. Antes de começar

**Você precisa de:**

- Um **Neo Geo CD** com o **Neo CD SD Loader** instalado (o kit de Furrtek, versão top-loading ou front-loading).
- Um computador com **Windows 10 ou 11**.
- Um **cartão SD formatado em FAT32**. O loader não lê exFAT nem NTFS; o aplicativo avisa se o cartão estiver em outro formato.
- Os seus jogos no cartão, **cada um em uma pasta na raiz** que contenha o arquivo **`.cue`** (mais os `.bin`/`.iso` e as faixas de áudio que o `.cue` cita). É assim que o menu enxerga os jogos: ele lista as pastas que têm um `.cue`. O menu mostra no máximo **200 jogos**.
- **Internet** na primeira vez: o aplicativo baixa o banco de nomes (Redump) e as capas. Depois ficam guardados no PC, em `%LOCALAPPDATA%\NeoCD-SD-Manager`.

**Instalação:** não há instalação. Baixe o `NeoCD-SD-Manager.exe` na página de [Releases](../../releases) e abra.

> Na primeira vez, o Windows pode mostrar "O Windows protegeu o computador" (SmartScreen), porque o programa é novo e não tem assinatura paga. Clique em **Mais informações → Executar assim mesmo**.

**Seu cartão está seguro:** o aplicativo **não apaga nada**. Ele só (1) copia o arquivo do menu, (2) renomeia pastas de jogos — e guarda o registro para desfazer — e (3) grava o arquivo `bg.bmp` dentro da pasta de cada jogo. Tudo o que for substituído vai para `_neocd-manager/backup`. Mesmo assim, faça uma cópia do cartão antes da primeira vez.

**O que o aplicativo não faz:** não fornece jogos nem BIOS, não converte formatos de disco (ISO solto, CHD, etc.) e não cria `.cue` que não existe.

---

## 2. A janela do aplicativo

![Janela do aplicativo](imagens/app-preparar.png)

- **Cartão SD** (topo): escolha a letra do cartão. Aparecem os discos removíveis; se o seu não aparecer, use **Procurar…** e escolha a raiz do cartão. Ao lado, o aplicativo mostra o sistema de arquivos, o espaço livre e quantos jogos encontrou (em vermelho se não for FAT32).
- **Abas:** *Preparar cartão* e *Jogos e capas*.
- **Rodapé:** etapa atual, andamento, tempo estimado e o botão **Cancelar**. Abaixo fica o **relatório** do que foi feito, com os avisos.
- **Menu Arquivo:** abre o cartão no Explorer.
- **Menu Tema:** cores da janela (Noite, Claro, Neo Geo, Tela CRT). A escolha fica salva.
- **Menu Idioma / Language:** janela em português ou inglês. Na primeira vez, usa o idioma do Windows.
- **Menu Ajuda:** blog Maniaco Game Room, página do projeto e Sobre.

---

## 3. Preparar cartão

É a aba principal: marque o que quer fazer e clique em **Preparar cartão**. Cada passo funciona sozinho.

### Passo 1 — Instalar o menu

Copia o arquivo de atualização **`NSDL0014.WAD`** (menu **V0.14 BR**) para a raiz do cartão e confere a cópia byte a byte (CRC32) antes de concluir.

- O loader usa o **primeiro `.wad`** que achar na raiz. Por isso, se houver outro `.wad` no cartão, o aplicativo o **move para o backup** (não apaga).
- O aplicativo **não grava nada no console**. A atualização acontece no console, quando você o liga com o cartão: se as versões do menu/CPLD instaladas forem diferentes das do arquivo, o loader se atualiza sozinho; se já estiverem iguais, nada acontece.
- Ao lado do passo aparece se o menu já está no cartão.

### Passo 2 — Organizar os nomes dos jogos

Lê as pastas de jogos do cartão e renomeia cada uma com o título certo.

**Como o jogo é identificado:**

1. Pelo **nome da pasta**, comparado com o banco Redump do Neo Geo CD (ignora `[!]`, `_`, maiúsculas, "The", regiões…). O banco traz o nome ocidental e o japonês de cada jogo, e qualquer um deles é aceito. Sequências não são confundidas ("Fatal Fury 3" nunca vira "Fatal Fury 2").
2. Se o nome não bastar — ou se você marcar **Conferir pelo conteúdo do disco (CRC)** —, pelo **CRC da faixa de dados** (Track 01) comparado com o banco. É mais seguro, porém lento: precisa ler o arquivo inteiro de cada jogo (centenas de MB), então o tempo depende da velocidade do cartão. O resultado fica guardado, então uma segunda passada é rápida. A comparação só funciona com dumps no padrão Redump (`.bin` de 2352 bytes por setor).
3. Se nada casar, a pasta **mantém o nome** e aparece no relatório como *não identificado*.

**Estilo do nome:**

- **Título curto (padrão):** o título ocidental, sem etiquetas. Ex.: `Garou Densetsu 2 ~ Fatal Fury 2 (Japan) (En,Ja)` → `Fatal Fury 2`. Se duas pastas dariam o mesmo nome, entra a região: `Fatal Fury 2 (Japan)` e `Fatal Fury 2 (USA)`.
- **Nome oficial completo:** o nome do banco Redump, como está.

Os nomes são gravados em **ASCII simples** (sem acentos e símbolos especiais), porque o loader usa a página de código 850 para nomes de arquivo. Só a **pasta** é renomeada: os arquivos dentro dela (`.cue`, `.bin`, `.wav`) **não são tocados**, então as referências do `.cue` continuam valendo. Uma pasta nunca sobrescreve outra: se o nome já existir, ela é pulada e o relatório avisa.

### Passo 3 — Gerar as capas

Cria um **`bg.bmp`** na pasta de cada jogo — é a capa que o menu mostra ao lado da lista.

- **Fonte da imagem, em ordem:** (1) a sua pasta de imagens (**Minhas imagens**), se você indicar uma; (2) a internet — o aplicativo baixa a capa do jogo do projeto libretro-thumbnails.
- **Minhas imagens:** qualquer pasta com `.png`, `.jpg`, `.webp` ou `.bmp`. O arquivo precisa ter o **mesmo nome do jogo** (o da pasta ou o título oficial), por exemplo `Fatal Fury 2.png`.
- **Ajuste da imagem:** *Esticar* (padrão, mostra a imagem inteira), *Preencher* (corta as bordas), *Inteira com fundo desfocado* ou *Inteira com bordas pretas*.
- **Refazer as que já existem:** por padrão, quem já tem `bg.bmp` é pulado. Marcando, o `bg.bmp` antigo vai para `_neocd-manager/backup/<data>` e é refeito.
- O formato é o do menu: **128 × 128**, 4 bits por pixel, até 8 paletas de 15 cores (a cor 0 é transparente no Neo Geo), cores em 5 bits por canal. As cores são reduzidas — por isso confira a **prévia** na aba *Jogos e capas*.

Ao final aparece o resumo: pastas renomeadas, capas geradas, jogos sem capa, jogos não identificados e avisos (por exemplo, arquivo citado no `.cue` que não existe — o jogo não carregaria).

---

## 4. Jogos e capas

![Jogos e capas](imagens/app-jogos.png)

Para ver e conferir tudo **antes** de mexer:

1. **Analisar cartão:** lista todos os jogos com o nome atual, o **nome novo**, *como foi identificado* (nome, nome aproximado, conteúdo/CRC ou não identificado) e se já têm capa. Laranja = será renomeado; verde = já está certo; vermelho = não identificado ou com arquivo faltando.
2. **Aplicar nomes:** renomeia as pastas (com confirmação). O registro fica em `_neocd-manager/desfazer.json`.
3. **Desfazer último:** volta as pastas do último lote ao nome anterior.
4. **Gerar capas:** cria os `bg.bmp` dos jogos listados, com as opções da aba *Preparar cartão*.
5. **Prévia:** clique num jogo para ver a capa **como o console vai mostrar** (cores e paletas reduzidas), com a origem da imagem.

Um nome marcado como **aproximado** significa que o título da pasta não bateu exatamente com o banco; confira antes de aplicar.

---

## 5. No console

1. Desligue o console, coloque o cartão no SD Loader e ligue.
2. Na primeira vez com o menu novo, o loader se atualiza sozinho durante a inicialização (veja os códigos de LED na [documentação do Furrtek](http://www.furrtek.org/sdloader/): verde-verde-verde indica sucesso). Não desligue durante a atualização.
3. Na lista de jogos, os títulos aparecem com os nomes organizados.
4. Ao parar o cursor sobre um jogo por instantes, a **capa** (`bg.bmp` da pasta do jogo) aparece na caixa ao lado da lista.

---

## 6. O que fica em cada pasta do cartão

```
/                         raiz do cartão (FAT32)
├─ NSDL0014.WAD           menu V0.14 BR (só precisa ficar até o console atualizar)
├─ Fatal Fury 2/          uma pasta por jogo
│   ├─ jogo.cue           o menu lista as pastas que têm um .cue
│   ├─ jogo.bin           (arquivos do disco: não são alterados)
│   └─ bg.bmp             capa gerada pelo aplicativo
└─ _neocd-manager/        criada pelo aplicativo
    ├─ desfazer.json      registro dos renomeados (para "Desfazer último")
    └─ backup/<data>/     .wad e bg.bmp que foram substituídos
```

O aplicativo guarda configurações e o cache de bancos/capas em `%LOCALAPPDATA%\NeoCD-SD-Manager`.

---

## 7. Problemas e soluções

**"O cartão está em NTFS/exFAT — precisa ser FAT32".** O loader só lê FAT32. Copie os arquivos para o PC, formate o cartão em FAT32 (em cartões grandes, use uma ferramenta de formatação FAT32) e copie de volta.

**Um jogo ficou "não identificado".** O nome da pasta não bate com nenhum jogo do banco (pode ser um homebrew, um hack ou um nome muito diferente). Renomeie a pasta com o nome do jogo e analise de novo, ou marque **Conferir pelo conteúdo (CRC)**. Jogos não identificados mantêm o nome e podem ganhar capa se você colocar uma imagem com o mesmo nome na pasta *Minhas imagens*.

**Um jogo ficou "sem capa".** Não há capa desse jogo no libretro-thumbnails. Coloque uma imagem sua na pasta *Minhas imagens* com o nome do jogo.

**A capa ficou feia ou com cores estranhas.** O menu só exibe 15 cores por bloco de 16×16 pixels; capas muito escuras ou com degradês sofrem. Teste outro *Ajuste da imagem*, use uma imagem sua mais simples e marque *Refazer*.

**O jogo não aparece no menu.** Confira se (1) a pasta está na raiz do cartão, (2) tem um `.cue` dentro, (3) o relatório não avisou de arquivo faltando e (4) o cartão não passa de 200 jogos.

**O console não atualizou o menu.** O loader só usa o **primeiro `.wad`** da raiz — deve haver um só. E só atualiza se as versões forem diferentes. Consoles com loader anterior à versão 0.6 precisam usar a opção *Update firmware* do menu (veja a documentação do Furrtek).

**O Windows bloqueou o programa / o antivírus reclamou.** O `.exe` é novo e sem assinatura paga; programas empacotados assim às vezes geram alerta falso. O código-fonte do menu está no GitHub e o `.exe` pode ser conferido pelo hash publicado na página da versão.

**Encontrou outro problema?** Abra uma [Issue](../../issues) informando o texto do relatório.

---

## 8. Créditos

- **Neo CD SD Loader** (hardware, firmware e menu originais): Furrtek — [furrtek.org/sdloader](http://www.furrtek.org/sdloader/)
- **BR Edition** (menu em português, capas, fundo dinâmico): Maniaco Game Room — [código do menu](https://github.com/maniaco007/NeoCDSDLoader-BR-Edition)
- Capas: [libretro-thumbnails](https://github.com/libretro-thumbnails) · Bancos de jogos (Redump): [libretro-database](https://github.com/libretro/libretro-database)
- Componentes do `.exe`: Python, Tcl/Tk, Pillow, NumPy e Nuitka (licenças em [TERCEIROS.md](TERCEIROS.md))
