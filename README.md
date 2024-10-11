# PowerBIDesafio
Desafio da DIO sobre PowerBI

Projeto: Modelo Star Schema e Visualizações no Power BI
Descrição do Projeto

Este projeto tem como objetivo criar um modelo de dados no formato Star Schema utilizando uma única tabela de dados financeiros. A partir desse modelo, foram criadas visualizações e tabelas dinâmicas que facilitam a análise de vendas, lucros, descontos e unidades vendidas por produto, país e período de tempo.
Etapas do Projeto

    Importação dos Dados:
        Os dados foram importados a partir de uma tabela de exemplo chamada "Financial Sample", disponível no formato .xlsx.
        A partir dessa tabela, foram criadas tabelas de fato e dimensões para construir o modelo no formato estrela.

    Criação das Tabelas Dimensão e Fato:
        Financials_origem: Um backup oculto da tabela original.
        D_Produtos: Inclui detalhes de produto e cálculos agregados, como a média e mediana das vendas.
        D_Produtos_Detalhes: Contém informações detalhadas sobre produtos, faixa de desconto, preço de venda e unidades vendidas.
        D_Descontos: Relaciona o produto com as informações de desconto.
        D_Detalhes: Fornece detalhes adicionais, como segmento de mercado e país.
        D_Calendário: Criada utilizando a função DAX CALENDAR() para incluir datas de início e fim das vendas.
        F_Vendas: Tabela de fato que registra as transações de vendas, incluindo informações como unidades vendidas, preço de venda, lucro, entre outros.

Diagrama do Modelo Star Schema

O diagrama de relacionamento foi construído no formato estrela com uma tabela de fato (F_Vendas) no centro, e as seguintes tabelas de dimensão:

    D_Produtos: Relacionada a F_Vendas pelo campo ID_Produto.
    D_Produtos_Detalhes: Relacionada a D_Produtos pelo campo ID_Produto.
    D_Descontos: Relacionada a F_Vendas e D_Produtos para cruzar informações de desconto.
    D_Calendário: Relacionada à F_Vendas pelo campo Date.

Funções DAX Utilizadas
1. Função CALENDAR()

    Criada para gerar uma tabela de datas que cobre o período total das vendas. A fórmula utilizada foi:

    DAX

    Calendário = CALENDAR(MIN(F_Vendas[Date]), MAX(F_Vendas[Date]))

    Esta função gera automaticamente uma lista de todas as datas entre a primeira e última data registrada na tabela F_Vendas, permitindo o uso dessa tabela para análises temporais.

2. Médias e Mediana (MEAN() e MEDIAN())

    Utilizada na criação da tabela D_Produtos para calcular a média e mediana do valor de vendas e das unidades vendidas, com a seguinte fórmula agregada:

    DAX

    Media_Valor_Vendas = AVERAGE(F_Vendas[Sales])
    Mediana_Valor_Vendas = MEDIAN(F_Vendas[Sales])

3. Agregações em Tabelas Dimensão

    Para calcular o valor máximo e mínimo de vendas por produto, foram utilizadas funções DAX como MAX() e MIN():

    DAX

    Valor_Max_Venda = MAX(F_Vendas[Sales])
    Valor_Min_Venda = MIN(F_Vendas[Sales])

Funcionalidades Implementadas

    Gráficos e Tabelas Dinâmicas:
        Gráficos de barras, pizza e linhas, além de tabelas dinâmicas que mostram detalhes de vendas, unidades vendidas, lucro, e descontos, organizados por produto, país e segmento.

    Modelo Star Schema:
        O modelo foi configurado com as tabelas dimensões interligadas pela tabela fato, permitindo análises rápidas e eficientes.

    Visualizações Detalhadas:
        Através de gráficos e tabelas, foi possível analisar o desempenho de vendas por períodos, produtos, e aplicar filtros dinâmicos.

Conclusão

Este projeto foi fundamental para mostrar como um modelo de dados no formato estrela pode melhorar a eficiência e clareza na análise de dados financeiros. Utilizamos funções DAX poderosas para criar medidas e cálculos agregados, além de visualizações que facilitam a tomada de decisões com base em dados.
