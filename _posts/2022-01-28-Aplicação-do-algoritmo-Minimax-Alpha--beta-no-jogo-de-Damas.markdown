---
layout: post
title:  "Aplicação do algoritmo Minimax Alpa-beta no jogo de Damas"
date:   2022-01-28 11:33:40 -0300
categories: IA
---
Diversos problemas podem ser tratados e resolvidos por algoritmos de busca - partimos de um estado inicial e tentamos encontrar uma solução que satisfaça nosso parâmetro percorrendo vários estados intermediários. Em jogos como o jogo dos 15 podemos aplicar uma busca simples para encontrar uma solução, como a busca em profundidade; isso é possível pois o agente tem total controle sobre suas ações e consequências, portanto é capaz de percorrer todos os estados possíveis do jogo. 

Existem, no entanto, jogos os quais esses conceitos não funcionam: jogos adversariais, onde temos dois agentes jogando, não necessariamente competindo entre si. O oponente é “imprevisível”, portanto temos que considerar todos os casos possíveis de jogada do adversário para encontrar soluções ideais já que não temos mais controle sobre as ações e consequências do jogo.

Jogos adversariais podem ser determinísticos ou de azar, com informação perfeita ou imperfeita. Analisaremos um jogo determinístico com informação perfeita, pois se trata de um caso mais básico. Um exemplo são os jogos de “soma zero", que são jogos que um agente só pode ganhar se o outro perder. Um dos jogadores tenta maximizar seus pontos enquanto o outro tenta minimizar.


Para exemplificar, examinaremos o jogo de damas:
Nesse jogo apenas um dos jogadores pode ganhar, então temos um jogo de soma zero. Temos os possíveis resultados finais, os quais 1 significa vitória, -1 derrota e 0 empate:

    jogador 1  |  jogador 2
        1      |     -1
        0      |      0
       -1      |      1


O algoritmo Minimax é baseado na forma que os humanos jogam esses jogos: consideram as suas possíveis jogadas e as respostas do oponente, analisando qual caminho é o mais benéfico. A estrutura de dados normalmente usada em sua implementação é uma árvore binária, onde a raiz dela é a posição atual, cada nó é uma posição legal e os ramos são os caminhos possíveis. Nós folhas são estados terminais, ou seja, onde o jogo acaba. 
 
Dentro da árvore de nós intercalamos um ramo MAX com um ramo MIN. O ramo MAX tenta maximizar sua utilidade e representa o jogador 1, enquanto o ramo MIN minimiza a utilidade de MAX e representa o jogador 2 (dentro de jogos de soma zero minimizar os pontos do adversário significa maximizar os seus ganhos).

O valor Minimax para um estado terminal é sua utilidade. Em um estado não terminal, o valor é a utilidade (para MAX) do menor estado terminal seguindo essa subárvore. Para entender melhor, imagine a seguinte situação:
Cada linha é uma rodada, e os nós são as possíveis jogadas. MAX e MIN alternam as jogadas (o quadrado significa que a jogada é do MAX, e o triângulo do MIN).
Para obtermos o valor Minimax das 3 possíveis jogadas de MIN, iremos até o fim de cada subárvore e retornaremos os valores de cada nó terminal. O valor mínimo é o valor Minimax, e a utilidade de seus pais passa a ser esse valor mínimo. Dessa forma, MAX é capaz de escolher o nó onde, supondo que o MIN jogue idealmente, tenha a menor perda. No caso da imagem a seguir, o melhor caminho a se escolher é o B, pois tem o maior valor Minimax. 



[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
