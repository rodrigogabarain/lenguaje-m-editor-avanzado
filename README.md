# Práctica: Lenguaje M y Editor Avanzado en Power Query

## Respuestas Teóricas

- **¿Qué hace exactamente el bloque let...in en lenguaje M? ¿Por qué cada paso puede referenciar al anterior?**
  El bloque `let...in` define una secuencia de pasos con nombre donde `let` declara y asigna variables de transformación de datos, y `in` determina cuál es el resultado final que se devolverá. Cada paso puede referenciar al paso anterior porque M evalúa las expresiones de manera procedural-funcional, permitiendo encadenar transformaciones sucesivas sobre la tabla de trabajo.

- **¿Por qué M es Case Sensitive y qué consecuencia práctica tiene? Dá un ejemplo de un error que esto puede causar.**
  El lenguaje M distingue estrictamente entre mayúsculas y minúsculas (*Case Sensitive*). Prácticamente, esto significa que escribir mal una función nativa (como `table.transformcolumns` en lugar de `Table.TransformColumns`) romperá la ejecución arrojando un error de sintaxis porque el motor no reconocerá la función.

- **¿Cuál es la diferencia entre usar Text.Trim y Text.Clean en M?**
  `Text.Trim` remueve caracteres de espacio en blanco (espacios comunes) situados al inicio y al final de una cadena de texto. En cambio, `Text.Clean` está diseñado para eliminar caracteres no imprimibles o de control (como saltos de línea o tabulaciones incrustadas dentro del texto).

- **¿Por qué filtraste los registros "PRUEBA" después de estandarizar la categoría y no antes?**
  Porque el dataset original contenía variaciones tipográficas en las categorías (como "PRUEBA" en mayúsculas). Si se filtraba antes de estandarizar, los registros con variaciones en minúsculas podrían haber quedado excluidos o el filtro exacto no los habría detectado correctamente debido a la sensibilidad a mayúsculas. Al aplicar primero `Text.Proper` (o estandarización), todos los registros de prueba adoptan un formato homogéneo (`Prueba`), permitiendo un filtrado robusto y seguro.
