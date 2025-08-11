<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Reservas - Green House San Ramón</title>
    <style>
        /* Estilos CSS básicos para que se vea un poco mejor */
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f4f4f4;
            color: #333;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: #fff;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1, h2 {
            color: #28a745; /* Color verde para los títulos */
            text-align: center;
        }
        .section {
            margin-bottom: 25px;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            background-color: #f9f9f9;
        }
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
        }
        input[type="text"],
        input[type="email"],
        input[type="tel"],
        input[type="date"],
        textarea {
            width: calc(100% - 20px);
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box; /* Incluye padding en el ancho total */
        }
        button {
            background-color: #28a745;
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        button.cancel {
            background-color: #dc3545; /* Rojo para cancelar */
            margin-left: 10px;
        }
        button:hover {
            opacity: 0.9;
        }
        .booking-details {
            background-color: #e2f0d9; /* Fondo claro para detalles de reserva */
            padding: 15px;
            border-left: 5px solid #28a745;
            margin-top: 20px;
        }
        .occupied-dates {
            color: #dc3545; /* Rojo para fechas ocupadas */
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🏡 Reservar en Green House San Ramón 🏡</h1>
        <p style="text-align: center; font-style: italic;">Tu escape perfecto en San Ramón.</p>

        <hr>

        <div class="section">
            <h2>📅 Selecciona tus Fechas</h2>
            <p>Por favor, elige el día de **entrada** y el día de **salida** en el calendario. Recuerda que la entrada es a las **3:00 p.m.** del primer día y la salida a las **11:00 a.m.** del último día.</p>
            
            <label for="fechaEntrada">Fecha de Entrada:</label>
            <input type="date" id="fechaEntrada" name="fechaEntrada" required>

            <label for="fechaSalida">Fecha de Salida:</label>
            <input type="date" id="fechaSalida" name="fechaSalida" required>

            <div class="occupied-dates">
                <p>Fechas ya ocupadas: (Esto se actualizará dinámicamente)</p>
                <ul>
                    <li>15 de Agosto, 2025</li>
                    <li>20 al 22 de Septiembre, 2025</li>
                    </ul>
            </div>
        </div>

        <hr>

        <div class="section">
            <h2>📝 Tus Datos de Contacto</h2>
            <form id="bookingForm">
                <label for="nombreCliente">Nombre Completo:</label>
                <input type="text" id="nombreCliente" name="nombreCliente" placeholder="Ej: Juan Pérez" required>

                <label for="correoCliente">Correo Electrónico:</label>
                <input type="email" id="correoCliente" name="correoCliente" placeholder="Ej: tu_correo@ejemplo.com" required>

                <label for="telefonoCliente">Número de Teléfono:</label>
                <input type="tel" id="telefonoCliente" name="telefonoCliente" placeholder="Ej: 8888-7777" required>

                <button type="submit">Confirmar Reserva</button>
                <button type="button" class="cancel" id="cancelReservationBtn">Cancelar Reserva</button>
            </form>
        </div>

        <hr>

        <div class="section booking-details">
            <h2>ℹ️ Detalles Importantes de tu Reserva</h2>
            <p><strong>Hora de Entrada:</strong> 3:00 p.m. del primer día de tu reserva.</p>
            <p><strong>Hora de Salida:</strong> 11:00 a.m. del último día de tu reserva.</p>
            <p>Si reservas un solo día, la entrada es a las 3:00 p.m. y la salida a las 11:00 a.m. del día siguiente.</p>
            <p>Si reservas múltiples días, la entrada es a las 3:00 p.m. del primer día y la salida a las 11:00 a.m. del último día.</p>
        </div>
    </div>

    <script>
        // Este es un JavaScript muy básico para la demostración.
        // Para una funcionalidad real, necesitarías enviar estos datos a un servidor
