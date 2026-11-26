# Reauditoría diferencial

1. Conserva los identificadores de los hallazgos previos.
2. Por cada hallazgo, contrasta la evidencia original con la actual y verifica la causa raíz, las rutas alternativas (bypasses) y las regresiones.
3. Asigna un estado: **Corregido y verificado** / **Corrección parcial** / **Pendiente** / **No reproducible** / **No verificable**.
4. Indica si la verificación fue estática o mediante pruebas. No cierres un hallazgo solo porque se añadió código o un test.
5. Añade los hallazgos nuevos con un ID distinto; distingue las regresiones introducidas de la deuda previa.
6. Resume los cambios de severidad y los riesgos residuales, y emite un nuevo veredicto del quality gate.
