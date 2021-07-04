# Apresentação
## Sobre o repositório
Esse repositório contém o Projeto Final do Módulo 03 do Bootcamp Data Science da Alura: Análise de séries temporais.
O projeto foi dividido em 4 notebooks:
- [Extração de dados](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/blob/main/notebooks/Projeto_Bootcamp(Modulo03)_Extra%C3%A7%C3%A3o_dos_dados.ipynb) ----> É feita a extração dos dados de covid no Ceará do bando com os dados de todo o Brasil
- [Análise com Prophet](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/blob/main/notebooks/Projeto_Bootcamp(Modulo03)_An%C3%A1lise_Prophet.ipynb) ---> Fazemos a análise de séries temporais usando Facebook Prophet
- [Análise de tendências](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/blob/main/notebooks/Projeto_Bootcamp(Modulo03)_An%C3%A1lise_de_tend%C3%AAncias.ipynb) ----> Usamos algumas ferramentas para fazer um estudo de tendências e pontos de virada.
- [Melhores hiperparâmetros](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/blob/main/notebooks/Projeto_Bootcamp(Modulo03)_Melhores_hiperpar%C3%A2metros.ipynb) ----> Notebook auxiliar, para encontrar os melhores hiperparâmetros dos modelos do Prophet

Os dados utilizados se encontram nessa [pasta](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/tree/main/dados).

## Sobre o Módulo 03
O objetivo desse módulo foi conhecer mais sobre séries temporais. Foi apresentado o Prophet, uma ferramenta desenvolvida pelo Facebook para análise de séries temporais. O módulo foi estruturado em 6 aulas:
- Entendendo a série temporal
- Primeiras previsões
- Mudança de tendência
- Feriados e sazonalidade
- Outliers e validação

# O projeto: Covid no Ceará - Um estudo de séries temporais 
## Introdução

O objetivo desse projeto é fazer uma análise de séries temporais relacionadas aos casos de covid no estado do Ceará. As séries analizadas (bem como algumas médias móveis) serão:

-  Casos novos de covid
-  Casos acumulados de covid
-  Óbitos novos por covid
-  Óbitos acumulados por covid


A análise será dividida em dois momentos. Na primeira parte, feita neste [notebook](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/blob/main/notebooks/Projeto_Bootcamp(Modulo03)_An%C3%A1lise_Prophet.ipynb), usando o Prophet, uma biblioteca desenvolvida pelo Facebook, para análise e previsões de séries temporais. Exploraremos alguns de seus recursos, como identificação de sazonalidade, feriadados e pontos de virada. Também usaremos métricas para mensurar a precisão das previsões feitas pelo Prophet.
Na segunda parte, que se encontra nesse [notebook](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/blob/main/notebooks/Projeto_Bootcamp(Modulo03)_An%C3%A1lise_de_tend%C3%AAncias.ipynb), faremos uma análise mais minuciosa das tendências em séries temporais, utilizando técnicas para identificar pontos de virada e tendências de crescimento e decrescimento. Para isso exploraremos conceitos como derivadas discretas, indicador supertrend e cruzamento de médias móveis, bem como o uso de aproximações poligonais. Isso será feito em um segundo notebook, confira o [repositório do projeto do Github](https://github.com/renanmath/Bootcamp_Projeto_Modulo03).
Os dados utilizados foram baixados do site [Brasil.io](https://brasil.io/dataset/covid19/caso_full/) e tratados em um [notebook separado](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/blob/main/notebooks/Projeto_Bootcamp(Modulo03)_Extra%C3%A7%C3%A3o_dos_dados.ipynb). Eles foram salvos em formato csv e foi feito o upload para esta [pasta do repositório](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/tree/main/dados). 

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

## Análise de tendências e pontos de virada
Nesse outro notebook realizamos um estudo sobre tendências e pontos de virada em séries temporais.

Grosso modo, podemos dizer que uma série temporal apresenta três grandes padrões de tendência, bem autoexplicativos:
- Tendência de alta
- Tendência de baixa
- Tendência estacionária ou lateralizada

Obviamente, estando em qualquer uma dessas tendências, a série pode oscilar para cima ou para baixo. A esse fenômeno chamamos de volatilidade. Existem séries temporais mais voláteis, outras menos voláteis. E existem métricas ou indicadores que mensuram a volatilidade.

É claro também que a tendência de uma série depende da janela de tempo que estamos considerando. Como dito acima, cada ciclo de alta/baixa/lateralização é formada por ciclos menores. Em uma janela de tempo de um mês, por exemplo, podemos observar uma tendência de baixa, enquanto que se considerarmos a série anualmente, ela está em tendência de alta. 

Independente disso, reversões de tendência ocorrem, e podemos utilizar alguns sinais para saber (com certa precisão, em geral atrasada) quando ocorrem. Esses momentos onde temos uma mudança da tendência chamamos de pontos de virada (*change points*). 

Utilizamos três ferramentas na identificação de tendências:

### Derivada (discreta)

A derivada é um conceito do cálculo diferencial. Grosso modo, é uma função que mede a taxa de variação de outra função. No caso de séries temporais, por estarmos lidando com dados discretos, esse conceito não se aplica ***ipsis litteris***. No entanto, o conceito de taxa de variação média é conhecido, e isso é apenas outro nome para a chamada derivada discreta. 

Em cálculo diferencial, é conhecido o seguinte resultado: pontos de máximo e mínimo locais tem derivada nula. Sabemos também que, com hipóteses razoáveis sobre a função, em pontos de máximo e mínimo temos reversão de tendência (crescente para decrescente ou vice-versa). 

Então faz sentido utilizar algo semelhante para estimar a localização de pontos de virada em séries temporais. O resultado é algo assim:

![derivada e pontos de virada](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/raw/main/imagens/mm28_casos_novos_pv.jpg)

As linhas pontilhadas verticais indicam pontos de virada (nessa abordagem, pontos onde a segunda derivada discreta inverte de sinal). Mais detalhes no notebook.

**Indicador SuperTrend**

Utilizado no mercado de ações, esse é um indicador do tipo bandas. Ele acompanha a tendência geral de uma série temporal, mas estabelece bandas inferior e superior, que podem ser intepretadas como suporte e resistência. Se a série cruza uma banda superior para cima, ele rompe a resistência e o que se espera é que entre em tendência de alta. Por outro lado, se a série cruza a banda inferior para baixo, espera-se uma tendência de baixa.

Nesse projeto, vamos adaptar esse indicador para as séries que temos. O resultado é algo assim:

![supertrend dos casos acumulados](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/raw/main/imagens/supertend_casos_acumulados.jpg)

Nesse gráfico, podemos considerar como pontos de virado os pontos onde a série (em azul) toca a banda superior (em vermelho). Mais detalhes no notebook.

**Cruzamento de médias móveis**

Médias móveis são um tipo de indicador seguidor de tendência. Como o próprio nome diz, elas acompanham a série temporal, tentando mensurar a tendência geral da mesma. Mas as médias móveis podem ter diferentes períodos. Aquelas com períodos mais curtos tendem a ter maior volatilidade, sendo bem próximas da série original. Já as de período mais longo tendem a ser mais suaves, ditanto uma tendência de longo prazo da série. 
Médias móveis mais curtas são mais sensíveis a mudanças de tendência. Séries longas são menos sensíveis e só revertem quando a mudança de tendência é realmente forte. 
A mágica acontece quando elas se cruzam. A leitura é a seguinte:
- Média curta cruzando a média longa para cima ---> indicação de início de tendência de alta.
- Média curta cruzando a média longa para baixo ---> indicação de início de tendência de baixa.

O resultado é algo assim:

![cruzamento de médias móveis](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/raw/main/imagens/cruzar_mm_casos_novos.jpg)

As linhas pontilhadas verticais indicam pontos onde a média móvel curta cruzou a média móvel longa para cima (tendência de alta) e as linhas pontilhadas verticais avermelhadas indicam pontos onde a média móvel curta cruzou a média móvel longa para baixo (tendência de baixa).


Além disso, exploramos também as **aproximações poligonais**. É uma maneira bem visual de ver os pontos de virada. Após identificar esses pontos no gráfico da série temporal, ligamos esses pontos por linhas retas. O resultado é algo assim:

![aproximação poligonal - casos novos de covid](https://github.com/renanmath/Bootcamp_Projeto_Modulo03/raw/main/imagens/aprox_poligonal_casos_novos.jpg)

A inclinação dessas retas pode ser uma forma de mensurar a taxa de crescimento (ou decrescimento) entre dois pontos de virada. 

## Conclusão final e projetos futuros
O principal ponto observado ao longo desse trabalho, e que foi confirmado pelas análise é esse:

**Os casos novos diários e óbitos novos diários de covid no estado do Ceará estão em tendência de queda, quebrando uma forte onda de alta.** 

(Sempre lembrando que os dados são de 2 semanas atrás)

Hipóteses levantadas:
- Consequência da campanha de vacinação, que está avançando rápido no estado.
- Dados incompletos. 

Nenhuma dessas hipóteses foi testada nesse projeto, mas poderá ser tema de estudos futuros. 


Outros temas relacionados que podem vir a ser trabalhados em futuros projetos:
- Analisar o impacto das medidas de isolamento social nos casos novos diários. 
- Desenvolver um projeto contínuo de análise e previsão de novos casos, usando o Prophet e as técnicas discutidas nesse notebook, atualizado semanalmente. Divulgar os resultados em alguma mídia. 
- Analisar o impacto da covid nos diversos setores econômicos. 
- Fazer a mesma análise a nível municipal. O município escolhido será Caucaia, minha cidade natal.

Além dos projetos em si, pretendo trabalhar mais nas funções aqui desenvolvidas, para melhorar seus códigos. Dentre as melhorias já planejadas:
- Criar uma função que plota a aproximação poligonal, tendo como base os pontos de virada identificados pelo SuperTrend.
- Para as funções que plotam os pontos de virada, criar um hiperparâmetro novo, que receberá uma lista de datas. A função também plotará essas datas junto com os pontos de viradas e será possível comparar os dois conjuntos de datas. Isso será útil, por exemplo, para estudar o impacto do isolamento social. Na lista de datas podemos inserir as datas de início e término dos lockdowns e ver se eles coincidem com algum ponto de virada. 
- Melhorar o código das funções TR, ATR e SuperTrend, que ainda não estão se comportado como deveriam. 

# Contato
Deixo aqui meus contatos, caso alguém queira trocar uma ideia sobre o projeto ou sobre ciência de dados em geral. Ou ainda sobre matemática. 
- [Linkedin](https://www.linkedin.com/in/renan-santos-5a24aa50/)
- [Github](https://github.com/renanmath)
- [Canal no YouTube sobre matemática](https://www.youtube.com/channel/UCJqOzdlOTtu4UPJ2cW5RUTw)



