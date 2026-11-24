# CORREDOR — versão Unity

Jogo de terror em primeira pessoa: encontre a chave e fuja do subsolo sem ser pego.
Portado do jogo original em HTML/three.js para o **Unity 6.6 (6000.6.9f1)** com **URP**.

## Como abrir o projeto

1. Instale o **Unity Hub** e, pelo Hub, o editor **6000.6.9f1** (a mesma versão evita problemas).
2. Clone este repositório (o jeito mais fácil é o **GitHub Desktop** → *File → Clone repository*).
3. No Unity Hub: **Projetos → Adicionar → Adicionar projeto do disco** e escolha a pasta clonada.
4. Na primeira vez o Unity demora alguns minutos para montar a pasta `Library`.
5. Abra a cena pelo menu **Corredor → Abrir cena do jogo** e aperte **▶ (Play)**.

## Multijogador e voz (configuração única)

O online usa serviços gratuitos da Unity: **Relay** (sala com código, funciona entre redes diferentes)
e **Vivox** (voz por proximidade). Só precisa fazer isto uma vez, no computador de quem é dono do projeto:

1. No Unity: **Edit → Project Settings → Services** → escolha a organização e clique em
   **Use an existing Unity project ID** (ou *Create project ID*) para ligar o projeto ao Unity Cloud.
2. Em **cloud.unity.com**, abra o projeto e ative **Relay** e **Vivox** (*Products* → *Multiplayer* / *Vivox Voice* → *Get started*).
3. Envie a mudança (o arquivo `ProjectSettings/ProjectSettings.asset` guarda o ID do projeto) para todos receberem.

**Testar sozinho:** *Window → Multiplayer → Multiplayer Play Mode*, ative um *Player 2* e aperte ▶.
Um jogador cria a sala, o outro entra com o código.

## Como o projeto está organizado

Quase tudo é criado por código quando o jogo abre (mapa, texturas, sons, monstro, menus).
A cena tem um único objeto, `Corredor`, com o componente `GameManager`.

| Arquivo | O que faz |
|---|---|
| `Assets/Corredor/Scripts/GameManager.cs` | Loop do jogo, regras (chave, porta, morte, vitória), luzes e efeitos |
| `Assets/Corredor/Scripts/GameManager.UI.cs` | Menus, HUD, configurações e a introdução |
| `Assets/Corredor/Scripts/Content.cs` | Mapas, dificuldades, gerador de labirinto e roteiro da introdução |
| `Assets/Corredor/Scripts/GameManager.Multiplayer.cs` | Sala, mensagens da rede, rodadas, chave, espectador |
| `Assets/Corredor/Scripts/Net.cs` / `Voice.cs` | Conexão (Relay + Netcode) e voz (Vivox) |
| `Assets/Corredor/Scripts/Puppet.cs` | Marionetes dos outros jogadores (rosto pintado, chapéu, lanterna) |
| `Assets/Corredor/Scripts/Monster.cs` | Modelo, animação e IA do monstro |
| `Assets/Corredor/Scripts/Player.cs` | Jogador (andar, correr, agachar, pular, armário, lanterna) |
| `Assets/Corredor/Scripts/World.cs` | Monta o mapa a partir do texto |
| `Assets/Corredor/Scripts/Hands.cs` / `MeshGen.cs` | Mãos de marionete em primeira pessoa |
| `Assets/Corredor/Scripts/Tex.cs` | Texturas desenhadas por código |
| `Assets/Corredor/Scripts/Synth.cs` | Sons sintetizados por código |
| `Assets/Corredor/Resources/*.shader` | Efeito de tela (Cinema/VHS/PS1) e poeira da lanterna |

**Criar um mapa novo:** adicione um item em `Content.Maps` (`#` parede, `.` chão, `P` jogador,
`E` monstro, `K` chave, `X` saída, `L` armário). Todas as linhas precisam ter o mesmo tamanho.

## Trabalhando em grupo

- Antes de começar: **puxe as novidades** (*Fetch/Pull* no GitHub Desktop).
- Faça mudanças pequenas e envie com frequência (*Commit* + *Push*).
- Para algo grande, crie um **branch** e abra um **Pull Request** para os outros revisarem.
- Evitem mexer na **mesma cena** ao mesmo tempo — conflitos em cenas do Unity são chatos de resolver.
- Nunca envie as pastas `Library`, `Temp`, `Logs` e `UserSettings` (o `.gitignore` já cuida disso).
