   ## Resumen de los Cambios
Grids Flexibles: Los filtros de fecha y la barra de búsqueda ahora se apilan verticalmente en pantallas pequeñas, en lugar de intentar caber en una sola fila.
Tablas Desplazables: Las tablas de datos (como la de "Vencimientos Próximos") ahora permiten el desplazamiento horizontal en móviles. Esto evita que la página se "rompa" y te permite ver toda la información de la tabla deslizando el dedo.
Formularios y Detalles Apilados: En los detalles de una propiedad y en los modales de edición, los campos y sus valores ahora se muestran uno debajo del otro en pantallas pequeñas, mejorando la legibilidad.
Ajustes Generales: He reducido un poco el padding y el tamaño de la fuente en móviles para aprovechar mejor el espacio.
A continuación te dejo el código con todas las modificaciones aplicadas
´´´
Código Modificado
    main.container { max-width: 1000px; }
    #loader { text-align: center; padding: 40px; }
    .grid { display: grid; grid-template-columns: 1fr auto; gap: 20px; }
    #dashboard .grid {
        grid-template-columns: 1fr 1fr auto;
        align-items: end;
        gap: 10px;
    }
    dialog header { display: flex; justify-content: space-between; align-items: center; }
    dialog h5 { margin: 0; }
    article { margin-bottom: 2rem; }
    table { margin-top: 1rem; }
    .table-wrapper {
      overflow-x: auto;
    }
    #property-details-container {
        border: 1px solid var(--contrast);
        padding: 1.5rem;
        grid-column: 2;
        margin: 0;
    }
    /* --- Estilos Responsivos --- */
    @media (max-width: 768px) {
      body {
        padding: 10px;
        --font-size: 15px;
      }
      
      /* Ajusta los grids para que sean de una sola columna en móviles */
      .grid, #dashboard .grid {
        grid-template-columns: 1fr;
        gap: 1rem;
      }

      /* Ajusta los formularios y listas de detalles para apilarse */
      #property-data dl, #form-edit-property {
        grid-template-columns: 1fr;
        gap: 5px 10px;
      }
      
      #property-data dt, #form-edit-property label,
      #property-data dd, #form-edit-property input, #form-edit-property textarea {
        grid-column: 1; /* Todos los elementos a una sola columna */
      }
      #property-data dd { margin-bottom: 10px; }
      dialog article { width: 95vw; }
    }
  </style>
</head>
<body>
      <header>
        <strong>Filtrar Vencimientos por Fecha</strong>
      </header>
      <div class="grid">
        <div>
          <label for="start-date">Fecha de Inicio</label>
          <input type="date" id="start-date">
        <button id="filter-button" onclick="handleFilterVencimientos()">Filtrar</button>
      </div>
      <div id="dashboard-loader" aria-busy="true" style="display: none;">Filtrando vencimientos...</div>
      <div class="table-wrapper">
        <table role="grid" id="vencimientos-proximos-table" style="display:none;">
          <thead>
            <tr>
              <th>Dirección</th>
              <th>Propietario</th>
              <th>Tipo</th>
              <th>Fecha Vencimiento</th>
              <th>Acciones</th>
            </tr>
          </thead>
          <tbody id="vencimientos-proximos-body"></tbody>
        </table>
      </div>
      <div id="dashboard-empty" style="display:none; text-align:center; padding: 20px; border: 1px dashed; border-radius: 5px;">
        <p>✅ No se encontraron vencimientos en el rango de fechas seleccionado.</p>
      </div>
         <h4 id="property-title"></h4>
         <div id="property-data"></div>
         <hr>
         <h5>Vencimientos Asociados</h5>
         <div class="table-wrapper">
           <table role="grid">
             <thead>
               <tr>
                 <th>Tipo de Vencimiento</th>
                 <th>Fecha</th>
                 <th>Acciones</th>
               </tr>
             </thead>
             <tbody id="property-vencimientos-body"></tbody>
           </table>
         </div>
      </div>
    </article>
    

´´´