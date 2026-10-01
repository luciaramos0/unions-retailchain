¿Cuántas filas devuelve cada consulta y por qué son distintas? Explicá con ejemplos concretos de los datos qué filas se eliminaron con UNION.
UNION (Consulta 1): 11 filas
UNION ALL (Consulta 2): 14 filas
Norte tiene 7 productos y Sur tiene 7, o sea 14 filas en total. UNION ALL las junta todas sin revisar nada. UNION elimina las filas completamente idénticas, y eso pasa con tres productos que existen en ambas sucursales.
Cada uno aparece dos veces (Norte y Sur) y UNION deja solo una copia, por eso 14 − 3 = 11.
La Webcam HD 1080p tiene id 107 en Norte y 111 en Sur. Como el id es distinto, las filas no son idénticas y UNION no las elimina, aunque sea el mismo producto.

¿Por qué UNION ALL es más eficiente que UNION? ¿Qué operación adicional realiza UNION internamente que consume más recursos?
UNION ALL solo concatena los resultados de ambas consultas, sin ningún procesamiento extra. UNION hace lo mismo y además elimina duplicados, y para eso tiene que comparar todas las filas entre sí.

¿En qué casos de negocio usarías cada uno? Dá al menos dos ejemplos reales distintos a los del ejercicio.
UNION (cuando necesitás valores únicos):
Campaña de email: juntar los correos de los suscriptores al newsletter y los de los clientes que compraron. Si alguien está en ambas listas, debe recibir el mensaje una sola vez.
Lista de ciudades con presencia: unir las ciudades donde hay clientes y las ciudades donde hay proveedores, sin repetir.

UNION ALL (cuando cada fila cuenta o sabés que no hay duplicados):
Ventas anuales: la empresa guarda una tabla por mes o por año (ventas_2025, ventas_2026). Para calcular el total hay que conservar todas las filas, porque dos ventas del mismo producto y monto son operaciones distintas y no deben eliminarse.
Logs de varios servidores: consolidar registros de actividad de distintos servidores para auditar. Cada evento es válido aunque se repita, y eliminar filas falsearía el conteo.

¿Qué pasa si las columnas de ambas consultas no coinciden en número o tipo? ¿Qué error genera SQL?
SQL Server da error y no ejecuta la consulta.
