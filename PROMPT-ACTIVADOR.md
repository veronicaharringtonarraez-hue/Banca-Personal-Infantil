# Prompt activador — Migrar la fusión al repo del Hogar

> Copia el bloque de abajo y pégalo en el chat de Claude Code que está abierto
> sobre el repositorio **Sistema-Hogar-Familiar**. Contiene todo lo acordado en
> el chat del banco.

---

```
Vamos a fusionar DOS apps de la familia en ESTE repo (Sistema-Hogar-Familiar),
que es la base. La otra app es el "Banco" (ChildBank), que vive en el repo
público veronicaharringtonarraez-hue/Banca-Personal-Infantil. El banco se
integra como un MÓDULO que administra los puntos; la sección de banca debe
quedar funcionalmente intacta.

ANTES DE CODIFICAR, lee el plan completo (documento público):
https://raw.githubusercontent.com/veronicaharringtonarraez-hue/Banca-Personal-Infantil/main/ESPECIFICACION-FUSION.md
El código del banco también es público en ese repo:
  index.html, app/data.js, app/store.jsx, app/components.jsx,
  app/screens.jsx, app/parent.jsx, app/app.jsx
(base raw: https://raw.githubusercontent.com/veronicaharringtonarraez-hue/Banca-Personal-Infantil/main/)

IDEA CENTRAL — separar GANAR de GASTAR con dos indicadores:
- MÉRITO (no se gasta): puntos de la semana + % de tareas. Reutiliza lo que ya
  existe en app.jsx (pointsFor sobre `done`, se reinicia con weekKey, no lo toca
  el gasto). Sirve para privilegios (elegibilidad de mascotas: >=50 mérito/semana
  y >=80% de tareas asignadas).
- CRÉDITOS (sí se gastan): saldo del banco (clave localStorage bancoCrece.v1).
- Conversión: 1 punto ganado = 1 crédito = +1 mérito (ajustable).

DECISIONES YA TOMADAS:
- D1: conservar el simulador educativo de presupuesto del banco (pagar
  alquiler/comida/diezmo, regla 70/10/10/10) como "modo aprendizaje" Y además
  agregar una Tienda de recompensas (canje de créditos por cosas opcionales).
  Las necesidades básicas son gratis.
- D2: mérito semanal; mascotas requieren >=50 y >=80% (ajustable).
- D3: el banco arranca LOCAL (localStorage). Firebase para el banco = fase futura.
- D4: conversión 1:1.

QUÉ QUEDA INTACTO (traer del banco): Pagar, Ahorro, Presupuesto editable por mes,
Registro, Logros y Modo Mamá/Papá (dar/quitar puntos, bono de exámenes, metas,
PIN, respaldo). Único cambio del lado banca: su ingreso ahora viene de las tareas
del Hogar aprobadas (se retira la pantalla "Ganar" del banco para no pagar doble).

PUNTOS DE ENGANCHE TÉCNICOS (ver §11 del documento):
- Estado del Hogar: clave fam_tareas_v1 = {profile,dist,tab,week,done,custom};
  done = {"pid:taskId":true}; reinicio semanal con weekKey().
- Puntos hoy planos: pointsFor = nº done × POINTS_PER_TASK (10). Calidad marks
  {s,o,c} vive en admin.jsx (Panel de Padres).
- PUENTE (idempotente): al APROBAR una tarea (cuando marks pasa a s:'ok' en
  admin.jsx, o con un botón "acreditar"), llamar Bank.creditForTask(pid, taskId,
  puntosFinales, weekKey()). Guardar en el store del banco un set
  paid["{week}:{pid}:{taskId}"]=true para NO pagar dos veces (la clave incluye la
  semana porque `done` se reinicia).
- Cuentas del banco = window.FAMILY (niños isKid: taylor/emmeth/christopher;
  adultos mama/papa con cuenta; rachel isBaby la administran los padres).
  Adaptar BC.CHILDREN para derivarse de FAMILY.
- PIN único: PARENT_PIN hoy es '0904' -> unificar a 181215 y que el banco use el
  mismo.
- Puntaje flexible (mejora nueva): base 10 por área ajustable con +/- sin tope,
  con motivos e historial; el número final aprobado va a créditos y mérito.
- CHOQUES a resolver: ambos archivos declaran App/Avatar/Confetti y const
  STORE_KEY ('fam_tareas_v1' vs 'bancoCrece.v1'). Namespingar el banco (IIFE o
  prefijos). NO montar dos ReactDOM.createRoot: renderizar el banco dentro de un
  tab. Agregar al BottomNav el item ['banco','🏦','Banco'].

CÓMO TRABAJAR:
1) Trabaja en una rama de desarrollo nueva (no en main directo). No rompas la app
   actual de tareas en ningún paso.
2) Implementa por FASES y muéstrame el avance al final de cada una:
   (1) montar banco + Hogar bajo un solo index.html, banco namespingado;
   (2) unificar FAMILY y PIN (181215);
   (3) tab "🏦 Banco" con la banca intacta (ver saldo/historial/ahorro/metas);
   (4) indicador de Mérito + pantalla de privilegios/elegibilidad de mascotas;
   (5) puente tareas aprobadas -> créditos + mérito, con anti-doble-pago; retirar
       "Ganar" del banco;
   (6) Tienda de recompensas + catálogo configurable; necesidades gratis;
   (7) respaldo que incluya ambos almacenes; publicar en Pages.
3) Si algo es ambiguo o implica un cambio grande/arquitectónico, PREGÚNTAME antes
   de hacerlo.

Empieza leyendo el documento y dame un plan corto de la Fase 1 antes de codificar.
```
