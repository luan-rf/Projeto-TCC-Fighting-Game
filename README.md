# Projeto de TCC (2019) - Fighting Game 2D

Jogo desenvolvido durante o trabalho de conclusão de curso de Informática, na plataforma de desenvolvimento Unity utilizando a linguagem de programação C#. O projeto contém menu, seleção de personagem e outros elementos caracteristicos de um fighting game clássico. O projeto continha outros jogos de plataforma e documentação acerca da lógica de programação e de linguagens de programação no desenvolvimento de jogos da época. 

# 🎮 Jogo de Luta 2D - Unity (Local Multiplayer)

Este é um projeto de um jogo de luta 2D multiplayer local desenvolvido na Unity utilizando C#. O sistema conta com mecânicas completas de seleção de personagens e cenários, movimentação física baseada em colisores, suporte a controles (Xbox/Joystick) e teclado, gerenciamento de ciclo de vida de combate (barras de vida) e transição dinâmica entre cenas.

---

## 🚀 Funcionalidades Principais

* **Multiplayer Local:** Suporte nativo para dois jogadores simultâneos no mesmo dispositivo.
* **Seleção Expandida:** Menus dedicados para a escolha de até 3 personagens diferentes por jogador e 3 arenas distintas.
* **Input Híbrido:** Configurado para aceitar comandos tanto pelo teclado quanto por controles analógicos (Xbox).
* **Mecânica de Combate Inteligente:** Detecção de acerto (*hitboxes*) baseada em triggers 2D, aplicação de dano em tempo real e atualização dinâmica da interface de UI.
* **Espelhamento Automático (*Flip*):** Os personagens rotacionam dinamicamente nos eixos para sempre se manterem de frente um para o outro durante a luta.

---

## 📂 Estrutura dos Scripts (Arquitetura do Projeto)

O projeto está dividido em scripts modulares para facilitar a manutenção e escalabilidade:

### 🖥️ Menus e Fluxo de Jogo
* **`menu.cs`**: Gerencia a tela inicial principal, lidando com a inicialização do jogo através do `SceneManager` e o fechamento do aplicativo.
* **`Menu_selecao.cs`**: Controla o cursor da tela de seleção de personagens para ambos os jogadores. Bloqueia os inputs após a confirmação e avança de cena assim que ambos estiverem prontos.
* **`selecao_cenario.cs`**: Responsável pela navegação e escolha da arena de combate.

### ⚔️ Combate e Sistemas de Jogo
* **`controle.cs`**: Atua como o *GameManager* da arena. Utiliza variáveis estáticas dos menus para instanciar (*Spawn*) os personagens escolhidos em suas respectivas posições e ativar as animações de fundo do cenário correto.
* **`barraVida.cs` & `barraVida2.cs`**: Controlam de forma independente a escala visual da UI de vida de cada jogador baseado na proporção matemática entre a vida atual e a vida máxima.

### 🏃 Controladores de Personagem
* **`Mov_1.cs` & `Mov_2.cs`**: Gerenciam a física (`Rigidbody2D`) e a movimentação dos Players 1 e 2. Controlam os estados do `Animator` (correndo, pulando, agachado, parado) e a lógica de inversão do `localScale` baseada na posição do oponente.
* **`Botoes1.cs`** (e complementares): Mapeia o conjunto de 6 botões de ataque para cada jogador, aciona as animações de ataque e calcula a perda de pontos de vida ao colidir com o *trigger* do adversário.

---

## 🕹️ Controles Padrão (Mapeamento de Input)

O projeto utiliza o sistema de Input clássico da Unity, mapeado da seguinte forma:

| Ação | Player 1 (Teclado/Controle) | Player 2 (Teclado/Controle) |
| :--- | :--- | :--- |
| **Movimento Horizontal** | `Horizontal` / Análogo `XboxH1` | `Horizontal2` / Análogo `XboxH2` |
| **Pular / Agachar** | `Vertical` / Análogo `XboxV1` | `Vertical2` / Análogo `XboxV2` |
| **Botões de Ataque** | Strings configuráveis (`b1` a `b6`) / `Cb1` a `Cb6` | Strings configuráveis (`b3` a `b4`) para UI |
| **Reset de Vida (Dev)** | `Space` (Restaura ambas as barras para 100) | `Space` |

---

## 🛠️ Como Configurar no Editor da Unity

Para que o projeto funcione perfeitamente, certifique-se de seguir os passos abaixo no Unity Editor:

1. **Input Manager:** Adicione e configure os eixos correspondentes (`XboxH1`, `XboxV1`, `XboxH2`, `XboxV2`, `Horizontal2`, `Vertical2`) nas configurações de Input do seu projeto (`Edit > Project Settings > Input Manager`).
2. **Tags:** Crie e atribua as seguintes Tags aos respectivos objetos:
    * `chao` -> Nos colisores das plataformas/chão.
    * `Player1` e `Player2` -> Nos respectivos prefabs dos personagens.
    * `trigger` -> Nos colisores responsáveis pela área de ataque.
3. **Build Settings:** Certifique-se de adicionar as cenas na ordem correta:
    * `Cena 0`: Menu Principal (`menu.cs`)
    * `Cena 1`: Seleção de Personagem (`Menu_selecao.cs`)
    * `Cena 2`: Seleção de Cenário (`selecao_cenario.cs`)
    * `Cena 3`: Arena de Combate (`controle.cs`)
4. **Variáveis Públicas:** No Inspector do script `controle`, associe os Prefabs dos seus personagens nos campos `F1, F2, S1, S2, T1, T2` e defina os locais de spawn em `pos1` e `pos2`.

---

## 📝 Licença

Este projeto é de código aberto e está disponível para fins de aprendizado e modificação sob a licença MIT.
