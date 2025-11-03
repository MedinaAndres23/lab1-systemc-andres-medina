# Laboratorio 1 – Compuertas lógicas en SystemC

Proyecto realizado en **Windows 11** usando **WSL (Ubuntu 24.04)** con **SystemC 2.3.3**.  
Se implementaron las compuertas **OR, XOR, NAND, NOR y XNOR** en archivos separados y un **testbench** en `main.cpp` que prueba las 4 combinaciones (00, 01, 10, 11).

---

## Estructura del proyecto

```text
lab2-systemc/
 ├── main.cpp
 ├── or_gate.cpp
 ├── xor_gate.cpp
 ├── nand_gate.cpp
 ├── nor_gate.cpp
 ├── xnor_gate.cpp
 └── README.md
```

Cada archivo `.cpp` define un `SC_MODULE` con sus puertos (`sc_in<bool>`, `sc_out<bool>`) y la operación lógica correspondiente.

---

## Compilación

Ejecutar dentro de la carpeta del proyecto (en WSL):

```bash
g++ main.cpp   -I /home/andresmedina/lab2-systemc/systemc-2.3.3/include   -L /home/andresmedina/lab2-systemc/systemc-2.3.3/lib-linux64   -lsystemc -lm -o logic_gates
```

> Nota: la guía usa `/usr/local/systemc`, pero en este caso SystemC se instaló en `/home/andresmedina/...`, por eso se usan esas rutas.

---

## Antes de ejecutar

Como la librería está en una ruta del usuario, hay que exportar el `LD_LIBRARY_PATH`:

```bash
export LD_LIBRARY_PATH=/home/andresmedina/lab2-systemc/systemc-2.3.3/lib-linux64:$LD_LIBRARY_PATH
```

(esto se puede poner en `~/.bashrc` para no escribirlo cada vez)

---

## Ejecución

```bash
./logic_gates
```

Salida esperada:

```text
A B | OR XOR NAND NOR XNOR
0 0 | 0   0    1    1    1
0 1 | 1   1    1    0    0
1 0 | 1   1    1    0    0
1 1 | 1   0    0    0    1
```

Con esto se comprueba que las 5 compuertas funcionan y que el testbench recorre las 4 combinaciones.

---

## Respuestas al cuestionario del laboratorio

**1. `sc_signal` vs `sc_in`/`sc_out`**  
- `sc_signal<T>`: es la **señal** que existe fuera de los módulos y por donde viaja el valor.  
- `sc_in<T>` / `sc_out<T>`: son **puertos** de un módulo; sirven para conectarse a una señal.  
En el testbench se crean las señales y luego se conectan a los puertos.  
**Frase clave:** la señal es el medio; los puertos son las interfaces.

**2. ¿Por qué `.read()` y `.write()`?**  
Porque SystemC controla el tiempo de simulación.  
- `.read()` obtiene el valor **estable** de la señal.  
- `.write(...)` publica un valor nuevo para que el kernel lo propague en el instante correcto.  
Así se evita que los módulos lean valores “a medio actualizar”.

**3. NAND → NOR (en cascada)**  
Encadenar compuertas no rompe nada: genera una **función booleana compuesta**.  
Si la NAND saca `X = !(A && B)` y esa salida entra en una NOR con otra entrada `C`, la salida es:  
`Y = !(X || C) = !( !(A && B) || C )`.  
La idea del laboratorio es que veas que puedes construir funciones más complejas a partir de las básicas.

**4. Ventaja de SystemC vs simulador visual**  
SystemC es textual, modular, se puede versionar (GitHub) y escala mejor para diseños grandes o jerárquicos.  
Los simuladores visuales (tipo Logisim) son muy buenos para aprender, pero no se integran tan bien en flujos reales de desarrollo.

---

## .gitignore recomendado

```text
logic_gates
*.swp
systemc-2.3.3
systemc-2.3.3.tar.gz
```

---

## Repositorio

Este proyecto forma parte de la entrega del laboratorio.

```text
https://github.com/MedinaAndres23/lab1-systemc-andres-medina
```
