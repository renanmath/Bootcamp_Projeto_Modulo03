# Apresentação
## Sobre o repositório
Esse repositório contém o Projeto Final do Módulo 03 do Bootcamp Data Science da Alura: Análise de séries temporais.

## Sobre o Módulo 03
O objetivo desse módulo foi conhecer mais sobre séries temporais. Foi apresentado o Prophet, uma ferramenta desenvolvida pelo Facebook para análise de séries temporais. O módulo foi estruturado em 6 aulas:
- Entendendo a série temporal
- Primeiras previsões
- Mudança de tendência
- Feriados e sazonalidade
- Outliers e validação

# O projeto: Covid no Ceará - onde vai? 
## Introdução

O objetivo desse projeto é fazer uma análise de séries temporais relacionadas aos casos de covid no estado do Ceará. As séries analizadas (bem como algumas médias móveis) serão:

-  Casos novos de covid
-  Casos acumulados de covid
-  Óbitos novos por covid
-  Óbitos acumulados por covid


A análise será dividida em dois momentos. Na primeira parte, feita neste notebook, usarem o Prophet, uma biblioteca desenvolvida pelo Facebook, para análise e previsões de séries temporais. Exploraremos alguns de seus recursos, como identificação de sazonalidade, feriadados e pontos de virada. Também usaremos métricas para mensurar a precisão das previsões feitas pelo Prophet.
Na segunda parte faremos uma análise mais minuciosa das tendências em séries temporais, utilizando técnicas para identificar pontos de virada e tendências de crescimento e decrescimento. Para isso exploraremos conceitos como derivadas discretas, indicador supertrend e cruzamento de médias móveis, bem como o uso de aproximações poligonais. Isso será feito em um segundo notebook, confira o [repositório do projeto do Github](https://github.com/renanmath/Bootcamp_Projeto_Modulo03).
Os dados utilizados foram baixados do site [Brasil.io](https://brasil.io/dataset/covid19/caso_full/) e tratados em um notebook separado (veja o [repositório do projeto](https://github.com/renanmath/Bootcamp_Projeto_Modulo03)). Eles foram salvos em formato csv e foi feito o upload para esta [pasta do repositório](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/tree/main/dados). 
Uma observação muito importante: esses dados foram baixados no dia 21/06/2021, e portanto toda a análise aqui feita está atrasada em duas semanas. Preferi manter assim, e posteriormente fazer uma análise com dados atualizados em outro projeto, pois o objetivo principal desse projeto é explorar as ferramentas de análise de séries temporais. Em um projeto futuro, poderemos comparar as previsões e conclusões feitas aqui, e confrontá-las com a realidade. 

## Análise usando Prophet
Como dito, o projeto foi dividido em dois notebooks principais. Nesse primeiro notebook, foi feita uma análise exploratória dos dados de covid no Ceará e logo em seguida, previsões usando o Prophet. Em termos técnicos, os resultados não foram animadores, haja vista que, no geral, os modelos tiveram péssimas métricas de avaliação com respeito aos dados de teste. Já as métricas dos dados de treino foram ótimas, o que aponta para um overfitting do modelo aos dados de treino. Nesse notebook foi feita uma análise dos hiperparâmetros, a fim de se encontrar os valores que retornariam os melhores r2-scores. Para os casos novos, óbitos novos e suas médias móveis, não foram encontrados bons hiperparâmetros que retornassem boas métricas.
No entanto, é necessário entender porque o modelo não estava prevendo bem os dados de teste e a resposta era visualmente clara: os dados iniciaram uma tendência de queda que ia na contra-mão das previsões, que apontavam para uma continuação da tendência de alta. Veja esses gráficos:

![médias móveis casos novos](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/raw/main/imagens/mm_casos_novos_covid.jpg)

![médias móveis óbitos novos](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/raw/main/imagens/mm_casos_novos.jpg)

Então, no sentido social, digamos assim, isso foi um bom resultado. No entanto, os modelos do Prophet de maneira alguma previram essa queda tão acentuada:

![modelo prhophet - média movel casos novos](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/raw/main/imagens/prophet_mm_casos_novos.jpg)

O modelo foi treinado com os dados em preto. Os pontinhos em vermelho são os dados de teste. Note como alguns deles saiem, inclusive, do intervalo de confiança. 

Em resumo, as conclusões desse notebook foram:

**Houve picos de casos novos em Julho de 2020 e Maio de 2020**

No entanto, esses picos tem ordens de grande distinto. Enquanto que em 2020 chegamos na casa dos 2 mil novos casos diários, em 2021 essa máxima foi quebrada e mais que dobrada, para mais de 4 mil novos casos diários. Isso é visível nos gráficos postados acima.

**Houve picos de óbitos novos em Junho/Julho de 2020 e Abril/Maio de 2020**

Mas ao contrário do que aconteceu com os casos novos, os picos de óbitos novos tiveram a mesma ordem de grandeza, na casa dos 120 óbitos novos diários. O que explica essa diferença? Levanto duas hipóteses:
- Melhora na eficiencia dos tratamentos.
- Em termos relativos, os óbitos novos diários são pequenos em comparação com os casos novos diários, o dificutaria uma correlação mais alta entre as duas variáveis. E com efeito, ao estudarmos a função de correlação cruzada entre as duas variáveis, vimos que a correlação máxima é de apenas 0.54, que é pouco significativa.
- Outros fatores biológicos, técnicos, e\ou socioeconômicos podem estar envolvidos, como por exemplo:
  - Taxa de mortalidade de variantes distintas do vírus
  - Inconsistência na coleta/processamento nos dados
  - Faixas etárias e classes da população afetada

**Os casos e óbitos novos (diários e semanais) estão em tendência de queda, nas últimas seis semanas**

Isso é visível pelos gráficos dos valores absolutos. No entanto, essa queda pode ter sido breve, visto que podemos estar vivenciando um novo período de aumento. É preciso observar os dados das próximas semanas. 
Mas a queda recente é inegável e inesperada, em termos puramente de dados brutos: os modelos preditivos do Prophet não foram capazes de prever essa queda repentina. De acordo com os modelos, era de se esperar que a tendência de aumento vivenciada até seis semanas atrás continuasse. 

