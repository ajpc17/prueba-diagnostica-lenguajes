Prueba Diagnóstica — Lenguajes y Compiladores
Universidad Nacional Experimental de Guayana (UNEG)
Vicerrectorado Académico — Coordinación de Ingeniería en Informática
Curso: Lenguajes y Compiladores
Profesor: Msc. Félix Márquez — fmarquez@e.uneg.edu.ve
Período: 2026-I
Autor: Arnaldo Perdomo CI:30.791.551

📦 prueba-diagnostica-lenguajes/
│
├── 📁 Problema 1/
│   ├── problema1.c            # Solución en C con memoria dinámica (malloc/free)
│   ├── problema1.exe          # Ejecutable compilado de la solución en C
│   ├── problema1.py           # Solución en Python con listas dinámicas
│   └── resultado_n100.txt     # Tiempos de ejecución para n=100 en ambos lenguajes
│
├── 📁 Problema 2/
│   └── problema2.py           # Validador de notación FEN en Python
│
├── 📁 Problema 3/
│   ├── problema3.py           # Traductor de palabras reservadas de C en Python
│   ├── programa_prueba.c      # Archivo de prueba usado como entrada del traductor
│   └── traduccion_resultado.txt  # Resultado de la traducción al español
│
├── 📁 Defensa/
│   └── link_defensa.txt       # Enlace al video de defensa en YouTube
│
└── README.md                  # Este archivo

Problema 1 — Triángulo de Pascal y Evaluación de (x+1)ⁿ
¿Qué hace?
Dado un número entero no negativo n:

Parte a) Genera los coeficientes del polinomio (x+1)ⁿ usando el
Triángulo de Pascal con memoria dinámica, y muestra el polinomio resultante.
Parte b) Evalúa f(x) = (x+1)ⁿ paso a paso para un valor de x dado,
usando los coeficientes generados.
Mide el tiempo de ejecución para n=100 en C y Python, y guarda los
resultados en resultado_n100.txt.

¿Cómo funciona el Triángulo de Pascal?
n=0:     1
n=1:    1 1
n=2:   1 2 1
n=3:  1 3 3 1          →  (x+1)³ = x³ + 3x² + 3x + 1
n=4: 1 4 6 4 1         →  (x+1)⁴ = x⁴ + 4x³ + 6x² + 4x + 1
Cada número es la suma de los dos que tiene arriba. Esos números son
exactamente los coeficientes del polinomio.
Memoria dinámica
LenguajeImplementaciónPythonListas dinámicas [0] * (i+1) que crecen en cada iteraciónCmalloc() por cada fila del triángulo + free() al terminar
Ejemplo de salida
Ingrese n: 5
Coeficientes: [1, 5, 10, 10, 5, 1]
f(x) = (x+1)^5 = x^5 + 5x^4 + 10x^3 + 10x^2 + 5x + 1

Ingrese x: 3
  Término 1: 1 × 3^5 = 243
  Término 2: 5 × 3^4 = 405
  Término 3: 10 × 3^3 = 270
  Término 4: 10 × 3^2 = 90
  Término 5: 5 × 3^1 = 15
  Término 6: 1 × 3^0 = 1
  f(3) = 1024 ✓
Comparación de tiempos para n=100
LenguajeTiempo de ejecuciónC~0.038 msPython~0.261 msDiferenciaC es ~7x más rápido
Los resultados completos están en resultado_n100.txt.
Cómo compilar y ejecutar
bash# Python
python problema1.py

# C — compilar
gcc -o problema1 problema1.c -lm

# C — ejecutar (Windows)
problema1.exe

# C — ejecutar (Linux/Mac)
./problema1

Problema 2 — Validador de Notación FEN
¿Qué hace?
Recibe una cadena de texto y valida si está en notación
FEN (Forsyth-Edwards Notation), el estándar internacional para
representar posiciones del tablero de ajedrez en una sola línea.
Estructura de una cadena FEN
rnbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1
└────────────────────────────────────────────┘ │ └──┘ │ │ └─ Número de jugada
              Tablero (8 filas)                 │  │   │ └─── Medio movimientos
                                              Turno │   └───── En passant
                                                 Enroque
Las 5 validaciones del programa
#ParteRegla validada1Tablero8 filas separadas por /, cada fila suma 8 casillas, solo letras rnbqkpRNBQKP y números 1-8, exactamente 1 rey de cada color2TurnoSolo w (blancas) o b (negras)3EnroqueSolo letras K Q k q, sin repetir, en ese orden4En passant- o casilla válida (fila 3 turno blanco / fila 6 turno negro)5ContadoresMedio movimientos ≥ 0, número de jugada ≥ 1
Ejemplo de salida
Validando: 'rnbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1'

  ✓ 1. Tablero    : Tablero valido
  ✓ 2. Turno      : Turno valido
  ✓ 3. Enroque    : Enroque valido
  ✓ 4. En passant : Sin en passant
  ✓ 5. Contadores : Contadores validos

  RESULTADO: ✓ Cadena FEN VÁLIDA
FEN válidos para probar
# Posición inicial
rnbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1

# Después de 1.e4
rnbqkbnr/pppppppp/8/8/4P3/8/PPPP1PPP/RNBQKBNR b KQkq e6 0 1
Cómo ejecutar
bash# Python
python problema2.py

# Opción 1: ingresar cadena FEN manualmente
# Opción 2: ejecutar casos de prueba automáticos

⚠️ Importante: La cadena FEN debe ingresarse completa con sus
6 partes separadas por espacio.


Problema 3 — Traductor de Palabras Reservadas de C al Español
¿Qué hace?
Carga un archivo .c en memoria dinámica, detecta todas las palabras
reservadas del lenguaje C y las traduce a su equivalente en español,
reproduciendo la etapa de análisis léxico de un compilador real.
Los 4 pasos del programa
[PASO 1]  Cargar archivo .c en memoria dinámica
          → Se mide el tamaño exacto y se reserva con malloc()

[PASO 2]  Crear diccionario de 32 palabras reservadas en memoria dinámica
          → Cada palabra y traducción tiene su propio espacio en memoria

[PASO 3]  Tokenizar el código caracter a caracter
          → Extraer cada palabra y buscarla en el diccionario

[PASO 4]  Generar código traducido
          → Reemplazar reservadas y guardar resultado en .txt
Tabla de traducción de palabras reservadas
CEspañolCEspañolCEspañolintenteroifsiwhilemientrascharcaracterelsesinoforparafloatflotantereturnretornarswitchsegundoubledoblebreakrompercasecasovoidvaciocontinuecontinuardohacerstructestructuratypedefdefinir_tipoconstconstantestaticestaticosizeoftamano_deenumenumeracionexternexternounsignedsin_signosignedcon_signolonglargoshortcortoautoautomaticoregisterregistrovolatilevolatilgotoir_aunionunion_cdefaultdefecto
Ejemplo de traducción
c/* ORIGINAL en C */          /* TRADUCIDO al Español */
int factorial(int n) {   →   entero factorial(entero n) {
    if (n <= 0) {        →       si (n <= 0) {
        return 1;        →           retornar 1;
    }                    →   }
    for (i=1; i<=n; i++) →   para (i=1; i<=n; i++)
    while (i < n) {      →   mientras (i < n) {
    switch (dia) {       →   segun (dia) {
    case 1: break;       →   caso 1: romper;
El archivo programa_prueba.c es el archivo de entrada de ejemplo
y traduccion_resultado.txt contiene el resultado completo.
Cómo ejecutar
bash# Python
python problema3.py

# Opción 1: analizar un archivo .c existente (ej: programa_prueba.c)
# Opción 2: crear archivo de prueba y analizarlo automáticamente

Requisitos del sistema
Python

Python 3.6 o superior
No requiere librerías externas

bashpython --version    # Verificar instalación
python problema1.py # Ejecutar
C

Compilador GCC

bash# Verificar instalación
gcc --version

# Instalar en Ubuntu/Debian
sudo apt install gcc

# Compilar cualquier programa
gcc -o programa programa.c -lm

Defensa
🎥 Video explicativo en YouTube: Ver Defensa/link_defensa.txt
Requisitos del video según el enunciado:

✅ Duración máxima: 20 minutos
✅ Formato horizontal (no shorts)
✅ El estudiante aparece visible y con audio durante todo el video
✅ Explicación argumentada del código fuente
✅ Demostración práctica en vivo de cada programa