let    
    // Paso 1: Origen de datos inicial
    Origen = Table.FromRows(
        {
            {1, " Laptop Pro 15 ", "Computación", 1200.00, #date(2024, 1, 5)},
            {2, "Mouse Inalámbrico", "accesorios", 28.00, #date(2024, 1, 8)},
            {3, " Teclado Mecánico", "PRUEBA", 95.00, #date(2024, 1, 12)},
            {4, "Monitor 4K ", "computación", 450.00, #date(2024, 2, 3)},
            {5, " Auriculares BT", "Audio", 120.00, #date(2024, 2, 10)},
            {6, "SSD Externo 1TB ", "PRUEBA", 130.00, #date(2024, 3, 5)},
            {7, "Webcam HD", "Accesorios", 85.00, #date(2024, 3, 12)}
        }, 
        {"id_venta", "nombre_producto", "categoria", "precio", "fecha_venta"}
    ),

    // Paso 2: Eliminar espacios en blanco al inicio y al final
    // de la columna nombre_producto usando Text.Trim
    LimpiarEspacios = Table.TransformColumns(Origen, {{"nombre_producto", Text.Trim, type text}}),

    // Paso 3: Estandarizar la columna categoria a Title Case
    // para unificar "computación", "COMPUTACIÓN" y "Computación"
    EstandarizarCategoria = Table.TransformColumns(LimpiarEspacios, {{"categoria", Text.Proper, type text}}),

    // Paso 4: Filtrar y eliminar registros de prueba
    // Excluir filas donde categoria sea exactamente "Prueba"
    // usando Table.SelectRows
    EliminarPruebas = Table.SelectRows(EstandarizarCategoria, each ([categoria] <> "Prueba")),

    // Paso 5: Definir tipos de datos correctos
    // id_venta: Int64.Type
    // nombre_producto y categoria: type text
    // precio: type number
    // fecha_venta: type date
    TiparColumnas = Table.TransformColumnTypes(EliminarPruebas, {
        {"id_venta", Int64.Type},
        {"nombre_producto", type text},
        {"categoria", type text},
        {"precio", type number},
        {"fecha_venta", type date}
    })

in
    TiparColumnas
