# Laboratorio 1 – Compuertas lógicas en SystemC

Proyecto realizado en Windows 11 usando WSL (Ubuntu 24.04) con SystemC 2.3.3.  
Se implementaron las compuertas OR, XOR, NAND, NOR y XNOR en archivos separados y un testbench en `main.cpp` que prueba las 4 combinaciones (00, 01, 10, 11).

## Compilación

```bash
g++ main.cpp -I /home/andresmedina/lab2-systemc/systemc-2.3.3/include -L /home/andresmedina/lab2-systemc/systemc-2.3.3/lib-linux64 -lsystemc -lm -o logic_gates
export LD_LIBRARY_PATH=/home/andresmedina/lab2-systemc/systemc-2.3.3/lib-linux64:$LD_LIBRARY_PATH
./logic_gates
