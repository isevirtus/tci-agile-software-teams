# Team Climate Inventory (TCI) - Português brasileiro

Questionário de 38 itens para avaliar a percepção do clima de equipe, com cinco opções de resposta por item.

## Arquivos

- [Questionário em PDF](tci-pt-br.pdf): pronto para impressão e aplicação.
- [Definições em JSON](tci-pt-br.json): instruções, itens, opções de resposta e regras de pontuação para implementar um formulário eletrônico.
- [Mapa de itens em CSV](tci-item-map.csv): códigos TCI, nomes das variáveis, dimensões e opções de resposta.

## Aplicação

Apresente as instruções e os 38 itens na ordem do questionário. Use as mesmas cinco opções em todos os itens, permita uma resposta por item e solicite o preenchimento de todas as linhas. Para uma aplicação eletrônica, configure as linhas como obrigatórias e mantenha a ordem fixa. Preserve o texto dos itens e das opções.

| Valor | Opção de resposta |
|---|---|
| 1 | Até muito pouco |
| 2 | Até um pouco |
| 3 | Em grau moderado |
| 4 | Em grande medida |
| 5 | Em ótima medida |

## Pontuação

Calcule a média aritmética dos itens de cada dimensão. Valores maiores indicam percepções mais favoráveis. Nenhum item tem pontuação invertida.

| Dimensão | Itens | Variáveis | Cálculo |
|---|---|---|---|
| Vision | TCI1-TCI11 | tv1-tv11 | Média de 11 itens |
| Task Orientation | TCI12-TCI18 | to1-to7 | Média de 7 itens |
| Support for Innovation | TCI19-TCI26 | si1-si8 | Média de 8 itens |
| Participative Safety | TCI27-TCI38 | ps1-ps12 | Média de 12 itens |

A aplicação solicita respostas completas. Se houver omissões, sinalize os escores incompletos e defina o tratamento antes da análise; não trate respostas ausentes como zero. Este guia não estabelece uma regra validada para pontuar dimensões com itens ausentes.

Se for utilizado um resumo geral descritivo, calcule a média das **quatro médias de dimensão**, atribuindo o mesmo peso a cada dimensão. Esse cálculo difere da média simples dos 38 itens e não estabelece que exista um único fator geral de clima.

## Interpretação

Use as distribuições das respostas e os itens específicos para orientar a discussão com a equipe. Os resultados do estudo indicaram alta consistência interna, mas sobreposição entre dimensões, sobretudo Task Orientation, Support for Innovation e Participative Safety. Não interprete esses escores como quatro diagnósticos independentes.

O estudo examinou percepções individuais em equipes ágeis de software. A interpretação de médias como clima compartilhado e as comparações entre equipes exigem evidência que sustente a agregação e a comparabilidade. Não há pontos de corte diagnósticos ou normas para classificar equipes neste material.

## Referências e citação

O TCI foi desenvolvido por Anderson e West (1998), *Measuring climate for work group innovation: Development and validation of the team climate inventory*, Journal of Organizational Behavior, 19(3), 235-258. [DOI](https://doi.org/10.1002/(SICI)1099-1379(199805)19:3%3C235::AID-JOB837%3E3.0.CO;2-C).

Para a avaliação desta versão no contexto de software, cite o manuscrito *Measuring perceived team climate in agile software teams: Internal consistency and dimensional overlap in the Team Climate Inventory* e a versão deste repositório utilizada. A referência do material suplementar está em [CITATION.cff](../CITATION.cff).

As condições de uso do instrumento original continuam aplicáveis. Este repositório não atribui uma nova licença aos itens do TCI.
