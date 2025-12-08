# 📘 Powerwall DIY con Celdas 18650 – Investigación, Diseño y Criterios Técnicos

Este documento organiza la información recopilada sobre construcción de sistemas tipo *Powerwall* basados en celdas Li-ion 18650 recicladas. Se incluye análisis de metodologías utilizadas en proyectos domésticos, diferencias con sistemas comerciales como Tesla, consideraciones técnicas para pruebas de capacidad, selección de baterías y elementos de carga/seguridad.

---

## 1. Introducción

Los *powerwalls DIY* con celdas 18650 se han popularizado en Europa y Latinoamérica debido al bajo costo de las baterías recuperadas. La lógica habitual de construcción observada en múltiples proyectos:

- **Ahorro en baterías** mediante reciclado, pero **inversores y BMS de buena calidad**.
- Configuración común: **14 series (14s)** para obtener ~48 V nominal.
- Secciones construidas a partir de **grupos en paralelo** (individuales o conjuntos de 4), luego conectadas en serie para formar el banco total.

Objetivo personal del proyecto:  
**Comprender procesos de selección, prueba y ensamblado para construir un pack confiable de ~1000 Wh para respaldo nocturno.**

---

## 2. Evaluación y clasificación de celdas 18650 recicladas

La calidad de una batería reciclada depende de:

### 2.1 Pruebas de capacidad
Instrumentos reportados:

| Dispositivo / Método | Observaciones |
|---|---|
| **Opus BT-C3100/3000** | Método común, carga/descarga controlada, resultados estables. |
| **Modulos descargadores DIY** | Más económicos, pero variabilidad mayor entre mediciones. |
| **Cargadores/descargadores caseros resistivos** | Útiles para curva básica, menos precisión. |

Los valores medidos pueden variar entre equipos (ej. 1420 mAh vs 1550 mAh), atribuible a diferencias de calibración, resistencia interna, método de descarga y temperatura.

### 2.2 Medición de capacidad – Criterio físico
La capacidad **nominal en mAh no es energía**, la energía real es:

\[
E(\text{Wh}) = \int V(t) \cdot I(t)\, dt
\]

Los testers suelen integrar la descarga completa **sin corregir por tensión**, por lo que 2000 mAh descargados desde 4.2 V a 3.0 V no equivalen a 2000 mAh descargados a menor tensión media.

📌 Próxima tarea para completar este README:  
> Incorporar curvas \(V\text{-}Q\) típicas Li-ion y definir criterio estandar para normalizar mediciones.

---

## 3. Ensamblado y arquitectura del banco

### 3.1 Modelos DIY observados

- Grupos **paralelo primero → serial después**.
- Bloques verticales con múltiples celdas compartiendo barrido térmico.
- Espacios amplios entre celdas para ventilación.
- Conexiones por **soldadura punto / níquel strip**.

### 3.2 Diseño industrial – Caso Tesla Powerwall

Características estructurales reportadas:

- **Densidad muy alta** (celdas extremadamente próximas entre sí).
- Encapsulado **sellado en chasis metálico** → contención térmica y de gases.
- Fijación interna mediante **resina estructural / adhesivo térmico**.
- Interconexión tipo *bus-bar flexible* sin puntos visibles convencionales.

> ➤ Conclusión: Tesla prioriza **compacidad, rigidez mecánica y control térmico interno**, lo opuesto al enfoque DIY orientado a ventilación y modularidad.

---

## 4. Carga, seguridad y electrónica asociada

### 4.1 Carga unitaria

Cargador común para celdas individuales:

- **TP4056** (5 V input USB)
- Pines: **B+ / B-**
- Recomendación: usar versiones con **protección integrada (DW01 + MOSFET)**

### 4.2 Módulos y BMS

- BMS laptop → reciclaje **no recomendado por complejidad**.
- Para sistemas de gran capacidad: **BMS dedicado 14s, balanceo activo ideal**.
- Peligro crítico: conectar celdas con **voltajes diferentes** genera corrientes internas no deseadas y calor.

\[
P_{\text{pérdida}} = I^2 \cdot R_{\text{int}}
\]

---

## 5. Adquisición de baterías

Experiencia en Argentina:

- Precio histórico bajo (≈ 40 ARS por celda usada), actualmente más elevado por aumento de demanda.
- Mercado emergente de **celdas probadas y clasificadas**.
- Pendiente investigar importación China ↔ AR.
- Fuente útil: **secondlifestorage.com** → consulta por código/serie para fichas técnicas.

---

## 6. Requerimientos energéticos objetivo del proyecto

Consumo nocturno estimado:

| Equipo | Potencia aproximada | Tiempo uso | Energía |
|---|---|---|---|
| Heladera | ~200 W (50 % duty) | 8 h | ~800 Wh |
| TV | 80 W | 4 h | ~320 Wh |
| Stand-by hogar | 40 W | 8 h | ~320 Wh |

**Objetivo banco:**  
\[
\approx 1000\text{–}1500\,\text{Wh} \quad(\text{mínimo práctico para respaldo nocturno})
\]

---

## 7. Próximos pasos de desarrollo del proyecto

- Agregar curvas oficiales de descarga NCR/Samsung LG.
- Estandarizar protocolo de test:
  - \(I\) descarga (0.5 C recomendado para medición realista)
  - Corte a 3.0 V
  - Temperatura controlada
- Crear planillas CSV para registro de capacidad y resistencia interna.
- Diseñar layout físico + selección de BMS 14s.
- Evaluar costos del pack vs comprar LiFePO₄ directamente.

---

## 8. Licencia, contribuciones y contacto

- Documento en desarrollo, abierto a revisión y aporte técnico.
- **Pull Requests bienvenidos** para añadir papers, mediciones y curvas oficiales.

---

### 📥 Recursos opcionales futuros

1. Carpeta *docs/* con esquemas eléctricos y fórmulas.
2. Plantilla `.csv` para testeo masivo de celdas.
3. Versión extendida PDF/LaTeX con figuras.
4. Cálculo automático del número de celdas necesarias en función Wh/Cycle-Life.

