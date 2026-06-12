# RELATÓRIO ANALÍTICO: Evasão dos Alunos das Academias
---

Este relatório foi feito baseado em um dataset de evasão dos alunos das academias disponibilizado publicamente no Kaggle, sobre evasão de alunos das academias.

<img width="945" height="215" alt="image" src="https://github.com/user-attachments/assets/dd2577fe-7c38-4b2a-add8-d530343d8651" />

Olhando o dataset logo de início, percebemos que aqui, verificamos que o dataset atual possui uma amostra de 4.000 linhas e 14 colunas distintas, com colunas teoricamente suficientes para realizar uma análise.

<img width="945" height="133" alt="image" src="https://github.com/user-attachments/assets/1463d5e1-dd45-45fe-942b-109beeec480e" />

Como vimos acima, temos apenas uma pequena quantidade de outliers. Sendo assim, podemos garantir que não irão gerar interferência significativa ao resultado da análise.

Baseado nas informações obtidas e por estudos externos sobre cada atributo do dataset, montamos um dicionário de dados sobre.


### **Dicionário de Dados:**

- `gender:` Gênero do cliente (0 = Homem, 1 = Mulher).

- `Near_Location:` Indica se o cliente mora ou trabalha no mesmo bairro onde a academia está localizada (0 = Não, 1 = Sim).

- `Partner:` Indica se o cliente é funcionário de uma empresa parceira da academia (empresas conveniadas que oferecem descontos aos funcionários) (0 = Não, 1 = Sim).

- `Promo_friends:` Indica se o cliente se inscreveu originalmente através de uma oferta "indique um amigo" (usando um código promocional de um conhecido) (0 = Não, 1 = Sim).

- `Phone:` Indica se o cliente forneceu o número de telefone no cadastro (0 = Não, 1 = Sim).

- `Contract_period:` Duração do contrato atual em meses (ex: 1, 6 ou 12 meses).

- `Group_visits:` Indica se o cliente participa de aulas ou sessões em grupo (0 = Não, 1 = Sim).

- `Age:` Idade do cliente em anos.

- `Avg_additional_charges_total:` Média de gastos totais em serviços adicionais da academia (cafeteria, massagem, loja de produtos, etc.).

- `Month_to_end_contract:` Quantidade de meses restantes até o término do contrato atual.

- `Lifetime:` Tempo de permanência (em meses) desde a primeira visita à academia.

- `Avg_class_frequency_total:` Frequência média de visitas por semana desde que o cliente se matriculou.

- `Avg_class_frequency_current_month:` Frequência média de visitas por semana durante o último mês.

- `Churn:` Variável alvo que indica se o cliente cancelou a matrícula no mês atual (0 = Permaneceu, 1 = Cancelou/Saiu).


Feito tudo isso, partimos então para a parte de visualização de dados na análise:

<img width="1484" height="1075" alt="image" src="https://github.com/user-attachments/assets/98b4826c-4bfb-4ac5-9716-915797c1e23a" />

A Matriz de Correlação gerada aponta caminhos lineares diretos para o risco de cancelamento. Quatro variáveis destacam-se com fortíssimas correlações negativas com o Churn:

    Lifetime (-0.44): O tempo de permanência é o maior aliado contra o cancelamento.

    Avg_class_frequency_current_month (-0.41): A frequência de treinos no último mês é o termômetro em tempo real da desistência.

    Age (-0.40) e Contract_period (-0.39): Idades mais jovens e contratos curtos são sinônimos de instabilidade.

Todas as variáveis destacadas como negativas apresentam índices de correlação negativos médios, o que sugere que uma unica não seja suficiente para explicar a evasão, mas sim o conjunto delas, sugerindo que possívelmente exista um perfil de alunos que não permanecem naquela academia. Mapear esse perfil é de grande valor para o negócio.
<br>
<br>
Obs: Variáveis cadastrais como gênero (gender) ou o fato de registrar o telefone (Phone) têm correlação praticamente nula com o cancelamento. Focar em campanhas de marketing baseadas em gênero é perda de tempo e dinheiro; o foco da gestão tem que ser exclusivamente comportamental.

<img width="1406" height="875" alt="image" src="https://github.com/user-attachments/assets/9a3e3046-6ec5-4a0b-812a-cdd9fcbe567b" />

Neste histograma, alunos com tempo de contrato igual ou inferiores a um mês tendem a abandonar a academia com mais facilidade, enquanto contratos mais longos de 6 meses a 1 ano tendem a reter os alunos que são mais fiéis, resultando em evasões mais baixas nesses pontos.

A duração menos previsível é a de 6 meses demonstrando o perfil dos alunos que ou já permanecem em um plano de 12 meses ou mantém o plano de um mês, e que geralmente alegam fazer isso pra evitar rompimento de contrato caso queiram cancelar.

A quantidade total de alunos que assinam contratos curtos chega a ser mais de de 40% em média maior do que os demais, sendo uma importante fonte de receita para a academia.

Na duração de um mês a evasão é catastrófica, mais de 40%, quase metade dos clientes que entram no plano mensal desistem imediatamente. Este plano serve apenas como uma "porta giratória".

<img width="1401" height="874" alt="image" src="https://github.com/user-attachments/assets/880cfe7c-88d3-4911-98e6-46aece69297f" />

Neste gráfico, pessoas entre 24 e 30 anos são mais propensas a cancelar contratos, enquanto aquelas acima dos 30 são mais fiéis ao ambiente. A academia falha terrivelmente em engajar o público jovem. Eles são mais voláteis, provavelmente possuem rotinas menos estáveis e exigem um acompanhamento de integração (onboarding) muito mais agressivo do que o público maduro. Alguns fatores psicólógicos e sociais podem explicar esse fator, como a busca por novidades, a maior facilidade dos concorrentes em seduzir jovens, a instabilidade financeira e a possibilidade de mudanças drásticas no início da vida adulta (mudança de cidade, mudança de emprego, aquisição de família e outras responsabilidades).

<img width="1397" height="873" alt="image" src="https://github.com/user-attachments/assets/7c2d4cca-6181-4593-afac-7a1958a5d909" />

Aqui neste gráfico, a imensa maioria dos clientes que evadem concentram seus gastos acumulados na faixa de R$ 0 a R$ 100. Essa variável apresentou uma correlação negativa baixa em relação à evasão, mas é interessante notar que clientes com menor gasto tendem a não permanecer.
Algumas hipóteses a serem levantadas, pode ser que a assinatura foi para conhecer o ambiente e por isso optou-se por um plano mais barato, ou as atividades ofertadas não eram do agrado desses clientes e abandonaram o serviço.
O gasto extra é um excelente indicador de pertencimento. O cliente que compra um suplemento, uma água ou paga por um serviço extra vê valor no ecossistema da academia. Quem não gasta nada extra, já está com um pé fora da empresa.

<img width="1401" height="873" alt="image" src="https://github.com/user-attachments/assets/3057c794-dc22-4fa3-ac46-f12c5da9153a" />

Aqui é notável, e faz bastante sentido do ponto de vista comportamental que a grande maioria das pessoas deixam de ir quando falta um mês ou menos para o encerramento do contrato. Com uma leve curva em torno dos 6 meses também.
Esperar o último mês para tentar renovar com o cliente é um erro fatal. A jornada de renovação precisa começar meses antes, principalmente para quem está no plano semestral.

<img width="1401" height="873" alt="image" src="https://github.com/user-attachments/assets/6091b7fa-6eb0-42c8-ae94-03fa6e1a4d5a" />

Ainda nessa mesma temática de meses de contrato, há um pico de abandono em torno de 0 e 2 meses. Superando esse período inicial, o aluno tende a permanecer, e quanto mais longo o período de presença, menor tende a ser a evasão. A academia tem um vale na recepção. O atendimento falha em acompanhar o aluno novato no momento mais crítico: o início, quando ele ainda não criou o hábito de treinar.

<img width="1397" height="877" alt="image" src="https://github.com/user-attachments/assets/eb04d4e8-1b47-4ac0-b8f1-5adabea56b7c" />

Já aqui é notável, e faz bastante sentido, que a frequência semanal seja reduzida de 1 a 2 treinos por semana para quem deixa de frequentar a academia. O que sinaliza para baixo interesse naquela atividade específica, ou alguma outra dificuldade na vida do aluno, aumentando o índice de evasão. Um cliente que costumava ir 3 vezes ou mais na semana e cai para 2, 1 ou 0 é um alerta vermelho pro negócio. A ausência física é o sintoma que antecede o cancelamento contratual.

<img width="1619" height="856" alt="image" src="https://github.com/user-attachments/assets/6c524acc-02f6-44bd-b984-08ef33c81f9f" />

Por último, esse gráfico mostra quais atributos tem mais impacto na evasão:

1. O primeiro atributo se torna o mais importante porque quanto mais o aluno permanece na academia, mais engajado e motivado ele está nas atividades, diminuindo bastante a chance de evasão.

2. Já o esforço total entra em segundo lugar, pois é a medida da quantidade de treinos semanal por mês vezes a quantidade de meses persistida na academia, demonstrando que quem mais fica na academia ao longo do tempo menos evade.

3. O terceiro, é o tempo de permanência mensal, que também conta da mesma forma.

4. E em quarto, a idade, onde jovens são mais propensos a saírem do que pessoas com mais de 30 anos.
