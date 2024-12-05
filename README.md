#include <stdio.h>
#include <string.h>
#define IVA 0.15
int main() {
    float inventario[5][2]; // Cantidad y Precio de hasta 5 productos
    char nombresProductos[5][100]; // Nombres de los productos
    int opcion, indiceEditar, indiceEliminar;
    int totalProductos = 2; // Número inicial de productos en el inventario

    // Llenar el inventario inicial
    printf("\nLlenado inicial del inventario:\n");
    for (int i = 0; i < totalProductos; i++) {
        printf("\nIntroduce el nombre del producto %d: ", i + 1);
        fgets(nombresProductos[i], sizeof(nombresProductos[i]), stdin);
        nombresProductos[i][strcspn(nombresProductos[i], "\n")] = '\0'; // Quitar el salto de línea

        printf("Ingrese la Cantidad: ");
        scanf("%f", &inventario[i][0]);
        printf("Ingrese el Precio: ");
        scanf("%f", &inventario[i][1]);
        inventario[i][1]+= (inventario[i][1]*IVA);

        getchar();
    }

    // Mostrar el inventario
    printf("\nInventario actual:\n");
    for (int i = 0; i < totalProductos; i++) {
        printf("%d. Nombre: %s - Cantidad: %.2f - Precio agregado IVA: %.2f\n", i, nombresProductos[i], inventario[i][0], inventario[i][1]);
    }
    
    SN:
    // Menú de opciones
    printf("\nSeleccione una opción: 1) Editar / 2) Eliminar / 3) Salir: ");
    scanf("%d", &opcion);
    getchar(); // Limpiar el buffer

    switch (opcion) {
        case 1: // Editar producto
            printf("\nSeleccione el índice del producto que desea editar (0 a %d): ", totalProductos - 1);
            scanf("%d", &indiceEditar);
            getchar(); // Limpiar el buffer

            if (indiceEditar >= 0 && indiceEditar < totalProductos) {
                printf("\nIntroduce el nuevo nombre del producto: ");
                fgets(nombresProductos[indiceEditar], sizeof(nombresProductos[indiceEditar]), stdin);
                nombresProductos[indiceEditar][strcspn(nombresProductos[indiceEditar], "\n")] = '\0';

                printf("Ingrese la nueva Cantidad: ");
                scanf("%f", &inventario[indiceEditar][0]);
                printf("Ingrese el nuevo Precio: ");
                scanf("%f", &inventario[indiceEditar][1]);
                inventario[indiceEditar][1]+= (inventario[indiceEditar][1]*IVA);
                getchar(); // Limpiar el buffer

                printf("\nProducto actualizado correctamente.\n");
            } else {
                printf("\nÍndice inválido.\n");
            }
            break;

        case 2: // Eliminar producto
            printf("\nSeleccione el índice del producto que desea eliminar (0 a %d): ", totalProductos - 1);
            scanf("%d", &indiceEliminar);

            if (indiceEliminar >= 0 && indiceEliminar < totalProductos) {
                for (int i = indiceEliminar; i < totalProductos - 1; i++) {
                    strcpy(nombresProductos[i], nombresProductos[i + 1]);
                    inventario[i][0] = inventario[i + 1][0];
                    inventario[i][1] = inventario[i + 1][1];
                }
                totalProductos--; // Reducir el número de productos
                printf("\nProducto eliminado correctamente.\n");
            } else {
                printf("\nÍndice inválido.\n");
            }
            break;

        case 3: // Salir
            printf("\nSaliendo del programa...\n");
            break;

        default:
            printf("\nOpción no válida.\n");
            break;
    }

    // Mostrar el inventario actualizado
    printf("\nInventario actualizado:\n");
    for (int i = 0; i < totalProductos; i++) {
        printf("%d. Nombre: %s - Cantidad: %.2f - Precio agragado IVA: %.2f\n", i, nombresProductos[i], inventario[i][0], inventario[i][1]);
    }

    if(opcion !=3){
        goto SN;
    }

    return 0;
}
