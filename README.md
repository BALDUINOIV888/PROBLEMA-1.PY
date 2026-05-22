# =========================================================
# FASE 5 - EVALUACION FINAL POA UNAD
# Problema 4: Reposicion de inventario
# Estudiante: Erick Stiven Sanchez Acosta
# =========================================================

INVENTARIO = [
    {"producto": "Camisa Casual", "stock": 12, "ventas_prom": 5},
    {"producto": "Pantalon Denim", "stock": 4, "ventas_prom": 8},
    {"producto": "Chaqueta Lona", "stock": 8, "ventas_prom": 3}
]

STOCK_MINIMO_SEGURIDAD = 10


def calcular_pedido(stock_actual):
    if stock_actual < STOCK_MINIMO_SEGURIDAD:
        return STOCK_MINIMO_SEGURIDAD - stock_actual
    return 0


def clasificar_prioridad(stock_actual):
    if stock_actual < 5:
        return "Alta"
    elif stock_actual < 10:
        return "Media"
    return "Baja"


def mostrar_reporte():
    print("\n--- REPORTE AUTOMATICO DE INVENTARIO ---")
    for item in INVENTARIO:
        nombre = item["producto"]
        stock = item["stock"]
        pedido = calcular_pedido(stock)
        prioridad = clasificar_prioridad(stock)

        print(f"Producto: {nombre}")
        print(f"Stock actual: {stock}")
        print(f"Prioridad: {prioridad}")
        print(f"Cantidad a pedir: {pedido}")
        print("-" * 40)


def consulta_manual():
    while True:
        nombre_prod = input("\nIngrese el nombre del producto (o 'salir'): ").strip()

        if nombre_prod.lower() == "salir":
            break

        try:
            stock_usuario = int(input("Ingrese el stock actual: "))
            pedido = calcular_pedido(stock_usuario)
            prioridad = clasificar_prioridad(stock_usuario)

            if prioridad == "Alta":
                estado = "URGENTE"
            else:
                estado = "Estable"

            print("\n--- RESULTADO DE LA CONSULTA ---")
            print(f"Producto: {nombre_prod}")
            print(f"Estado: {estado}")
            print(f"Prioridad: {prioridad}")
            print(f"Cantidad a pedir: {pedido}")

        except ValueError:
            print("Error: debe ingresar un numero entero para el stock.")


if __name__ == "__main__":
    mostrar_reporte()
    consulta_manual()
    print("\nSistema finalizado.")
