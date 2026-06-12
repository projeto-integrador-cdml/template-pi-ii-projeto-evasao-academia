RELATÓRIO ANALÍTICO: Evasão dos Alunos das Academias


Este relatório foi feito baseado em um dataset de evasão dos alunos das academias disponibilizado publicamente no Kaggle, sobre evasão de alunos das academias.

Olhando o dataset logo de início, percebemos que aqui, verificamos que o dataset atual possui uma amostra de 4.000 linhas e 14 colunas distintas, com colunas teoricamente suficientes para realizar uma análise.


Como vimos acima, temos apenas uma pequena quantidade de outliers. Sendo assim, podemos garantir que não irão gerar interferência significativa ao resultado da análise.

Baseado nas informações obtidas e por estudos externos sobre cada atributo do dataset, montamos um dicionário de dados sobre.

Dicionário de Dados:
gender: Gênero do cliente (0 = Homem, 1 = Mulher).
Near_Location: Indica se o cliente mora ou trabalha no mesmo bairro onde a academia está localizada (0 = Não, 1 = Sim).
Partner: Indica se o cliente é funcionário de uma
empresa parceira da academia (empresas conveniadas que oferecem
descontos aos funcionários) (0 = Não, 1 = Sim).
Promo_friends: Indica se o cliente se inscreveu
originalmente através de uma oferta "indique um amigo" (usando um código
promocional de um conhecido) (0 = Não, 1 = Sim).
Phone: Indica se o cliente forneceu o número de telefone no cadastro (0 = Não, 1 = Sim).
Contract_period: Duração do contrato atual em meses (ex: 1, 6 ou 12 meses).
Group_visits: Indica se o cliente participa de aulas ou sessões em grupo (0 = Não, 1 = Sim).
Age: Idade do cliente em anos.
Avg_additional_charges_total: Média de gastos totais em serviços adicionais da academia (cafeteria, massagem, loja de produtos, etc.).
Month_to_end_contract: Quantidade de meses restantes até o término do contrato atual.
Lifetime: Tempo de permanência (em meses) desde a primeira visita à academia.
Avg_class_frequency_total: Frequência média de visitas por semana desde que o cliente se matriculou.
Avg_class_frequency_current_month: Frequência média de visitas por semana durante o último mês.
Churn: Variável alvo que indica se o cliente cancelou a matrícula no mês atual (0 = Permaneceu, 1 = Cancelou/Saiu).
Feito tudo isso, partimos então para a parte de visualização de dados na análise:


Aqui neste gráfico, a imensa maioria dos clientes que evadem concentram seus gastos acumulados na faixa de R$ 0 a R$ 100. Essa variável apresentou uma correlação negativa baixa em relação à evasão, mas é interessante notar que clientes com menor gasto tendem a não permanecer.
Algumas hipóteses a serem levantadas, pode ser que a assinatura foi para conhecer o ambiente e por isso optou-se por um plano mais barato, ou as atividades ofertadas não eram do agrado desses clientes e abandonaram o serviço.
O gasto extra é um excelente indicador de pertencimento. O cliente que compra um suplemento, uma água ou paga por um serviço extra vê valor no ecossistema da academia. Quem não gasta nada extra, já está com um pé fora da empresa.


Aqui é notável, e faz bastante sentido do ponto de vistacomportamental que a grande maioria das pessoas deixa de ir quando falta um mês ou menos para o encerramento do contrato. Com uma leve curva em torno dos 6 meses também.
Esperar o último mês para tentar renovar com o cliente é um erro fatal. A jornada de renovação precisa começar meses antes, principalmente para quem está no plano semestral.


Ainda nessa mesma temática de meses de contrato, há um pico de abandono em torno de 0 e 2 meses. Superando esse período inicial, o aluno tende a permanecer, e quanto mais longo o período de presença, menor tende a ser a evasão. A academia tem um vale na recepção. O atendimento falha em acompanhar o aluno novato no momento mais crítico: o início, quando ele ainda não criou o hábito de treinar.


Já aqui é notável, e faz bastante sentido, que a frequência semanal seja reduzida de 1 a 2 treinos por semana para quem deixa de frequentar a academia. O que sinaliza para baixo interesse naquela atividade específica, ou alguma outra dificuldade na vida do aluno, aumentando o índice de evasão. Um cliente que costumava ir 3 vezes ou mais na semana e cai para 2, 1 ou 0 é um alerta vermelho pro negócio. A ausência física é o sintoma que antecede o cancelamento contratual.


Por último, este gráfico mostra quais atributos tem mais impacto na evasão:
O primeiro atributo se torna o mais importante porque quanto mais o aluno permanece na academia, mais engajado e motivado ele está nas atividades, diminuindo bastante a chance de evasão.
Já o esforço total entra em segundo lugar, pois é a medida da quantidade de treinos semanal por mês vezes a quantidade de meses persistida na academia, demonstrando que quem mais fica na academia ao longo do tempo menos evade.
O terceiro, é o tempo de permanência mensal, que também conta da mesma forma.
E em quarto, a idade, onde jovens são mais propensos a saírem do que pessoas com mais de 30 anos.
