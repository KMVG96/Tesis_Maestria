# Análisis de Correlación entre NFI, CCI y GEDI
## Explicación Simplificada del Proceso

---

## ¿Qué hicimos?

Imagina que tienes tres formas diferentes de medir cuántos árboles y cuánta biomasa (peso de los árboles) hay en un bosque:

1. **NFI (Inventario Forestal Nacional)**: Personas que van al bosque y miden los árboles directamente
2. **CCI (Climate Change Initiative)**: Satélites que toman fotos desde el espacio para estimar la biomasa
3. **GEDI**: Un láser espacial que mide la altura de los árboles desde la Estación Espacial Internacional

Lo que queríamos saber es: **¿Qué tan bien se relacionan estas tres formas de medir?**

---

## Diagrama de Flujo del Proceso

```
┌─────────────────────────────────────────────────────────────────┐
│                    INICIO DEL ANÁLISIS                          │
└─────────────────┬───────────────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────────────────┐
│  PASO 1: Cargar las librerías necesarias                       │
│  • ggplot2 (para hacer gráficas bonitas)                       │
└─────────────────┬───────────────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────────────────┐
│  PASO 2: Leer los datos del archivo CSV                        │
│  • Archivo: NFI_CCI_GEDIheights_2.csv                          │
│  • Contiene: coordenadas, biomasa NFI, biomasa CCI,            │
│              altura GEDI                                        │
└─────────────────┬───────────────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────────────────┐
│  PASO 3: Transformar los datos                                 │
│  • Aplicar logaritmo a los datos de NFI                        │
│  • ¿Por qué? Porque algunos valores son muy grandes y otros    │
│    muy pequeños. El logaritmo los "aplana" para verlos mejor   │
└─────────────────┬───────────────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────────────────┐
│  PASO 4: Calcular las correlaciones (valor R)                  │
│  • R entre NFI y CCI                                           │
│  • R entre NFI y GEDI                                          │
│  • R entre log(NFI) y CCI                                      │
│  • R entre log(NFI) y GEDI                                     │
│                                                                 │
│  ¿Qué es R? Un número entre -1 y 1 que indica:                │
│  • R cercano a 1: Muy buena relación positiva                  │
│  • R cercano a 0: No hay relación                              │
│  • R cercano a -1: Relación negativa                           │
└─────────────────┬───────────────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────────────────┐
│  PASO 5: Crear las gráficas de calor                           │
│                                                                 │
│  GRÁFICA 1: NFI vs CCI                                         │
│  • Eje X: Biomasa según NFI                                    │
│  • Eje Y: Biomasa según CCI                                    │
│  • Colores: Muestran cuántos puntos hay en cada zona           │
│  • Etiqueta: Valor de R                                        │
│                                                                 │
│  GRÁFICA 2: NFI vs GEDI                                        │
│  • Eje X: Biomasa según NFI                                    │
│  • Eje Y: Altura según GEDI                                    │
│  • Colores: Diferentes (inferno)                               │
│  • Etiqueta: Valor de R                                        │
│                                                                 │
│  GRÁFICA 3: log(NFI) vs CCI                                    │
│  • Eje X: Logaritmo de biomasa NFI                             │
│  • Eje Y: Biomasa según CCI                                    │
│  • Colores: Diferentes (magma)                                 │
│  • Etiqueta: Valor de R                                        │
│                                                                 │
│  GRÁFICA 4: log(NFI) vs GEDI                                   │
│  • Eje X: Logaritmo de biomasa NFI                             │
│  • Eje Y: Altura según GEDI                                    │
│  • Colores: Diferentes (viridis)                               │
│  • Etiqueta: Valor de R                                        │
└─────────────────┬───────────────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────────────────┐
│                    FIN DEL ANÁLISIS                             │
│  Resultado: 4 gráficas que muestran cómo se relacionan         │
│  las diferentes formas de medir la biomasa forestal            │
└─────────────────────────────────────────────────────────────────┘
```

---

## Mapa Conceptual

```
                    ┌──────────────────────┐
                    │  DATOS FORESTALES    │
                    │   (de México)        │
                    └──────────┬───────────┘
                               │
                ┌──────────────┼──────────────┐
                │              │              │
                ▼              ▼              ▼
         ┌──────────┐   ┌──────────┐   ┌──────────┐
         │   NFI    │   │   CCI    │   │   GEDI   │
         │ (Terreno)│   │(Satélite)│   │  (Láser) │
         └────┬─────┘   └────┬─────┘   └────┬─────┘
              │              │              │
              │    ┌─────────┴─────────┐    │
              │    │                   │    │
              ▼    ▼                   ▼    ▼
         ┌────────────────┐       ┌────────────────┐
         │ COMPARACIÓN 1  │       │ COMPARACIÓN 2  │
         │  NFI vs CCI    │       │  NFI vs GEDI   │
         │  (Biomasa)     │       │ (Biomasa-Alt.) │
         └────────┬───────┘       └────────┬───────┘
                  │                        │
                  └────────┬───────────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │  TRANSFORMACIÓN │
                  │   LOGARÍTMICA   │
                  │   (Normalizar)  │
                  └────────┬────────┘
                           │
                ┌──────────┼──────────┐
                │                     │
                ▼                     ▼
         ┌──────────────┐      ┌──────────────┐
         │ COMPARACIÓN 3│      │ COMPARACIÓN 4│
         │log(NFI)-CCI  │      │log(NFI)-GEDI │
         └──────┬───────┘      └──────┬───────┘
                │                     │
                └──────────┬──────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │ CORRELACIONES   │
                  │ (Valor R)       │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │  4 GRÁFICAS DE  │
                  │  MAPAS DE CALOR │
                  └─────────────────┘
```

---

## Explicación Detallada para Preparatoria

### ¿Qué problema estamos resolviendo?

Cuando los científicos quieren saber cuánta biomasa (cantidad de árboles y plantas) hay en los bosques de México, pueden usar diferentes métodos. El problema es que cada método puede dar resultados diferentes. Por eso, queremos saber: **¿Se parecen los resultados de estos tres métodos?**

### Los tres métodos:

#### 1. **NFI (Inventario Forestal Nacional)** - Medición en campo

**¿Cómo funciona?**
- Personas capacitadas van físicamente al bosque
- Delimitan parcelas cuadradas o circulares (por ejemplo, de 400 m²)
- Miden cada árbol dentro de la parcela

**¿Qué miden en cada árbol?**
1. **DAP (Diámetro a la Altura del Pecho)**: Miden el grosor del tronco a 1.30 metros del suelo usando una cinta métrica especial
2. **Altura del árbol**: Usan instrumentos como clinómetros o hipsómetros
3. **Especie del árbol**: Identifican qué tipo de árbol es (pino, encino, etc.)

**¿Cómo calculan la biomasa?**

Aquí viene la parte científica. No pueden pesar los árboles directamente (¡imagina intentar poner un árbol en una báscula!), entonces usan **ecuaciones alométricas**.

**Ecuación alométrica básica:**
```
Biomasa (kg) = a × (DAP)^b × (Altura)^c
```

Donde:
- **a, b, c** = números que cambian según la especie del árbol
- **DAP** = diámetro del tronco en centímetros
- **Altura** = altura del árbol en metros

**Ejemplo práctico:**
Imagina un pino con:
- DAP = 30 cm
- Altura = 15 metros
- Usando la ecuación para pinos: Biomasa = 0.0509 × (30)^2.13 × (15)^0.95
- Resultado ≈ 450 kg de biomasa por árbol

Luego suman la biomasa de **todos los árboles** en la parcela y la convierten a **toneladas por hectárea** (Mg/ha).

**¿De dónde vienen estas ecuaciones?**
Científicos cortaron y pesaron cientos de árboles de diferentes especies, midieron su diámetro y altura, y encontraron patrones matemáticos que relacionan estas medidas con el peso real.

**Ventajas:**
- ✅ Muy preciso
- ✅ Mide directamente en el terreno
- ✅ Puede identificar especies

**Desventajas:**
- ❌ Muy caro (necesitas equipos en el campo)
- ❌ Toma mucho tiempo
- ❌ Solo puedes medir algunas parcelas, no todo el país

---

#### 2. **CCI (Climate Change Initiative)** - Estimación por satélite

**¿Cómo funciona?**
- Satélites toman imágenes desde el espacio
- Analizan la "firma espectral" de la vegetación
- Los sensores captan diferentes tipos de luz (visible, infrarroja, etc.)

**¿Cómo estiman la biomasa?**
1. **Índices de vegetación**: Calculan índices como NDVI (Normalized Difference Vegetation Index)
   - Plantas sanas reflejan mucha luz infrarroja
   - Plantas con menos biomasa reflejan menos

2. **Modelos estadísticos**: Relacionan estos índices con mediciones de NFI en el terreno
   - Entrenan algoritmos con datos conocidos de NFI
   - Luego aplican el modelo a todo el territorio

**Ventajas:**
- ✅ Cubre grandes extensiones (todo México)
- ✅ Más económico
- ✅ Se puede repetir frecuentemente

**Desventajas:**
- ❌ Menos preciso que NFI
- ❌ Las nubes pueden bloquear las imágenes
- ❌ Necesita calibración con datos de campo

---

#### 3. **GEDI (Global Ecosystem Dynamics Investigation)** - Láser espacial

**¿Cómo funciona?**
- Instalado en la Estación Espacial Internacional
- Dispara pulsos láser hacia la Tierra (como un radar, pero con luz)
- El láser rebota en las hojas, ramas y suelo
- Mide el tiempo que tarda en regresar cada rebote

**¿Cómo estiman la biomasa?**
1. **Perfil vertical**: Crea un perfil 3D de la vegetación
   ```
   Tiempo = 0.000001 s → Copa del árbol (20 m de altura)
   Tiempo = 0.000002 s → Ramas medias (10 m de altura)
   Tiempo = 0.000003 s → Suelo (0 m)
   ```

2. **Métricas de altura**: Calcula:
   - RH98 = Altura al 98% de la energía retornada
   - RH50 = Altura media del dosel
   - Densidad del dosel

3. **Modelos de regresión**: Relaciona estas alturas con biomasa
   - Árboles más altos generalmente tienen más biomasa
   - Doseles más densos tienen más biomasa

**Ventajas:**
- ✅ Mide estructura 3D de los bosques
- ✅ No le afectan las nubes (el láser las atraviesa)
- ✅ Precisión vertical de centímetros

**Desventajas:**
- ❌ Solo mide "huellas" pequeñas (no cobertura total)
- ❌ No pasa por todos los lugares
- ❌ Estima biomasa indirectamente a través de altura

### ¿Qué hicimos paso a paso?

#### Paso 1: Preparar las herramientas
Cargamos una librería llamada `ggplot2` que nos permite hacer gráficas muy bonitas y profesionales.

#### Paso 2: Cargar los datos
Leímos un archivo CSV (como una hoja de Excel) que tiene:
- La ubicación de cada parcela forestal (coordenadas X, Y)
- La biomasa medida por NFI (en toneladas por hectárea)
- La biomasa estimada por CCI (en toneladas por hectárea)
- La altura medida por GEDI (en metros)

#### Paso 3: Transformar los datos
Aplicamos una transformación logarítmica. ¿Por qué?

Imagina que tienes estas mediciones: 10, 100, 1000, 10000
- La diferencia entre 10 y 100 es de 90
- La diferencia entre 1000 y 10000 es de 9000

¡Es muy difícil graficar esto! Pero si usamos logaritmo:
- log(10) = 1
- log(100) = 2
- log(1000) = 3
- log(10000) = 4

Ahora las diferencias son iguales (de 1 en 1) y podemos ver mejor los patrones.

#### Paso 4: Calcular la correlación (R)
La correlación es un número que nos dice qué tan relacionadas están dos cosas:

- **R = 1**: Relación perfecta positiva
  - Si NFI sube, CCI también sube exactamente igual

- **R = 0**: No hay relación
  - Lo que hace NFI no afecta a CCI para nada

- **R = -1**: Relación perfecta negativa
  - Si NFI sube, CCI baja

Por ejemplo, si R = 0.85 entre NFI y CCI, significa que cuando el NFI dice que hay mucha biomasa, generalmente CCI también dice que hay mucha biomasa.

#### Paso 5: Hacer las gráficas
Creamos 4 gráficas de "mapas de calor" (heat maps):

**¿Qué es un mapa de calor?**
Imagina un tablero de ajedrez donde cada cuadrito tiene un color:
- **Colores oscuros/fríos**: Pocos datos en esa zona
- **Colores brillantes/calientes**: Muchos datos en esa zona

En nuestras gráficas:
- El **eje X** muestra un método de medición (ej: NFI)
- El **eje Y** muestra otro método (ej: CCI)
- Los **colores** muestran cuántas parcelas tienen esos valores
- La **etiqueta R** nos dice qué tan relacionados están

### ¿Por qué hicimos 4 gráficas y no solo 1?

1. **Gráfica 1 (NFI vs CCI)**: ¿Se parecen las mediciones terrestres con las satelitales?
2. **Gráfica 2 (NFI vs GEDI)**: ¿La biomasa medida en tierra coincide con las alturas del láser?
3. **Gráfica 3 (log(NFI) vs CCI)**: Igual que la 1, pero con datos "aplanados" para ver mejor
4. **Gráfica 4 (log(NFI) vs GEDI)**: Igual que la 2, pero con datos "aplanados" para ver mejor

### Optimizaciones del código

Para que el código sea más eficiente y profesional:

1. **Calculamos todas las correlaciones al inicio**: En vez de calcular R justo antes de cada gráfica, las calculamos todas juntas al principio.

2. **Creamos un tema común**: En vez de escribir el mismo código de diseño 4 veces, lo escribimos una sola vez y lo reutilizamos.

3. **Organizamos por secciones**: Todo está ordenado con comentarios claros que explican qué hace cada parte.

4. **Eliminamos variables innecesarias**: No creamos copias de los datos si no son necesarias.

---

## Resultados esperados

Al final, deberías ver 4 gráficas donde:
- Si los puntos forman una **línea diagonal**, significa que los dos métodos están muy relacionados
- Si los puntos están **dispersos por todos lados**, significa que los métodos no se relacionan bien
- El **valor R** te confirma numéricamente qué tan fuerte es la relación

### Interpretación del valor R:

| Rango de R | Interpretación |
|------------|----------------|
| 0.00 - 0.19 | Muy débil correlación |
| 0.20 - 0.39 | Débil correlación |
| 0.40 - 0.59 | Moderada correlación |
| 0.60 - 0.79 | Fuerte correlación |
| 0.80 - 1.00 | Muy fuerte correlación |

---

## Conclusión

Este análisis nos ayuda a entender si los diferentes métodos de medir biomasa forestal están dando resultados similares. Si la correlación es alta, podemos confiar más en usar datos satelitales (que son más rápidos y baratos) en lugar de siempre tener que ir al bosque a medir (que es caro y tarda mucho).

¡Es como comparar diferentes termómetros para ver si todos marcan la misma temperatura!

---

**Fecha de creación**: 2026-03-22
**Archivo relacionado**: GMB_malla_modif_3modelos - copia.Rmd
**Datos utilizados**: NFI_CCI_GEDIheights_2.csv
