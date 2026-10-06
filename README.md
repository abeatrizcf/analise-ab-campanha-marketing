# Projeto 4 — Análise de efetividade de uma campanha de marketing

## Contexto e Problema de Negócio

O time de marketing de uma empresa realizou uma campanha de marketing e deseja verificar se, de fato, ela é efetiva. Para isso, serão analisadas as conversões dos usuários após a realização da mesma. Além disso, um grande desafio é compreender se aquela conversão ocorreu devido a influência da campanha ou se já aconteceria de forma orgânica, isto é, análise de incrementalidade. Sem medir a incrementalidade real, a empresa corre o risco de queimar verba em usuários que já converteriam normalmente.

## Objetivo do Projeto

* Avaliar se a campanha foi efetiva na geração de conversões de clientes;
* Comparar as taxas de conversão entre o Grupo de Tratamento (exposto aos anúncios) e o Grupo de Controle (não exposto aos anúncios);
* Verificar a significância estatística da diferença observada;
* Calcular o lift absoluto e relativo da campanha;
* Estimar o impacto incremental da publicidade, ou seja, quantas conversões aconteceram a mais por causa da publicidade;
* Transformar os resultados em insights e recomendações para tomada de decisão.
* Visualização dos dados obtidos com as bibliotecas MatPlotLib e Seaborn

---

# Planejamento da Solução

O projeto será executado nas seguintes etapas:

### Passo 01: Definição do Problema de negócio

Qual resultado esperado ao final do teste? Qual a métrica objetivo do experimento?

### Passo 02: Design do Experimento

**2.1 Formulação das hipóteses:** composto pela definição da Hipótese Nula e da hipótese alternativa. Em seguida, a escolha do tipo de teste sendo ele unicaudal ou bicaudal. Por fim, a definição do nível de confiança do experimento.

**2.2 Escolha da variável:** Definição da métrica de avaliação e/ou variável dependente.

**2.3 Separação dos grupos:** Separação do grupo de controle e de tratamento e definição do tamanho da amostra de cada grupo.

### Passo 03: Coleta e limpeza dos dados

Nessa etapa, os dados são coletados. Para isso, define-se a estrutura de coleta e armazenamento dos dados, é criada a flag do A/B e escolhidas as ferramentas de teste A/B. Em seguida, os dados são limpos e verificados e por fim, é realizado o cálculo da métrica escolhida para o grupo controle e para o grupo de tratamento.

### Passo 04: Testando as Hipóteses

Definição de qual método de inferência estatística será utilizado (t-test, anova, chi-squared) e cálculo do p-valor.

### Passo 05: Conclusões e Insights

Interpretação do p-valor comparando-o com o nível de confiança e cálculo de outras métricas que o projeto nos revela.

### Passo 06: Visualização dos dados

Utilização de uma ferramenta de visualização para transmitir o que os dados contam.

---

# Etapas e Execução do projeto

## Etapa 01 — Definição do Problema de negócio

Avaliar se a campanha de marketing é eficaz baseado na taxa de conversão dos clientes dos grupos de controle e de tratamento. Em caso afirmativo, a empresa deve continuar investindo renda na campanha de marketing.

---

## Etapa 02 — Design do Experimento

### 2.1 Formulação das Hipóteses

No início do design do experimento foi estabelecido:

### 2.2 Escolha das variáveis

Em seguida, as variáveis foram definidas.

### 2.3 Separação dos grupos

Nessa etapa, foi usado o cálculo do tamanho amostral mínimo teórico para definir a menor quantidade de dados necessária nas amostras para que os resultados sejam confiáveis e representativos.

Para realizar esse cálculo para achar o tamanho mínimo da amostra, foi utilizada a biblioteca Statsmodels do Python. Foram consideradas uma taxa de conversão de referência (baseline) de 5%, um efeito mínimo detectável (MDE) de 1 ponto percentual, nível de significância de 5%, poder estatístico de 80%, teste bicaudal e proporção de 1:1 entre os grupos de tratamento e controle. O cálculo permite estimar a quantidade mínima de usuários necessária em cada grupo para que o experimento tenha o poder estatístico planejado para detectar o efeito definido.

O código utilizado para chegar no valor de n está no arquivo `tamanhoAmostralMinimo.ipynb`

Com isso, o valor alcançado foi um valor mínimo de 8142 amostras.

---

## Etapa 03 — Coleta e limpeza dos dados

O banco de dados Marketing A/B Testing disponível no Kaggle.

A flag do A/B será a coluna “test grupo” e a ferramenta de teste utilizada será a biblioteca Statsmodels do Python. Em seguida, como demonstrado no arquivo `exploracaoDados.ipynb` foi realizado a verificação dos dados do banco e por fim, é realizado o cálculo da taxa de conversão de clientes para o grupo controle e para o grupo de tratamento.

Nessa etapa, nota-se que a quantidade de amostras do grupo que viu a propaganda corresponde a 564.577 e a que não viu, 23.524. Nota-se que o banco está bem acima do valor mínimo de teórico de amostras calculado na etapa 02. Por fim, essa etapa é finalizada com o cálculo da métrica escolhida, a taxa de conversão, de cada grupo, chegando no seguinte resultado:

**Taxa de conversão com propaganda: 2.555%**

**Taxa de conversão sem propaganda: 1.785%**

---

## Etapa 04 — Testando as Hipóteses

Nessa etapa, foi definido o Z-test como método de inferência estatística. A escolha foi devido ao fato de estamos comparando uma proporção (taxa de conversão) entre dois grupos independentes. Em seguida, será calculado o p-valor e o Z-stat:

**Estatística Z: 7.3701**

**P-valor: 1.71e-13**

Os cálculos acima estão no arquivo `analiseTesteAB.ipynb`

---

## Etapa 05 — Conclusões e Insights

Nessa etapa, será realizada a Interpretação do p-valor comparando-o com o nível de significância. Nota-se que 1.71e-13 é muito menor do que o nível de significância, é chegada a conclusão que **REJEITAMOS A HIPÓTESE NULA**.

Nessa etapa, também foi calculado o ganho incremental estimado, ou seja, aquele que estima-se como oriundo da utilização das propagandas. Além disso, também foi calculada a conversão orgânica estimada. Isto é, aquela esperada independe do uso de anúncios. Sabe-se que o banco contém 564577 registros com propaganda (dos quais 14 423 se converteram) e 23524 registros sem propaganda (dos quais 420 se converteram). Pode-se calcular que a diferença das taxas de conversão é 0.7692%. Aplicando essa taxa nos registros com propaganda, nota-se um ganho incremental de 4343 conversões. Também nota-se uma conversão orgânica estimada de 10.080 conversões.

Esses dados a respeito do ganho incremental e das conversões orgânicas também estão presentes no arquivo `analiseTesteAB.ipynb`.

---

## Etapa 06 — Visualização dos dados

Nessa etapa, foram usadas as bibliotecas MatPlotLib e Seaborn. Os códigos estão presentes no notebook `visualizacaoDados.ipynb`.

---

# Principais Insights de Negócio

💡 O teste de hipótese realizado a partir do experimento A/B, utilizando o teste Z para comparação de duas proporções demonstrou que o aumento do número de conversões visto no grupo de tratamento não aconteceu por acaso, mas sim, por influência do uso da propaganda. Sendo assim, a partir da observação do p-valor, a hipótese nula, ou seja, que a taxa de conversão de ambos os grupos são iguais, é rejeitada seguramente já que o P-valor: 1.71e-13 < 0,05 (nível de significância).

💡 A taxa de conversão do grupo com propaganda foi de 2.5547%, enquanto a do grupo de controle (sem propaganda) ficou em 1.7854%. Isso representa um aumento de aproximadamente 43,09% na taxa de conversão (o que corresponde ao lift relativo da campanha).

💡 Além disso, nota-se um lift absoluto de 0,7693 pontos percentuais (taxa de conversão com propaganda - a taxa de conversão sem propaganda).

💡 Por fim, estima-se que o uso das propagandas gerou 4.343 conversões a mais o que corresponde a aproximadamente 30,11% das conversões do grupo de tratamento.

---

# Conclusão e próximos passos

A partir do teste A/B, conclui-se que a campanha de marketing desenvolvida pelo time de marketing foi efetiva. Essa afirmação pode ser constatada a partir do Z-stat e do p-valor menor que o nível de significância. Além disso, a taxa de conversão aumentou 43,09% comparando os valores sem e com a campanha.

A incrementalidade real da campanha demonstra que dentre as conversões ocorridas no grupo que teve acesso à campanha de marketing 30,11% das conversões são estimadas como incrementais. Dessa forma, há evidências iniciais que é válido continuar investindo na realização da campanha realizada pelo time de marketing. Porém, como próximo passo, recomenda-se avaliar os custos da campanha e os valores financeiros concretos que ela refletiu.
