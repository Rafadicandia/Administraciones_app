# Administraciones_app
Repo de la app para gestionar los vencimientos de la inmo
¡Excelente pregunta\! La respuesta es: **sí, absolutamente.**

El esquema que hemos construido está diseñado precisamente para que puedas agregar más tipos de vencimientos en el futuro de una manera muy sencilla. Tu intuición es correcta: **la forma de hacerlo es creando nuevas hojas en tu Google Sheet.**

### ¿Cómo Funciona la "Magia"?

La clave de la aplicación está en el objeto `SHEETS` que definimos al principio de tu archivo `Code.gs`.

```javascript
const SHEETS = {
  PROPERTIES: 'Propiedades',
  CONTRATO: 'Vencimiento_Contrato',
  REAJUSTE: 'Vencimiento_Reajuste',
  TRIBUTOS: 'Vencimiento_Tributos',
  SANEAMIENTO: 'Vencimiento_Saneamiento',
  ADICIONAL_MERCANTIL: 'Vencimiento_Adicional_Mercantil'
};
```

Casi todas las funciones de la aplicación (como `filterVencimientos` o `getPropertyAndVencimientos`) no tienen los nombres de las hojas escritos directamente, sino que **leen este objeto y recorren cada una de las hojas que están listadas aquí**.

Esto hace que el sistema sea increíblemente flexible.

### Guía Paso a Paso para Agregar un Nuevo Vencimiento (Ej: "Seguro")

Imaginemos que quieres empezar a controlar el vencimiento de los seguros de las propiedades. Solo tendrías que seguir estos 3 pasos:

1.  **Crear la Nueva Hoja en Google Sheets:**

      * En tu archivo de Google Sheets, crea una nueva pestaña. Llámala, por ejemplo, `Vencimiento_Seguro`.
      * Añade las columnas que necesites. Lo **único obligatorio** es que tengas una columna llamada `Padrón` para poder vincularla a la propiedad, y al menos una columna de fecha (ej: `Fecha_Vencimiento_Poliza`). Puedes añadir otras como `Nro_Poliza`, `Compania`, `Monto_Asegurado`, etc.

2.  **Actualizar el Backend (`Code.gs`):**

      * Abre tu `Code.gs`.
      * Simplemente añade una nueva línea al objeto `SHEETS`, dándole un nombre clave (en mayúsculas) y apuntando al nombre de la nueva hoja que creaste.

    <!-- end list -->

    ```javascript
    const SHEETS = {
      PROPERTIES: 'Propiedades',
      CONTRATO: 'Vencimiento_Contrato',
      REAJUSTE: 'Vencimiento_Reajuste',
      TRIBUTOS: 'Vencimiento_Tributos',
      SANEAMIENTO: 'Vencimiento_Saneamiento',
      ADICIONAL_MERCANTIL: 'Vencimiento_Adicional_Mercantil',
      // --- TU NUEVA LÍNEA ---
      SEGURO: 'Vencimiento_Seguro' 
    };
    ```

3.  **Re-implementar la API:**

      * Como has hecho un cambio en el código del backend, necesitas volver a publicarlo. Ve a `Implementar` \> `Gestionar implementaciones`, edita tu implementación actual y crea una `Nueva versión`.

**¡Y eso es todo\!** No necesitas tocar ni una sola línea del archivo `index.html`.

### ¿Qué Pasará Automáticamente?

Al hacer estos cambios, la aplicación se adaptará sola:

  * El **filtro de vencimientos** ahora incluirá los nuevos `Seguros` en sus búsquedas.
  * Cuando busques una propiedad, la tabla de **"Vencimientos Asociados"** mostrará los seguros junto con los demás tipos.
  * Si haces clic en "Editar" en un vencimiento de tipo seguro, el **modal se construirá dinámicamente** con los campos que hayas definido en tu nueva hoja (Nro\_Poliza, Compania, etc.).

Has elegido una arquitectura muy robusta y escalable. Puedes seguir añadiendo todos los tipos de vencimiento que necesites sin miedo a romper nada.