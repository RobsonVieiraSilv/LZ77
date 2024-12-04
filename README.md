# Código Lempel-Ziv 77 (LZ77)
Neste repositório, apresenta-se uma implementação básica do algoritmo LZ77 para apresentação na disciplina "Teoria da Informação", no PPGEE/UFPE.

## Breve explicação
O algoritmo LZ77 foi desenvolvido em 1977 por Abraham Lempel e Jacob Ziv, o qual é amplamente utilizado para compressão de dados. O algoritmo descrito no artigo de 1977 codifica uma sequência encontrando a correspondência mais longa em qualquer posição dentro de uma janela de símbolos passados. Ele representa a sequência por meio de um ponteiro para a localização da correspondência dentro da janela e pelo comprimento dessa correspondência (Cover e Thomas, 2006). Esse ponteiro é um par dado por (P,L), em que P é a posição, o início da correspondência, e L é o comprimento da correspondência. Ou, podemos representa por (F, P, L), em que F é a flag que assume valores 1 ou 0 se houver correspondência ou não, respectivamente. Chamaremos essa representação de tupla.

Por exemplo, considere \( W = 4 \), o comprimento da janela, e a string `ABBABBABBBAABABA`. Podemos separar a string da seguinte forma:  
`A | B | B | ABBABB | BA | A | BA | BA`.  

Analisando os dois primeiros caracteres separados, percebemos que eles não possuem correspondências anteriores, sendo, portanto, representados pelas tuplas `(0, A)` e `(0, B)`, respectivamente.  

Os caracteres subsequentes são representados pelas seguintes tuplas:  
- `(1, 1, 1)`  
- `(1, 3, 6)`  
- `(1, 4, 2)`  
- `(1, 1, 1)`  
- `(1, 3, 2)`  
- `(1, 2, 2)`  

Dessa forma, a string é representada pela sequência de tuplas:  
`(0, A), (0, B), (1, 1, 1), (1, 3, 6), (1, 4, 2), (1, 1, 1), (1, 3, 2), (1, 2, 2)`.  

Um detalhe importante é a quarta tupla, `(1, 3, 6)`, que possui comprimento 6. Isso ocorre porque o correspondente começa na terceira posição da string com comprimento 3 (`ABB`). Essa sequência (`ABB`) se repete mais uma vez, totalizando um comprimento de 6.  

A partir da sequência de tuplas, é possível recuperar, ou reconstruir, a string/texto original. Esse processo corresponde à descompressão. Durante a descompressão, as informações de posição e comprimento fornecidas pelas tuplas referem-se à string que está sendo progressivamente reconstruída.
Por exemplo, suponha que a string reconstruída até o momento seja `BAB`. Se a próxima tupla for `(1, 2, 2)`, isso significa:
- A posição 2 indica que a correspondência começa 2 posições antes do final da string reconstruída, ou seja, no caractere `A`;
- O comprimento 2 indica que dois caracteres devem ser copiados a partir dessa posição, resultando em `AB`;
- `AB` é adicionado ao final de `BAB`, resultando em `BABAB`. 

Dessa forma, ao processar a tupla `(1, 2, 2)`, a string em reconstrução passa de `BAB` para `BABAB`. Esse processo continua até que todas as tuplas tenham sido processadas, resultando na recuperação completa da string original.

Agora, podemos recuperar a string a partir das tuplas `(0, A), (0, B), (1, 1, 1), (1, 3, 6), (1, 4, 2), (1, 1, 1), (1, 3, 2), (1, 2, 2)`:
               | **Tupla**       | **Ação**                                                             | **String Construída**  |
|--------------|-----------------|----------------------------------------------------------------------|------------------------|
| 1            | `(0, A)`        | Adicione `A` diretamente.                                            | `A`                    |
| 2            | `(0, B)`        | Adicione `B` diretamente.                                            | `AB`                   |
| 3            | `(1, 1, 1)`     | Copie o caractere de posição e comprimento 1, ou seja, `B`.          | `ABB`                  |
| 4            | `(1, 3, 6)`     | Copie 3 caracteres começando na posição 3, ou seja, `ABB`, e repita. | `ABBABBABB`            |
| 5            | `(1, 4, 2)`     | Copie 2 caracteres começando na posição 4, ou seja, `BA`.            | `ABBABBABBBA`          |
| 6            | `(1, 1, 1)`     | Copie o caractere de posição e comprimento 1, ou seja, `A`.          | `ABBABBABBBAA`         |
| 7            | `(1, 3, 2)`     | Copie 2 caracteres começando na posição 3, ou seja, `BA`.            | `ABBABBABBBAABA`       |
| 8            | `(1, 2, 2)`     | Copie 2 caracteres começando na posição 2, ou seja, `BA`.            | `ABBABBABBBAABABA`     |

Portanto, a string foi recuperada com sucesso.

## Implementação do LZ77 em Python

O algoritmo LZ77 foi implementado em Python, utilizando o ambiente Colab (Jupyter Notebook). A implementação está organizada em duas partes principais:

1. **Compressão e descompressão básicas**:  
   - A função `LZ77_compress` comprime uma string ou texto recebido, gerando uma sequência de tuplas.  
   - A função `LZ77_decompress`, por sua vez, recebe essa sequência de tuplas e a utiliza para descomprimir, recuperando a string ou texto original.  
   - Esta parte corresponde diretamente à descrição conceitual do funcionamento do LZ77 apresentada anteriormente.  

2. **Codificação e decodificação binária**:  
   - A função `LZ77_encoder` recebe uma string, gerando como saída uma sequência de tuplas e uma string codificada, que consiste em uma sequência binária.  
   - A função `LZ77_decoder` realiza o processo inverso: a partir da string codificada, ela recupera tanto a sequência de tuplas quanto a string original.  

Além disso, apresentamos alguns exemplos e resolvemos dois exercícios do livro *"Information Theory, Inference, and Learning Algorithms"* de David MacKay.

## Referências
1. MacKay, David JC. Information theory, inference and learning algorithms. Cambridge university press, 2002.
2. Thomas, M. T. C. A. J., and A. Thomas Joy. Elements of information theory. Wiley-Interscience, 2006.
