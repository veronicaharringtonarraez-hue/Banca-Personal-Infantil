# Especificación de Fusión — App Familiar (Hogar + Banco)

> Documento de diseño para combinar **Sistema-Hogar-Familiar** (base) con
> **Banca-Personal-Infantil / ChildBank** (módulo de banco). Se ejecuta en el
> repo `Sistema-Hogar-Familiar`. La sección de banca se reutiliza; lo que cambia
> se detalla en §7.

## 0. Filosofía
No se premia solo "completar la tarea", sino **calidad, esfuerzo, iniciativa y
responsabilidad**. Se separan dos preguntas:

- **¿Cómo se ganan los puntos?** → Módulo 1 (Tareas y Recompensas).
- **¿Qué hago con lo que gané?** → Módulo 2 (Banco Familiar).

## 1. Arquitectura: DOS indicadores (clave del diseño)
Cada acción ganada genera **dos cosas a la vez**:

1. **Mérito** (NO se gasta): mide responsabilidad/constancia/calidad. Es un
   acumulado **semanal** (puntos ganados en la semana + % de tareas asignadas
   completadas). **No baja cuando el niño gasta.** Sirve para **desbloquear
   privilegios** (p. ej. cuidar mascotas). Se reinicia/rola cada semana.
2. **Créditos del banco / Saldo** (SÍ se gasta): es la moneda. Sube con lo
   ganado y **baja al canjear** premios/experiencias/extras.

Conversión por defecto: **1 punto ganado = 1 crédito = +1 mérito** (ajustable).
Gastar créditos **no** afecta el mérito ni el historial de responsabilidad.

```
   Acción evaluada (Módulo 1)
        │  + puntos
        ├──────────────► MÉRITO (semanal, no se gasta) ─► Privilegios/Elegibilidad
        └──────────────► CRÉDITOS (saldo, Módulo 2)     ─► Canje de premios
```

## 2. Cuentas por integrante
- 👨 Maykol (papá) · 👩 Verónica (mamá) — adultos, también con cuenta.
- 👧 Taylor · 👦 Emmeth · 👦 Christopher — niños.
- 👶 Rachel — administrada por los padres (sin gasto propio).

Cada integrante acumula sus propios mérito y créditos.

## 3. Módulo 1 — Tareas y Recompensas (cómo se ganan)
### 3.1 Áreas con puntaje flexible
- Cada **área** de la casa tiene **puntaje base 10**, ajustable con **➕ / ➖**
  por el administrador (Verónica/Maykol). **Sin tope superior fijo**; mínimo
  configurable.
- Las **subtareas son un checklist de referencia** (guía de qué incluye una
  limpieza completa) y **no dan puntos individuales**.
- Escala orientativa: 8 mínimo aceptable · 10 correcto · 12 excelente ·
  15 profunda con iniciativa · 18–20 excepcional.

### 3.2 Autocuidado (hábitos)
- Cada hábito = **1 punto fijo** (cepillarse, bañarse, peinarse, desodorante,
  protector solar, rutina facial, vitaminas, meta de agua…), con ajuste ±
  opcional.

### 3.3 Cuidado de mascotas (también da puntos)
- Dar comida +1 · cambiar agua +1 · cepillar +1 · limpiar área de descanso +1 ·
  pasear +2 · jugar activamente +1.

### 3.4 Bonificaciones
- Todas las tareas del día +5 · toda la semana +20 · 30 días de higiene +30 ·
  cuarto impecable una semana +15 · iniciativa +3 · ayudar a otro +2.

### 3.5 Control de calidad (antes del puntaje final)
- **Orden:** ¿todo en su lugar?, superficies despejadas.
- **Limpieza:** sin polvo, piso limpio, sin manchas ni basura.
- **Presentación:** luce agradable, se nota el esfuerzo.
- Ejemplos de **➕** (rincones, mover muebles, telarañas, rodapiés, interruptores,
  reponer insumos, detectar daños…) y **➖** (polvo, basura, área olvidada,
  trabajo superficial, esconder desorden…).

### 3.6 Configuración editable por área
Nombre · responsable(s) · frecuencia (diaria/semanal/mensual…) · checklist ·
puntaje base (10) · mínimo · máximo (opcional/ilimitado) · observaciones.

### 3.7 Historial y transparencia (cada evaluación registra)
Puntaje base · ajustes ➕ con motivo · ajustes ➖ con motivo · puntaje final ·
comentarios · fecha · persona que evaluó.

## 4. Módulo 2 — Banco Familiar (qué hacer con los créditos)
- Ver **saldo** (créditos).
- **Historial** de ingresos y gastos.
- **Ahorro para metas** (ej.: "Nintendo Switch 5,000", "Libro 300").
- **Presupuestos** (editable por mes — ya existe en el banco).
- **Tienda / canje de recompensas** (ver §6).
- **Transferencias** entre cuentas, solo si los padres lo permiten.

## 5. Mérito y privilegios (elegibilidad)
- Las **mascotas NO tienen cuenta ni gastan puntos**. Hay un **Sistema de
  Elegibilidad para Cuidadores**.
- Requisito ejemplo para participar en actividades con la mascota:
  **≥ 50 puntos de mérito activos en la semana** y **≥ 80% de tareas asignadas**
  + buen historial.
- Desbloquea: dar comida, cambiar agua, cepillar, pasear, jugar, entrenar,
  elegir juguete para la mascota. (Registrar estos cuidados a su vez da puntos.)

## 6. En qué se gastan los créditos
### Siempre GRATIS (los padres lo cubren; nunca cuestan puntos)
Comida · agua · vivienda · ropa esencial · útiles escolares obligatorios ·
medicinas · atención médica · transporte escolar · higiene básica.
> Esto evita que el niño sienta que debe "comprar" necesidades fundamentales.

### Opcionales que SÍ pueden costar créditos
- **Entretenimiento:** elegir película/postre/restaurante/juego de mesa/actividad
  del finde.
- **Tecnología:** tiempo extra de pantalla/videojuegos, película especial.
- **Compras:** juguetes, libros, accesorios, decoración, materiales de hobby.
- **Experiencias:** helado, parque favorito, noche especial con mamá/papá.

(El catálogo y sus costos son configurables por el administrador.)

## 7. Conexión con el banco actual (qué se reutiliza y qué cambia)
**Se reutiliza intacto:** saldo, historial de movimientos, ahorro/metas,
presupuesto editable por mes, logros/insignias, Modo Mamá/Papá (dar/quitar,
bono, metas, PIN, respaldo), guardado automático.

**Cambia / se agrega:**
1. **Fuente de ingreso:** ahora viene de las evaluaciones del Módulo 1 (áreas,
   autocuidado, mascotas, bonos). Se **retira** la pantalla "Ganar" del banco
   (evita pago doble).
2. **Indicador de Mérito** nuevo (semanal, no se gasta) + pantalla de privilegios.
3. **Tienda de recompensas** (canje de créditos por lo opcional de §6).
4. **Gastos obligatorios:** las necesidades pasan a ser **gratis** (informativas),
   no se "pagan" con puntos. → Ver decisión pendiente D1.
5. **Cuentas:** la lista de cuentas se toma de la FAMILIA (incluye a Maykol y
   Verónica), no solo los 3 niños.
6. **PIN único** de adulto (181215) para todo.

**El puente (lo más delicado):** cuando un adulto **aprueba** una evaluación,
se acreditan los puntos finales como **créditos** y como **mérito**. Hay que
llevar un registro de "ya pagado" (por persona + ítem + fecha/semana) para que
el reinicio diario/semanal **no pague dos veces**.

## 8. Persistencia
- Hogar usa `localStorage` (`fam_tareas_v1`) + Firebase opcional.
- Banco usa `localStorage` (`bancoCrece.v1`).
- Se mantienen ambos almacenes, conectados por el puente. El **respaldo**
  (exportar/importar) debe incluir los dos. El banco arranca local (Firebase
  para el banco queda como fase futura — ver D3).

## 9. Fases de implementación (en el repo del Hogar)
1. Un solo `index.html` que cargue Hogar + el banco (el banco ya está
   namespaced en `window.BC`, casi no choca).
2. Unificar **familia** (una sola lista de integrantes) y **PIN** (181215).
3. Agregar tab **🏦 Banco** mostrando la banca (saldo/historial/ahorro/metas).
4. Indicador de **Mérito** + pantalla de **privilegios/elegibilidad de mascotas**.
5. **Puente** evaluación aprobada → créditos + mérito, con registro anti-doble-pago.
   Retirar "Ganar".
6. **Tienda de recompensas** y catálogo configurable. Necesidades gratis.
7. Respaldo que incluya ambos almacenes. Desplegar en Pages.

## 10. Decisiones pendientes
- **D1 — Gastos obligatorios vs. simulador educativo.** El banco actual tiene un
  "Pagar gastos" (alquiler, comida, diezmo…) con fin **educativo** (regla
  70/10/10/10). Tu nueva filosofía dice que las necesidades son **gratis**.
  ¿Qué prefieres?
  - (a) Reemplazar "Pagar gastos" por la **Tienda de recompensas** (necesidades
    gratis). *Más alineado con tu visión.*
  - (b) **Conservar** el simulador de presupuesto como "modo aprendizaje"
    opcional **y además** agregar la tienda.
- **D2 — Mérito.** ¿Confirmas que es **semanal** y que la elegibilidad de
  mascotas usa ≥50 mérito/semana y ≥80% de tareas? (valores ajustables)
- **D3 — Nube para el banco.** ¿El banco también sincroniza con Firebase como el
  Hogar, o arranca solo local? (recomendado: local primero)
- **D4 — Conversión.** ¿1 punto = 1 crédito = +1 mérito (recomendado), u otra?
