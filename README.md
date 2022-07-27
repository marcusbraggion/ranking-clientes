# Previsão de clientes mais prováveis ​​para adquirir um seguro de veículo novo.

## Uma breve descrição do projeto

#### Este projeto foi feito por Marcus Bragion.

# 1. Problema de negócios.

Uma Empresa no ramo de Seguro de Automóveis decidiu iniciar uma estratégia de vendas, e para auxiliar a sua estratégia, a empresa considerou contratar uma Consultoria de Data Science para elaborar uma solução orientada a dados que resulte em uma base de clientes com maior propensão de contratar o serviço da Empresa diminuindo o custo da operação e aumentando sua receita.

Com essas informações em mãos, a empresa precisa que esclarecessem algumas questões. Dentre todas as características coletadas, quais evidenciam mais a intenção dos clientes em adquirir o seguro do carro?

1. Se a equipe de vendas conseguir fazer 20.000 ligações, qual fração dos clientes interessados ​​será alcançada?

2. Se a equipe de vendas agora puder fazer 40.000 ligações, qual fração dos clientes interessados ​​será alcançada?

3. Quantas ligações a equipe de vendas precisa fazer para atingir 80% dos clientes interessados?

Para responder a essas perguntas, o modelo de aprendizado de máquina (mais informações abaixo) deve informar a probabilidade de cada cliente adquirir o seguro do veículo, e o banco de dados deve ser classificado por essas informações. Tendo os clientes com maiores probabilidades no topo, as questões acima serão abordadas.

# 2. Premissas de Negócios.

id: ID exclusivo do cliente.

gender: Gênero do cliente.

age: Idade do cliente

driving_license: de condução: se o cliente tem carta de condução ou não.

region_code: Código exclusivo para a localização do cliente.

previously_insured: Se o cliente já possui seguro de veículo ou não.

vehicle_age: Idade do veículo.

vehicle_damage: Se o veículo sofreu danos no passado ou não.

annual_premium: O valor pago pelo cliente anualmente.

policy_sales_channel: Código anônimo para o canal de divulgação do cliente.

vintage: Quantidade de tempo (em dias) desde que o cliente está associado à empresa.

response: Se o cliente tem interesse em adquirir o seguro do veículo ou não.

# 3. Estratégia de Solução

A minha estratégia para resolver este desafio foi:

**Etapa 01. Descrição dos dados:** Eu trouxe informações da Dimensão dos Dados, pesquisei os NA, verifiquei os tipos de dados, adaptei alguns deles para analises e apresentei uma descrição estatística.

**Etapa 02. Feature Engineering:** Novos campos foram criados para possibilitar uma análise mais completa.

**Etapa 03. Filtragem de dados:** Foram filtradas as entradas sem informações ou com informações que não condizem com o escopo do projeto.

**Etapa 04. Análise Exploratória de Dados:** Realizei análises de dados univariados, bivariados, obtendo propriedades estatísticas de cada um deles, correlações e testando hipóteses (as mais importantes estão detalhadas na seção a seguir).

**Etapa 05. Preparação de Dados:** Essa etapa é necessária tanto para a seleção de recursos quanto para os modelos de aprendizado de máquina. Em relação aos tipos de dados, os dados numéricos foram reescalonados e os dados categóricos foram codificados para numéricos.

**Etapa 06. Seleção de recursos:** Os recursos estatisticamente mais relevantes foram selecionados usando algoritmo de arvore Extra Trees, obtendo as "importâncias dos atributos" de ambos.

**Etapa 07. Modelagem de aprendizado de máquina:**  Alguns modelos de aprendizado de máquina foram treinados. O que apresentou melhores resultados após a validação cruzada passou por mais uma etapa de ajuste fino de hiper parâmetros para otimizar a generalização do modelo.

**Etapa 08. Ajuste fino de hiper parâmetros:** O melhor modelo foi elencado para ser otimizado ajustando seus parâmetros.

**Etapa 09. Converta o desempenho do modelo em valores de negócios:** O desempenho dos modelos foi convertido em valores de negócios.

**Etapa 10. Implantar o Modelo em Produção:** O modelo foi implantado em um ambiente de nuvem para possibilitar que os stakeholders interessados acessem seus resultados.

# 4. Os 3 principais insights de dados

**Hipótese 01:** Interesse em contratar seguro aumenta quando a pessoa possui veiculo que já sofreu dano anteriormente.

**Verdadeira**

**Hipótese 02:** Interesse em contratar seguro aumenta enquanto a idade de uso do veículo aumenta.

**Verdadeira**

**Hipótese 03:** Interesse em contratar seguro aumenta quando a idade aumenta.

**Verdadeira**

# 5. Modelo de aprendizado de máquina aplicado

Os seguintes modelos de aprendizado de máquina foram treinados:

Extra Trees
Random Forest
Logistic Regressor
XGBoost
KNN

Todos eles passaram por cross-validation para apurar seus resultados.

# 6. Desempenho do Modelo de Aprendizado de Máquina

Os modelos "Random Forest Classifier" e "XGBoost Classifier" apresentaram melhor desempenho de generalização que os demais modelos, mas devido a problemas de armazenamento, optou-se pelo "XGBoost Classifier". Os gráficos mais adequados que mostram o desempenho do modelo neste problema de classificação são a curva de ganho cumulativo, a curva Lift. Essas duas curvas são exibidas abaixo.

![metrics_perfomance](https://user-images.githubusercontent.com/97288194/181206943-9697fbf8-fb62-4d91-a7c9-822c6f88732c.png)

O modelo treinado (validado cruzado e ajustado) também foi aplicado em um conjunto de dados de clientes em potencial que não participaram da pesquisa inicial. Portanto, este último conjunto de dados não contém uma variável "resposta". Nesse caso, calcula-se a probabilidade de que cada cliente em potencial adquira o seguro do veículo, o conjunto de dados é classificado de acordo com a probabilidade e a equipe de vendas recebe o conjunto de dados classificado para oferecer o seguro do veículo para os indivíduos mais propensos cadastrados no conjunto.

# 7. Resultados de Negócios

* Ao ligar para 20.000 clientes classificados com nosso modelo, a quantidade de clientes interessados ​​alcançados seria mais de 3 vezes o que uma lista aleatória alcançaria;

* Ao aumentar o número de ligações para 40.000 clientes, a quantidade de clientes interessados ​​alcançados seria mais de 2,5 vezes o que uma lista aleatória alcançaria;

* Para atingir a meta de contatar 80% dos clientes interessados ​​em mais de 127.000 pessoas, bastaria um pouco mais de 39.000 ligações.

# 8. Conclusões

A identificação dos potenciais clientes mais propensos a adquirir o seguro de veículo novo é um problema de classificação, um tipo particular de problema de classificação. Como tal, requer métricas específicas para avaliar o desempenho do modelo. Mas o mais importante, do ponto de vista do negócio, é que o modelo fornece insights sobre as características mais relevantes que caracterizam um cliente em potencial, permitindo que a equipe de vendas da empresa foque seus atendimentos, reduzindo assim o custo da empresa.

# 9. Lições aprendidas

A analise exploratória de dados é uma ferramenta poderosa tão quanto aos algoritmos de aprendizado de máquina, com ela foi possível gerar conhecimento do problema, levantando e validando hipóteses que contradizem o problema inicial. Essas informações são valiosas para o entendimento do negócio e para o planejamento de ações futuras. Esta etapa também fornece uma visualização do resultado da etapa de seleção de recursos.

Existem métricas específicas mais adequadas a esse tipo de problema do que algumas métricas usuais usadas em problemas de classificação.

A escolha do modelo de aprendizado de máquina utilizado deve considerar a generalização do modelo, mas também o custo de sua implantação.


# 10. Próximos passos para melhorar

Lidar com os dados desbalanceados através de técnicas de Balanceamento

# LICENÇA

# Todos os direitos reservados - Comunidade DS 2022
