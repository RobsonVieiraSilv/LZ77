# Código Lempel-Ziv 77 (LZ77)
Neste repositório, apresenta-se uma implementação básica do algoritmo LZ77 para apresentação na disciplina "Teoria da Informação", no PPGEE/UFPE.

## Breve explicação sobre o funcionamento do código
O algoritmo LZ77 foi desenvolvido em 1977 por Abraham Lempel e Jacob Ziv, o qual é amplamente utilizado para compressão de dados. O algoritmo descrito no artigo de 1977 codifica uma sequência encontrando a correspondência mais longa em qualquer posição dentro de uma janela de símbolos passados. Ele representa a sequência por meio de um ponteiro para a localização da correspondência dentro da janela e pelo comprimento dessa correspondência (Cover e Thomas, 2006). Esse ponteiro é um par dado por (P,L), em que P é a posição, o início da correspondência, e L é o comprimento da correspondência.

Por exemplo, seja W = 4, o comprimento do janelamento, e a string seja ABBABBABBBAABABA. Podemos separar a string da seguinte forma: A | B | B | ABBABB | BA | A | BA | BA. Se houver correspondência assumimeros que a flag = 1, caso contrário será zero. Observando os dois primeiros caracteres que separamos, notaremos que eles não possuem correspondentes, portanto, são representado por (0, A) e (0,B), respectivamente. Os demais são representados da seguinte forma: (0,A), (0,B), (1,1), (3,6), (4,2), (1,1), (3,2), (2,2). 
