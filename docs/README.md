# RELATÓRIO ANALÍTICO: Evasão dos Alunos das Academias
---

**Nomes:** Davi Amâncio, Italo Nascimento, Henrique Valle, Matheus Lopes
**Instituição:** CEUB - Centro Universitário de Brasília
**Curso:** Ciência de Dados e Machine Learning
**Turno:** Matutino
**Matéria:** Projeto Integrador II
**Período:** 1º/2026 (6/7º Semestre)
**Professor(a):** Weslley Rodrigues da Silva

---

## 1. Introdução

### 1.1 Contextualização do Problema

O aumento da procura por academias de ginástica nas últimas décadas demonstra a crescente preocupação da população com saúde e bem-estar. Entretanto, um dos principais desafios enfrentados por essas instituições é a alta taxa de evasão de alunos. Muitos se matriculam, mas abandonam as atividades em poucos meses, o que impacta diretamente a receita e dificulta o planejamento de recursos humanos e operacionais.

Com o avanço das tecnologias de análise de dados e aprendizado de máquina, surge a possibilidade de compreender padrões de comportamento e prever, com antecedência, quais alunos apresentam maior propensão ao abandono. Esse cenário motiva o desenvolvimento deste projeto, que busca propor uma abordagem para prever a evasão em academias a partir de dados históricos e comportamentais dos alunos.

### 1.2 Justificativa

A evasão representa um problema relevante tanto sob a ótica econômica quanto sob a perspectiva de gestão e relacionamento com o cliente. Para o setor fitness, compreender os fatores que levam um aluno a abandonar a academia é essencial para otimizar estratégias de retenção e melhorar a experiência do usuário.

### 1.3 Objetivo Geral

Desenvolver uma solução aplicada de Ciência de Dados e Aprendizado de Máquina para previsão de evasão de alunos em academias, visando identificar padrões comportamentais e apoiar a tomada de decisões estratégicas voltadas à retenção de clientes.

### 1.4 Objetivos Específicos

- Levantar e compreender os fatores que influenciam a evasão em academias;
- Propor uma estrutura de dados e pipeline analítico para coleta e processamento das informações;
- Definir, treinar e avaliar o modelo preditivo (artefato aplicado); e
- Identificar contribuições científicas e práticas do modelo proposto.

---

## 2. Análise Exploratória de Dados (EDA)

### 2.1 Coleta e Tratamento dos Dados

Este relatório foi feito baseado em um dataset de evasão dos alunos das academias disponibilizado publicamente no Kaggle, sobre evasão de alunos das academias.

<img width="945" height="215" alt="image" src="https://github.com/user-attachments/assets/dd2577fe-7c38-4b2a-add8-d530343d8651" />

Olhando o dataset logo de início, percebemos que aqui, verificamos que o dataset atual possui uma amostra de 4.000 linhas e 14 colunas distintas, com colunas teoricamente suficientes para realizar uma análise.

<img width="945" height="133" alt="image" src="https://github.com/user-attachments/assets/1463d5e1-dd45-45fe-942b-109beeec480e" />

Como vimos acima, temos apenas uma pequena quantidade de outliers. Sendo assim, podemos garantir que não irão gerar interferência significativa ao resultado da análise.

Baseado nas informações obtidas e por estudos externos sobre cada atributo do dataset, montamos um dicionário de dados sobre.

### 2.2 Dicionário de Dados

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

### 2.3 Visualização e Interpretação

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

---

## 3. Modelagem e Treinamento de Machine Learning

Antes do treinamento dos modelos com as features derivadas, foi realizada uma etapa de engenharia de atributos, criando variáveis que combinam sinais de diferentes colunas originais. Entre as principais, destacam-se: `Frequencia_ATUAL_menos_TOTAL` (diferença entre a frequência do último mês e a frequência histórica, capturando quedas recentes de engajamento) e `Esforco_Total_Academia` (produto entre a frequência semanal e o tempo de permanência, medindo o esforço acumulado do aluno na academia). Essas variáveis derivadas se mostraram as mais relevantes entre todos os atributos, conforme indicado no gráfico de importância de atributos (Seção 2.3).

### 3.1 Decision Tree

<img width="945" alt="Decision Tree v1 — Somente Features Originais" src="https://github.com/user-attachments/assets/c4f1581c-2b24-49a1-af2c-1e427d4c7a8a" />

<img width="945" alt="Decision Tree v2 — Features Originais + Engineered" src="https://github.com/user-attachments/assets/ca6cc2a3-4e66-48ab-885d-a71572a415bb" />

Modelos treinados:

- DT v1 - só com as 13 features originais (max_depth=5, min_samples_leaf=30, class_weight='balanced')
- DT v2 - originais + as 8 features engineered do notebook
- CatBoost - exatamente com os hiperparâmetros do best dict que já tinhamos

<img width="945" alt="Comparação de Modelos — Previsão de Evasão em Academias" src="https://github.com/user-attachments/assets/dd60e470-6de7-44da-a239-1f2d10d2a80b" />

**Comparação entre os modelos:**

**DT v1 originais:**

Métricas mais baixas, mas as regras são 100% legíveis. Cada nó da árvore é uma frase de perfil - "aluno com menos de 4 meses de casa E frequência abaixo de 2x/semana → 81% de chance de evadir". Valor do projeto: mapear o perfil, não maximizar performance.

**DT v2 + engineered:**

Performance melhor que v1. As features derivadas condensam sinal de múltiplas variáveis originais. A árvore vai usar Esforco_Total_Academia e Tempo_casa_x_Frequencia como galhos principais - o que faz sentido biologicamente, mas torna a interpretação um pouco menos direta para um gestor de academia.

**CatBoost + engineered:**

É o modelo com as melhores métricas absolutas: Accuracy ≈ 0,96, F1-Score ≈ 0,92 e ROC-AUC ≈ 0,98, superando as duas árvores em todos os indicadores agregados. Não é interpretável, mas valida que as features que criamos realmente têm poder preditivo. No entanto, ao calcularmos o recall isoladamente — métrica mais crítica para o negócio, pois mede a capacidade de capturar quem de fato vai evadir — a DT v2 atinge 0,925, superando o próprio CatBoost (0,906) e a DT v1 (0,877). Isso confirma que a árvore interpretável não só é suficiente, como é a melhor opção nesse cenário: não há necessidade do modelo caixa-preta.

### 3.2 Interpretação dos Resultados

**As Regras da Árvore — o Perfil do Aluno que Evade**

A árvore identificou automaticamente os seguintes perfis de risco, em ordem de prioridade:

**Perfil 1 — O mais crítico (maior probabilidade de evasão):**

Lifetime ≤ 2.5 meses + Month_to_end_contract ≤ 2.5 + Frequência atual ≤ 2.34x/semana + Idade ≤ 31 anos → classe Evade

Traduzindo: aluno novo (menos de 2.5 meses na academia), com contrato quase vencendo, que já reduziu a frequência para menos de 2 vezes por semana e tem menos de 31 anos. Esse é o candidato mais óbvio a sair — a academia deveria ter um protocolo de retenção disparado automaticamente para esse grupo.

**Perfil 2 — Jovem sem engajamento inicial:**

Lifetime ≤ 2.5 + Month_to_end_contract > 2.5 + Idade ≤ 29.5 + Lifetime ≤ 1.5 + Frequência atual ≤ 2.17x/semana → classe Evade

Aluno com menos de 1.5 mês de academia, jovem (até 29 anos), ainda tem tempo de contrato mas já frequenta menos de 2x por semana. O contrato não venceu ainda, mas o comportamento já sinaliza abandono iminente. A janela de intervenção aqui é maior — há tempo para agir antes do vencimento.

O que a árvore não capturou diretamente mas está implícito nas regras: o Lifetime aparece como primeiro nó em todos os caminhos de evasão. Isso confirma o que o EDA já havia sugerido: os primeiros 2.5 meses são o período mais crítico da jornada do cliente. Qualquer cliente que sobrevive esse período com frequência razoável tem probabilidade muito maior de permanecer.

**Possíveis soluções:**

1. Sistema de alerta em 3 variáveis: monitorar Lifetime, Month_to_end_contract e Avg_class_frequency_current_month. Quando os três estiverem nos thresholds da árvore simultaneamente, disparar um alerta para o gestor.
2. Segmentação de risco: os perfis identificados permitem criar grupos de intervenção com intensidades diferentes — alunos no Perfil 1 recebem contato imediato, Perfil 2 recebem um check-in menos urgente.
3. KPI de retenção: com o recall de 0,877 (DT v1) — ou 0,925 considerando a DT v2 — a academia poderia medir a efetividade das intervenções comparando a taxa de evasão antes e depois de implementar os alertas.

---

## 4. CONCLUSÃO

O projeto cumpriu o objetivo geral proposto: desenvolver uma solução de Ciência de Dados e Machine Learning capaz de identificar, com alta sensibilidade, os alunos com maior propensão à evasão em academias, a partir de seus dados comportamentais e contratuais.

A análise exploratória revelou que a evasão não é explicada por um único fator, mas por um conjunto de variáveis comportamentais - tempo de permanência (Lifetime), frequência de treino no último mês, idade e duração do contrato - que juntas formam um perfil de risco bem definido: alunos jovens (até 31 anos), nos primeiros 2,5 meses de academia, com contrato próximo do vencimento e frequência semanal em queda. Variáveis cadastrais como gênero e telefone se mostraram irrelevantes, reforçando que a retenção deve ser tratada como um problema comportamental, não demográfico.

Na etapa de modelagem, a comparação entre os três modelos (DT v1, DT v2 e CatBoost) confirmou que as features de engenharia criadas - como o cruzamento entre frequência atual e histórica, e o esforço acumulado na academia - carregam sinal preditivo real: o CatBoost, modelo de maior performance absoluta (Accuracy ≈ 0,96 / ROC-AUC ≈ 0,98), validou esse ganho, mas foi a Decision Tree v2 que apresentou o maior recall entre todos os modelos (0,925), superando inclusive o CatBoost. Esse resultado é o achado mais relevante do ponto de vista prático: um modelo interpretável, cujas regras podem ser traduzidas em frases de perfil compreensíveis por um gestor de academia, é capaz de superar um modelo caixa-preta na métrica mais crítica para o negócio - detectar o máximo de alunos que realmente vão evadir.

Como contribuição prática, o projeto propôs um sistema de alerta de três variáveis e uma segmentação de risco em dois perfis de prioridade, permitindo que a academia direcione esforços de retenção de forma proporcional à urgência de cada caso, em vez de campanhas genéricas.

Como limitação, destaca-se que o dataset utilizado é público e estático, sem informações longitudinais reais de uma academia específica nem dados de campanhas de retenção já testadas - o que impede, por ora, validar o impacto real das soluções propostas em um cenário de produção.

Quanto à etapa atual do projeto, a fase de coleta, tratamento, análise exploratória e modelagem está concluída, restando como próximos passos: 1- a consolidação final do relatório com a inclusão dos pontos de melhoria identificados; II- a preparação da apresentação para a banca; e III- como sugestão de trabalho futuro, a validação do modelo em um cenário com dados reais e monitoramento de um teste A/B do sistema de alertas proposto.
