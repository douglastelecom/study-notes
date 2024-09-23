<div align='justify'>

## Probabilidade

>[Link](https://)
>
>22 Setembro de 2024

#### FORMULA BINOMIAL

Quanto eventos são independentes, a maioria dos problemas probabilísticos podem ser formulados na fórmula binomial.

A fórmula da probabilidade binomial é a seguinte:

\[ P(X = k) = \binom{n}{k} p^k (1-p)^{n-k} \]

Onde:
- \( P(X = k) \) é a probabilidade de obter exatamente \( k \) sucessos em \( n \) tentativas.
- \( \binom{n}{k} \) é o coeficiente binomial, que se calcula como \( \frac{n!}{k!(n-k)!} \).
- \( p \) é a probabilidade de sucesso em uma única tentativa.
- \( 1-p \) é a probabilidade de fracasso.
- \( n \) é o número total de tentativas.
- \( k \) é o número de sucessos desejados.

A fórmula abaixo mostra a chance de fazer um flush no Poker (ter cinco cartas de mesmo naipe, considerando que sempre a chance 1/4 para fins didáticos) :

\[ \frac{7!}{5!(2!)}(0.25^5*0.75^2)\]

\( \frac{7!}{5!(2!)}\) é o tanto de combinações possíveis com as cartas de sucesso e fracasso, considerando que as cartas de sucesso são um elemetno indistinguível das outras cartas de sucesso, e as cartas de fracasso como elementos indistinguíveis das outras cartas de fracasso. 
Por exemplo, é como se nas 7! (5040) combinações apenas 21 delas seriam realmente diferentes, enquanto o restante das 5019 combinações seriam apenas alguma combinação repetida dentre as 21.

As 21 combinações possíveis entre sucesso e fracasso seriam:

SSSSSFF
SSSSFSF
SSSSFFS
SSSSFSS
SSSFSFS
SSSFFSS
SSFSSSF
SSFSSFS
SSFSFSS
SSFFSSS
SFSSSSF
SFSSSFS
SFSSFSS
SFSFSSS
SFFSSSS
FSSSSSF
FSSSSFS
FSSSFSS
FSSFSSS
FSFSSSS
FFSSSSS

</div>