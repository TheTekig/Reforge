Game Design Document (GDD) - Reforge: O Começo do Fim 
1. Visão Geral do Jogo (Game Overview)
    Título do Jogo: Reforge: O Começo do Fim
   
    Conceito Principal: Um RPG de ação isométrico onde um protagonista "comum" liberta acidentalmente uma arma sarcástica e milenar que selou os horrores de outro reino.        Juntos, eles devem conter o colapso do mundo, com a progressão do jogador baseada na absorção de itens pela arma para desbloquear e evoluir habilidades.
    Gênero: RPG de Ação, Isométrico, Comédia Sarcástica, Exploração, Dungeon Crawler.
   
    Plataformas Alvo: Inicialmente Windows Desktop (Windows 10+), com potencial para macOS, Linux, consoles e mobile no futuro.
    Público-Alvo: Jogadores que apreciam RPGs de ação com foco em progressão não-linear, exploração, humor negro e narrativa interativa.
   
    Proposta de Venda Única (USP):
    Uma arma protagonista com personalidade sarcástica e interativa, que comenta constantemente as ações do jogador.
    Sistema de progressão inovador baseado na "absorção" de qualquer item para desbloquear e evoluir habilidades, permitindo builds orgânicas e experimentais.
    Múltiplos finais moldados pelas escolhas do jogador, sua relação com a arma e as facções.
    Mundo reagente que muda com as ações do jogador e um sistema de comércio regional dinâmico.

2. História e Mundo (Story and World)
   
    2.1. Introdução: O Começo do Fim
    O jogador é um cidadão comum de uma vila entediante que, durante uma caminhada sem rumo, cai em um buraco e encontra um baú misterioso. Ao abri-lo, libera uma rajada de 
    energia, almas corrompidas e monstros, e uma arma brilhante surge no centro do baú. A arma, que se revela uma entidade viva, imediatamente culpa o jogador por ser "o 
    fim do mundo".
   
    2.2. A Arma Sarcástica: Guardiã Esquecida
    Essa arma não é qualquer relíquia. Ela é uma entidade viva, guardião milenar que selou os horrores do outro reino há séculos, sacrificando-se no processo. Seu poder era 
    tão perigoso e a ameaça tão grande que ela mesma prendeu-se no baú como última camada de segurança. E você... bem, você foi "burro o suficiente pra tirar o cadeado". 
    Agora, a arma está forçada a te acompanhar, pois só pode ser empunhada por quem a libertou — e não está nada feliz com isso.
   
    2.3. Escolha de Arma
    No momento em que empunha a arma, ela assume a forma mais compatível com a "alma" atual do jogador, que pode ser:
    🛡️ Escudo: Defensivo e provocador.
    🗡️ Espada: Equilibrada e ácida.
    🏹 Arco: Rápido e irônico.
    🪓 Lança: Agressiva e sarcástica. 
    Cada forma possui sua própria personalidade e forma de se comunicar, mantendo o deboche. O humor muda, mas o deboche continua.

    2.4. Desequilíbrio dos Reinos
    Com o selo rompido:
     - As almas corrompidas escapam.
     - Um reino sombrio começa a sobrepor o seu.
     - Criaturas distorcidas invadem o mundo.
     - NPCs começam a perder a sanidade, e alguns são possuídos. O mundo entra em colapso progressivo, e a única coisa que impede a destruição imediata é o vínculo tênue 
      entre 
     - o protagonista e a arma.
   
    2.5. Relação Jogador–Arma (Central)
   
    A arma:
     - Te insulta, avisa, aconselha (contra vontade).
     - Comenta suas decisões, estilo de jogo, erros e até diálogos com NPCs.
     - Às vezes age sozinha se você hesita demais. O jogador e a arma formam uma dupla forçada, onde a evolução da relação define partes da história, das skills e do final 
       obtido.

3. Gameplay
    3.1. Mecânicas Centrais de Jogo
   
        3.1.1. Movimentação e Colisão
        Sistema de movimentação baseado em movimentação pixel a pixel com verificação de colisão via place_meeting e refinamento com sign() para suavidade.
        Máscaras de colisão invisíveis serão usadas para objetos do cenário (árvores, pedras, geladeiras) para impedir passagem sem bloquear a visibilidade.
        Elementos como moitas terão controle de profundidade com depth = -y para criar o efeito de sobreposição vertical.
   
        3.1.2. Combate e Golpes
        O jogador inicia com uma arma básica (dependente da classe), que pode atacar em diferentes direções.
        Ataques possuem cooldown controlado por alarm e detecção de acerto via place_meeting entre hitbox do golpe e objeto do inimigo.
        Golpes não são apenas visuais: eles se comportam como instâncias (ex: obj_slash) com própria colisão, tempo de vida e animação.
        Sistema de Stamina para controlar uso exagerado de dash, bloqueio ou combos.
        Cooldown com Alarms: cada skill possui tempo de recarga próprio.
        Sistema de Combo: bônus ao realizar ataques sem tomar dano por um tempo.
   
        3.1.3. Absorção de Itens (Core Mechanic)
        A arma que o jogador encontra não apenas fala — ela consome. Sua verdadeira habilidade é a absorção de qualquer item com energia latente: desde uma folha boba até o     
        coração de um arqui-demônio.
        "Você me deu... uma folha seca. Que incrível. Vou usá-la para espantar mosquitos. Espera — isso virou uma skill?" Essa é a base do sistema de progressão.
        A absorção ocorre quando o jogador se aproxima do item e interage ou passa por cima (via instance_place() + verificação de tipo).
   
    3.2. Sistema de Classes e Armas
   
        3.2.1. Escolha de Classe
        No início do jogo, ao abrir o baú selado, o jogador é envolvido por almas que representam classes:
        Espada: Balanceada, foco em combos e dano médio.
        Escudo: Defesa superior, habilidade de empurrar ou refletir ataques.
        Arco: Ataques à distância com mira precisa.
        Lança: Alcance longo e ataque giratório. A escolha define o tipo base da arma, mas todas as armas compartilham o mesmo sistema de absorção e evolução.
        3.2.2. Arma com Vontade Própria
        A arma possui uma personalidade sarcástica e debochada. Dialoga com o jogador nos momentos-chave, fazendo piadas ou críticas durante o combate e decisões. Revela-se 
        como o verdadeiro guardião selador dos arquidemônios, que selou a si mesmo para conter o poder.

4. Sistema de Skills e Progressão
    4.1. A Arma que Absorve Tudo (e Reclama de Tudo):
    Ao derrotar inimigos, explorar o mundo ou quebrar objetos, o jogador pode encontrar itens que alimentam o sistema da arma:
    🌿 Itens Naturais: Folhas, pedras, sementes -> Skills básicas ou utilitárias.
    🧠 Espólios Comuns: Inimigos normais (ondas) -> Skills ofensivas ou defensivas.
    💀 Espólios Corrompidos: Inimigos corrompidos ou elites -> Skills complexas e sinistras.
    🔥 Núcleos Arqui-Demônios: Bosses de dungeon / chefes de wave -> Skills únicas, com mecânicas próprias.
   
    4.2. Progressão das Skills:
    Cada skill possui 3 níveis de poder. Ela evolui por:
    Uso contínuo (ganham XP).
    Ou alimentação com mais itens do mesmo tipo (absorção extra, ex: consumir mais venenos melhora skill "Dardo Tóxico").
    Nível 1: Skill básica desbloqueada.
    Nível 2: Skill é fortalecida após uso contínuo ou fusão com mais itens similares.
    Nível 3: Forma final da skill, com efeitos adicionais, redução de cooldown ou novo comportamento. "Você está tentando me fazer cuspir fogo com cinco tomates podres? … 
    Tá. Funcionou."
   
    4.3. Propriedades dos Itens
    Cada item absorvível carrega propriedades como (no formato tipo JSON):
    JSON
    {
      "nome": "Espinho de Trepadeira",
      "sprite": "spr_espinho",
      "poder": 5,
      "valor": 10,
      "consumivel": true,
      "absorcao": true,
      "skill_tipo": "veneno",
      "raridade": "comum"
   }
   
    Essas informações alimentam o sistema da arma e o inventário, e cada tipo pode ser usado para desbloquear novos estilos de build, como:
    Build de veneno
    Build de gelo (com névoas de espíritos)
    Build de teleporte (com cristais de sombra)
    Build tanque (com escamas de arqui-demônios)
   
    4.4. Aplicações Práticas:
    O jogador explora e coleta tudo que vê.
    Testa combinações — o sistema não revela tudo de cara.
    Skills desbloqueadas alteram drasticamente o gameplay.
    O Sistema lembra um pouco Megaman, Kirby ou Risk of Rain — mas com identidade própria e sarcasmo constante. "Absorveu um graveto e aprendeu a cutucar. Magnífico.            Realmente somos a última esperança da humanidade."
   
    4.5. Categorias de Itens e Rota de Builds:
    Itens dropados em combate possuem tags e elementos latentes, que determinam o tipo de skill ao serem absorvidos. Assim surgem rotas de build:
    Caminho de Build / Tipo de Itens Absorvidos / Exemplos de Skills
   
    🥾 Ágil
    Penas, folhas, cascos leves
    Dash Triplo, Corte Relâmpago
    🛡️ Tank
    Carapaças, escamas, metais
    Escudo Espinhoso, Absorver Golpe
    🔥 Ofensiva
    Brasas, garras, espólios demoníacos
    Explosão Demoníaca, Corte Flamejante
    🌿 Controle
    Raízes, cogumelos, gelo, sombra
    Prisão de Espinhos, Gelo Estagnante
    🧬 Mística
    Fragmentos mágicos, almas, runas
    Teleporte, Skill Aleatória
    ⚡ Caótica
    Mistura instável de tudo
    Efeitos imprevisíveis e combos sinérgicos


     O jogador descobre essas builds organicamente, não por um menu, mas por feedbacks visuais, efeitos e falas da arma.
 
    4.6. Interações e Sinergias (comentários da arma):
    Combinação de Skills cria efeitos sinérgicos. Ex:
    Usar "Rajada de Fogo" + "Campo de Óleo" = Incêndio em área.
    Usar "Prisão de Espinhos" + "Explosão Demoníaca" = Dano massivo a inimigos presos. A arma comenta sarcasticamente sobre suas escolhas: “Ah sim, claro, mais veneno.     
    Porque nada diz ‘herói’ como envenenar tudo que respira.”
    
    4.7. Reconfiguração (Respec):
    A arma pode “digerir” skills antigas para abrir espaço para novas. O jogador pode oferecer fragmentos especiais (drop de bosses ou dungeons) para:
    Esquecer uma skill.
    Reduzir seu nível.
    Substituir uma skill com algo aleatório (com risco). A arma odeia isso e comenta sarcasticamente, mas permite: “Estamos jogando fora a Explosão Etérea por uma Folhinha 
    Saltitante... ótimo plano, chefe.”

5. Exploração e Estrutura do Mundo
   
    5.1. Mapa Interligado e Aberto
    O mundo de Reforge é um mapa interligado com áreas bloqueadas por skills. Algumas regiões só são acessíveis com determinadas habilidades (ex: dash para atravessar 
    buracos, skill de fogo para queimar raízes). O mapa terá atalhos, segredos e zonas ocultas reveladas ao evoluir a arma.
   
    5.2. Regiões e Cidades
    O mundo é dividido em regiões distintas, cada uma com clima, fauna, inimigos e drops próprios. As cidades são pontos de apoio com comércio e histórias locais.

        5.2.1. Estrutura Global
            Região             / Clima                     /  Inimigo                                   /  Drops Característicos
            Floresta de Miril  - Densa, viva, vibrante     - Plantas carnívoras, feras místicas         - Folhas mágicas, seiva, raízes vivas
            Planícies do Fim   - Vento constante, vastidão - Bestas blindadas, arqueiros fantasmas      - Ossos, couro, penas cinzas
            Caverna de Tharn   - Escura, sufocante         - Demônios, morcegos, monstros de sombra     - Garras, pedras arcanas, ectoplasma
            Montanhas do Norte - Neve, gelo, altitude      - Golens, espectros                          - Cristais, gelo eterno, escamas
            Terras Arruinadas  - Pós-batalha, corrompida   - Fantasmas, restos de cavaleiros, parasitas - Armaduras quebradas, armas malditas
            Cidade Central (hub) - Centro de tudo          -                                            - Acesso a tudo, NPCs principais, upgrade da arma

    5.3. Sistema de Dungeons:
     - As dungeons são portais abertos após absorção do poder da caixa de Pandora.
     - Geradas dinamicamente (semi-procedural), baseadas em: sua build (afinidade influencia inimigos), progresso (quanto mais avançado, mais complexas), eventos globais.
     - Contêm: waves de inimigos, mini puzzles, chefes intermediários, loots com drops raros.
     - Ao completar: Drop especial para arma, fragmento de narrativa desbloqueado, skill rara garantida.

            5.3.1. Tipos de Eventos nas Dungeons
            Eventos de escolha: Salvar ou sacrificar um NPC → consequência futura.
            Eventos de memória: Arma revela memórias do passado (vídeos, imagens ou frases-chave).
            Eventos randômicos: Sala de troca, sala de maldição, sala de desafio.
       
    5.4. Eventos Aleatórios e Exploração Dinâmica
    Ao explorar, o jogador pode encontrar:
    Mercadores viajantes raros.
    NPCs em perigo que podem virar aliados.
    Rituais de absorção corrompida (buffs poderosos com riscos).
    Portais instáveis para micro-dungeons. A chance desses eventos ocorre com base no nível do jogador, região e reputação com facções. "Genial. Entramos voluntariamente        numa caverna fedendo a enxofre. Que tal pular num poço agora?”
   
    5.5. Interação com a Arma durante a Exploração
    A arma interage constantemente com o ambiente:
    Alerta perigos (ou te incentiva a entrar mesmo assim).
    Faz piadas com NPCs.
    Revela segredos se for levada para locais específicos (ex: mural antigo, templo, ruína).
    “Essa estátua aí... fui eu quem quebrei séculos atrás. Ops.”

6. Sistema de Economia e Cidades
    6.1. NPCs com Comportamento Variável
    Os NPCs não são genéricos. Suas falas, opções de interação e até presença no mapa variam conforme:
    A reputação do jogador.
    A build atual (afinidade com luz, trevas, natureza, etc.).
    A região onde estão.
    Progresso na história.
    Exemplos: Um clérigo pode recusar falar com jogadores de build sombria. Um mercador pode dar desconto para builds do tipo gelo por ser de uma cidade montanhosa.


    6.2. Economia Regional e Flutuação de Preços
    Cada cidade tem uma economia própria, ligada ao tipo de drop da região. Isso afeta:
    Preços de itens.
    Itens disponíveis para troca.
    Aceitação de itens absorvíveis.
    Demanda mercantil (miniquests).

Cidade
Itens Valorizados
Itens Baratos
Especialidade
Vila Miril
Folhas Vivas, Raízes
Metal, Chamas
Poções naturais, buffs temp
Tothran
Garras, Pedras
Cristais, Penas
Forja de arma, Melhorias skill
Gelstheim
Gelo eterno, Escamas
Itens orgânicos
Armaduras,Resistência elemental


    Impactos da Economia Regional: Os preços dos itens mudam com o tempo ou com a interferência do jogador (pode criar escassez de itens). Ajudar cidades aumenta seus           estoques e reduz preços.

    6.3. Sistema de Comércio entre Regiões
    O jogador pode atuar como comerciante: transportar itens valiosos de uma cidade para outra e vendê-los com lucro. Algumas cidades possuem mercado negro, aceitando itens 
    “proibidos” para criar skills instáveis. Existe chance de assalto por inimigos, quebra de carroça ou traição de NPCs em transportes.
    
    6.4. NPCs Comerciais e Reforjadores
    Ferreiro especializado: Permite reforjar a arma, mudando suas afinidades.
    Vendedor de escombros: Troca partes quebradas de inimigos por buffs passivos.
    Mercador de almas: Troca almas por skills “corrompidas” (fortes, mas imprevisíveis).
    Mago das runas: Vende runas únicas que podem ser absorvidas para mudar o efeito de uma skill já existente.





    6.5. Facções com Causas e Missões Próprias
    O jogador pode interagir com facções que possuem suas próprias agendas, inimigos e recompensas.
🔰 Exemplos de Facções:
Guardião da Forja: Domínio das armas e da honra -> Skills exclusivas de arma.
Sombras do Véu: Culto secreto ao equilíbrio -> Itens únicos e finais alternativos.
Círculo Verdejante: Defensores da vida e natureza -> Buffs de cura e defesa.
Lâmina do Abismo: Destruidores e caçadores de chefes -> Acesso a dungeons ocultas e equipamentos sinistros.
Reputação: Cada ação aumenta ou reduz sua reputação com uma ou mais facções. Matar certos inimigos ou absorver determinados tipos de skill pode ofender ou agradar facções.

7. Sistema de Combate e Inimigos
   
    7.1. Tipos de Ataques
    Melee (Corpo a Corpo): Usa a arma principal (espada, escudo, lança, arco) para ataques próximos.
    Ranged (À Distância): Para armas que permitem ataques à distância (arco e habilidades especiais da arma).
    Skills Ativas e Passivas: Ativas desencadeadas manualmente (ex: ataque especial que consome itens absorvidos). Passivas melhoram atributos do personagem e da arma (ex: 
    aumento da velocidade, chance de crítico).
   
    7.2. IA dos Inimigos (Inimigos Comuns)
    IA Baseada em Estados: Patrulha, Alerta, Agressivo, Fuga (alguns inimigos).
    Comportamento Específico por Tipo: Inimigos voadores ignoram colisões de solo. Inimigos blindados requerem ataques laterais ou habilidades específicas. Inimigos 
    ilusórios desaparecem se atacados sem skill mágica ativa.
    Grupos Inteligentes: Em áreas mais avançadas, inimigos atacam em sincronia (um puxa agro, outro embosca).

    7.3. Chefes e Arquidemônios (Bosses das Waves)
    Os bosses representam picos de desafio e cada um é guardião de um Espólio Singular necessário para liberar skills especiais na arma.
    🧠 Estrutura dos Bosses: Fases (mudam padrão de comportamento com base na vida), frases únicas (conexão narrativa), comportamentos únicos (teletransporte, manipulação 
    de cenário, invocação de mobs), e diálogos com a arma do jogador (cutscenes rápidas antes ou depois).
    🧬 Drop Especial: Cada boss solta um item de absorção única para liberar: uma skill rara, uma transformação visual na arma, um fragmento da memória selada da arma.
   
    7.4. IA Adaptativa (em Dungeons)
    A cada dungeon superada, o sistema ajusta o comportamento dos inimigos: mais velocidade de reação, grupos com sinergia (healer + melee), inimigos começam a evitar 
    skills usadas com frequência. Bosses podem reaparecer com novos padrões, se invocados novamente.

8. Inventário, Interface de Habilidades e Sistema de Upgrades
   
    8.1. Sistema de Inventário
    O inventário é o coração da progressão do jogador. Ele armazena todos os itens absorvíveis, consumíveis, materiais especiais e drops raros usados para:
    Liberar novas skills.
    Melhorar skills existentes.
    Evoluir a arma.
    Trocar por favores em cidades (eventos, reputação, upgrades estéticos).
    Estrutura de um Item: {"nome": "Essência Ardente", "sprite": spr_essencia_fogo, "tipo": "material", "consumível": false, "absorvível": true, "elemento": "fogo", 
    "poder": 12, "skill_associada": "Explosão Flamejante"}
    Sistema de filtros e busca será adicionado futuramente.


    8.2. Interface de Habilidades (Skill Tree Adaptativa)
    A Skill Tree não é fixa. Ela cresce organicamente de acordo com os tipos de itens absorvidos. Cada skill aprendida abre ramificações de evolução e combinações.
    🧭 Exibição: Interface circular ou radial, skills conectadas por afinidade (cores e elementos), exibição por uso frequente e nível atual.
   
    8.3. Sistema de Evolução da Arma (Build)
    A arma evolui em conjunto com o jogador e assume formas e efeitos visuais conforme as skills absorvidas.
    🎭 Aparência: Visual da arma muda com a afinidade dominante. Quanto mais skills absorvidas de um mesmo tipo, mais a arma "corrompe" seu estilo visual (ex: flamejante, 
    sombria, angelical...).
    💡 Vontade da Arma: A arma interage com as escolhas do jogador. Critica ou elogia o tipo de skill absorvido. Pode se recusar a usar uma skill por tempo limitado se o 
    jogador "trair" uma afinidade.
   
    8.4. Sistema de Nível por Skill (Sem XP Tradicional)
    O jogador não sobe de nível por XP, mas sim por:
    Quantidade de skills absorvidas.
    Nível individual de cada skill.
    Diversidade de builds experimentadas.
    Nível = Soma dos níveis de todas as skills absorvidas.
    🛠 Efeitos do Nível: Aumenta HP, estamina e velocidade de movimento. Desbloqueia diálogos com NPCs e interações secretas. Permite acessar dungeons e regiões mais 
    complexas.
   
    8.5. Resumo da Progressão
    Sistema
    Como Evolui
    Impacto
    Skills
    Uso e absorção de itens
    Melhora combate e desbloqueia novas áreas
    Arma
    Afinidade e tipo de skills absorvidas
    Visual, diálogos e poder
    Nível
    Soma dos níveis de skills
    Novas áreas, eventos e buffs
    Build
    Escolhas estratégicas de skillset
    Estilo de jogo e finais possíveis
    
    Exportar para as Planilhas

9. Arte e Áudio
    9.1. Arte e Design Visual
    Estilo Visual: Pixel art detalhada, com estética isométrica para dar sensação de profundidade e perspectiva.
    Personagens, Inimigos e Itens: Animações frame a frame.
    Tilesets: Para construção das dungeons e mapas, com variações para diferentes biomas e cidades.
    Animações: Movimentação fluida com 8 direções. Animações específicas para ataques, bloqueios, uso de skills e interações.
   
    9.2. Interface de Usuário (UI) e Experiência do Usuário (UX)
    UI/UX: Interface limpa e intuitiva, com HUD para vida, mana, stamina, inventário e skills.
    Menus: Seleção de classe, upgrades de skill, e inventário.
   
    9.3. Áudio
    Música: Trilhas sonoras ambientais para cidades, dungeons e batalhas. Música adaptativa que muda conforme a situação do jogo.
    Efeitos Sonoros: Sons para ataques, absorção de itens, uso de skills, passos, interações e notificações. Feedback sonoro para cooldowns, danos e pickups.

10. Aspectos Técnicos
    10.1. Motor Gráfico e Plataforma
    Motor: GameMaker Studio 2/3 (GameMaker Language - GML).
    Foco: Engine 2D, facilita o desenvolvimento do RPG isométrico com visão isométrica.
    Suporte Multiplataforma: Windows, macOS, Linux, e exportação para consoles e mobile no futuro.
    Renders: Gráficos 2D com sprites em pixel art estilizados. Suporte para camadas para simular profundidade. Uso de máscaras de colisão pixel-perfect para interações 
    precisas.
    
    10.2. Linguagem de Programação
    GameMaker Language (GML): Linguagem de script proprietária do GameMaker, baseada em sintaxe similar ao C e JavaScript.
    Funcionalidades: Permite manipulação de objetos, eventos, colisões, animações, sons e lógica do jogo.
    Modularidade: Suporte para criação de scripts modulares e reutilizáveis (funções e scripts customizados).
    
    10.3. Estrutura de Dados
    Inventário e Itens: Estruturados em dicionários e arrays (GML) para armazenar atributos (nome, sprite, poder, consumível, etc).
    Persistência: Possibilidade de salvar e carregar dados em JSON para persistência entre sessões.
    Skills e Builds: Tabelas para armazenar níveis de skills, efeitos e cooldowns. Sistema modular para adicionar novos skills via dados configuráveis.
    
    10.4. Colisão e Física
    Detecção de Colisão: Uso intensivo de place_meeting e instance_place para colisões pixel-perfect.
    Máscaras de Colisão: Customizadas para cada sprite, inclusive para ataques e habilidades.
    Movimentação: Sistema baseado em velocidade horizontal (hsp) e vertical (vsp), com resolução detalhada para impedir atravessar objetos. Script reutilizável para 
    movimentação de jogadores e inimigos.
    
    10.5. Requisitos Mínimos e Plataformas Alvo
    Plataforma Inicial: Windows Desktop (Windows 10+).
    Requisitos Mínimos: Processador Dual-Core 2.0 GHz ou superior, 4 GB RAM, Placa gráfica compatível com DirectX 9 (integrada serve), Espaço em disco ~500 MB.
    Futuro: Possibilidade de exportação para macOS, Linux, e plataformas móveis com ajustes.
    
    10.6. Ferramentas Auxiliares
    Editor de Pixel Art: Aseprite, Piskel ou similar para criação de sprites.
    Editor de Áudio: Audacity, FL Studio para edição e criação de sons.
    Versionamento: GitHub para controle de versões e backup do código.

11. Vida, Morte e Ressurgimento
    11.1. Sistema de Vida
    Barra de vida do jogador visível na UI.
    Ao perder toda a vida, o jogador "morre" e ressuscita em checkpoints ou cidades específicas.
    
    11.2. Penalidades de Morte
    Perda de parte dos itens consumíveis (ex: folhas, espólios) que estavam sendo absorvidos.
    Diminuição temporária de algumas skills passivas (ex: redução de dano por 5 minutos).
    Reputação com facções pode ser afetada dependendo da causa da morte.
    
    11.3. Checkpoints e Save Points
    Localizados em cidades e dentro de dungeons (como altares ou fogueiras).
    Restauram vida, mana e stamina, além de permitir salvar o progresso.

12. Finais Múltiplos e Narrativa Dinâmica
    12.1. Decisões do Jogador Moldam o Final
    Escolha da classe inicial (arma) impacta possíveis finais.
    Relações com facções influenciam desfechos e até missões finais.
    
    12.2. Evolução da Arma e Finais
    A arma sarcástica reage conforme o uso de habilidades, absorção e escolhas do jogador:
    Final “Voltar ao Normal”: Você ajuda a arma a refazer o selo, sacrificando tudo. A arma volta ao baú. Você esquece de tudo — e o ciclo pode recomeçar.
    Final “Fuga Covarde”: Você abandona a missão, foge para longe. O mundo é consumido lentamente. A arma zomba de você até os créditos.
    Final “Domínio”: Você força a arma a absorver poder demais, desequilibra a balança. Ela perde o controle… e você se torna o novo selo.
    Final Secreto “Guardião Substituto”: Ao entender o peso do sacrifício, você voluntariamente se funde com a arma para contê-la. Um novo ciclo começa — mas agora você é o 
    guardião.
    Finais Implícitos pela Afinidade da Arma:
    Se usada para absorver apenas itens puros → final "Herói Libertador".
    Se usada para absorver itens sombrios/monstros → final "Guardião Sombrio".
    Uso equilibrado → final "Equilibrador do Reino".
    
    12.3. Narrativa Interativa
    A arma sarcástica tem falas dinâmicas, comentando as ações do jogador, e pode influenciar decisões.
    Interações com NPCs e facções variam conforme o progresso e build.


