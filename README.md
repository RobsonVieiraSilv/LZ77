# Código Lempel-Ziv 77 (LZ77)
Neste repositório, apresenta-se uma implementação básica do algoritmo LZ77 para apresentação na disciplina "Teoria da Informação", no PPGEE/UFPE.

## Breve explicação
O algoritmo LZ77 foi desenvolvido em 1977 por Abraham Lempel e Jacob Ziv, o qual é amplamente utilizado para compressão de dados. O algoritmo descrito no artigo de 1977 codifica uma sequência encontrando a correspondência mais longa em qualquer posição dentro de uma janela de símbolos passados. Ele representa a sequência por meio de um ponteiro para a localização da correspondência dentro da janela e pelo comprimento dessa correspondência (Cover e Thomas, 2006). Esse ponteiro é um par dado por (P,L), em que P é a posição, o início da correspondência, e L é o comprimento da correspondência. Ou, podemos representa por (F, P, L), em que F é a flag que assume valores 1 ou 0 se houver correspondência ou não, respectivamente. Chamaremos essa representação de tupla.

Por exemplo, seja W = 4, o comprimento do janelamento, e a string seja ABBABBABBBAABABA. Podemos separar a string da seguinte forma: A | B | B | ABBABB | BA | A | BA | BA. Observando os dois primeiros caracteres que separamos, notaremos que eles não possuem correspondentes, portanto, são representados pelas tuplas (0, A) e (0,B), respectivamente. Os demais são representados pelas seguinte tuplas: (1,1,1), (1,3,6), (1,4,2), (1,1,1), (1,3,2), (1,2,2). Portanto, a string é representada pela sequência de tuplas (0, A), (0, B), (1,1,1), (1,3,6), (1,4,2), (1,1,1), (1,3,2), (1,2,2).   Note que a quarta tupla tem comprimento 6, isso porque o correspondente A inicia na terceira posição e tem comprimento 3, ou seja, ABB, mas essa sequência se repete mais uma vez, logo, o comprimento é 6. 

# Implementação do LZ77 em Python

O algoritmo LZ77 foi implementado em Python, utilizando o ambiente Colab (Jupyter Notebook). A implementação está organizada em duas partes principais:

1. **Compressão e descompressão básicas**:  
   - A função `LZ77_compress` comprime uma string ou texto recebido, gerando uma sequência de tuplas.  
   - A função `LZ77_decompress`, por sua vez, recebe essa sequência de tuplas e a utiliza para descomprimir, recuperando a string ou texto original.  
   - Esta parte corresponde diretamente à descrição conceitual do funcionamento do LZ77 apresentada anteriormente.  

2. **Codificação e decodificação binária**:  
   - A função `LZ77_encoder` recebe uma string, gerando como saída uma sequência de tuplas e uma string codificada, que consiste em uma sequência binária.  
   - A função `LZ77_decoder` realiza o processo inverso: a partir da string codificada, ela recupera tanto a sequência de tuplas quanto a string original.  

Além disso, apresentamos exemplos práticos e resolvemos dois exercícios do livro *"Information Theory, Inference, and Learning Algorithms"* de David MacKay.
