# Simula preço das ações, um banco e um cliente fazendo aplicação

Neste projeto você vai construir pelo 3 módulos: 

* Um simulador de Bolsa de Valores, que vai simular o valor de 10 ações;
* Um simulador de um banco, onde está a conta corrente do cliente;
* Um simulador de um cliente, que define uma estratégia de aplicação, gera alguns cenários simulados e escolhe 5 ações para realizar uma aplicação com o dinheiro que tem na sua conta corrente.

## Simulador da Bolsa de Valores

Deverão ser utilizadas 10 ações da B3, para as quais você deverá baixar os preços históricos para um perído de 1 ano.

Você utilizará um simulador baseado na _Geometric Brownian Motion_; você poderá se basear na implementação dada neste [repositório](https://github.com/mariomack/stochastic-asset-pricing-in-continuous-time).

O simulador ao ser iniciado proverá duas APIs:

* `GetStockPrice/<TICKER>` -- retorna o preço atual da ação indicada por `TICKER`
* `GetStockFuturePrice/<TICKER>/<NDaysAhead>` -- retorna o preço da ação `TICKER` `NDaysAhead` (**N** dias à frente, no máximo 180 dias)

## Simulador do Banco

Você deverá implementar uma aplicação que simula um banco com uma conta corrente onde o cliente poderá efetuar as seguintes operações:

* Abre Conta -- `AbreConta/<USUARIO>/<VALORINICIAL>`, onde `USUARIO` é um identificador do usuário, nome simples, sem caracteres especiais; `VALORINICIAL` é o depósito inicial feito para abrir a conta.
    * Retorna o Número da Conta que será um _hash_ e deverá ser utilizado em todas as transações posteriores.
* Saque -- `Saque/<CONTA>/<VALOR>`
* Depósito -- `Deposito/<CONTA>/<VALOR>`
* Saldo  -- `Saldo/<CONTA>`, retorna o saldo da conta.

## Cliente

Você deverá implementar um cliente que terá as seguintes características:

O cliente vai construir uma estratégia de aplicação em 5 ações; para isso ele deverá obter o valor atual destas 5 ações e deverá rodar o seu próprio simulador para **N** dias.

Com os cenários construídos, ele irá definir por uma estratégia, isto é, das 10 ações que foram simuladas, quais darão o maior lucro com base nas simulações realizadas.

Definida a estratégia, o cliente deverá sacar o valor correspondente na sua conta corrente para a compra das ações.

Depois disso, o cliente deverá pegar no Simulador da Bolsa o valor das ações após **N** dias, isto é, vai chamar a API `GetStockFuturePrice`.

O cliente então verifica o resultado de sua aplicação, fazendo a diferença entre a cotação real **N** dias à frente (obtida da Bolsa) e o valor inicial da ação; depois de calcular o resultado, o cliente vai depositar ou sacar esse valor de sua conta corrente.

# Implementação

O **Simulador da Bolsa** e o **Simulador do Banco** deverão rodar em _containers_ separados, expondo as URLs (APIs) especificadas. O **Cliente** poderá rodar diretamente no console, sem necessidade de interação com o usuário; roda, grava o resultado e sai.

Você deverá gravar todos os eventos em um arquivo de log que deverá ser utilizado para gerar o relatório da execução. Itens no log: preços iniciais das ações, ações escolhidas na estratégia, preços finais das ações escolhidas, resultado da estratégia (lucro ou prejuízo), e outros itens relevantes.

# Entregas

* Todo o código (**em Python com Flask**)
* Relatório do trabalho em PDF, contendo:
    * Descrição da implementação, decisões, estratégias de implementação, como executar o projeto.
    * Relatório da execução, com prints das telas, detalhes do log, etc.
    * Relatório de participação de cada componente do grupo, individualizando o que cada um fez no projeto.

**Poderá ser realizado em grupos de até 4 componentes**


