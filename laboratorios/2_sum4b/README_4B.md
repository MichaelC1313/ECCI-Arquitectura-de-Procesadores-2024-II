Aquí tienes un archivo `.md` que explica el funcionamiento del código Verilog proporcionado, el cual extiende el módulo `sum1b` a un sumador de 4 bits.

---

# SUMADOR 4 BITS

Para este modulo implementaremos el anteriormente realizado (SUMADOR 1 BIT), llamando a traves de la instancia 

## Descripción del Módulo

```verilog
`include "sum1b.v"

module sum4b (
    input  [3:0] A,
    input  [3:0] B,
    output       Cout,
    output [3:0] Sum
);

wire c1, c2, c3;
wire c_out;

sum1b s0 (.A(A[0]), .B(B[0]), .Ci(1'b0),  .Cout(c1), .Sum(Sum[0]));
sum1b s1 (.A(A[1]), .B(B[1]), .Ci(c1),    .Cout(c2), .Sum(Sum[1]));
sum1b s2 (.A(A[2]), .B(B[2]), .Ci(c2),    .Cout(c3), .Sum(Sum[2]));
sum1b s3 (.A(A[3]), .B(B[3]), .Ci(c3),    .Cout(Cout), .Sum(Sum[3]));

endmodule
```

### Entradas y Salidas

- **Entradas:**
  - `A[3:0]`: Un vector de 4 bits que representa el primer operando.
  - `B[3:0]`: Un vector de 4 bits que representa el segundo operando.

- **Salidas:**
  - `Sum[3:0]`: El resultado de la suma de los dos operandos de 4 bits.
  - `Cout`: Bit de acarreo de salida (carry-out), que indica si hay un acarreo hacia un bit más significativo, si existiera.

### Funcionamiento del Módulo

El módulo `sum4b` es un sumador de 4 bits que se construye utilizando cuatro instancias del sumador de 1 bit (`sum1b`), conectadas en serie para propagar el acarreo entre cada bit.

1. **Instanciación de Sumadores de 1 Bit (`sum1b`):**
   - `s0`: Suma los bits menos significativos (`A[0]` y `B[0]`) sin acarreo de entrada (`Ci = 0`). Produce la suma `Sum[0]` y un acarreo `c1`.
   - `s1`: Suma los segundos bits (`A[1]` y `B[1]`) junto con el acarreo `c1` producido por la primera suma. Produce la suma `Sum[1]` y un acarreo `c2`.
   - `s2`: Suma los terceros bits (`A[2]` y `B[2]`) junto con el acarreo `c2` producido por la segunda suma. Produce la suma `Sum[2]` y un acarreo `c3`.
   - `s3`: Suma los bits más significativos (`A[3]` y `B[3]`) junto con el acarreo `c3` producido por la tercera suma. Produce la suma `Sum[3]` y el acarreo final `Cout`.

### Cómo funciona?

  - El acarreo se propaga de un bit a otro, desde el bit menos significativo hasta el más significativo.
  - Esto permite que el módulo `sum4b` maneje correctamente la adición de números de 4 bits, produciendo tanto la suma de los bits como el acarreo final.


