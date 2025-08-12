<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Green House San Ramón - Reservas</title>
    <!-- CDN de Tailwind CSS para un diseño moderno y responsive -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Estilo básico para la fuente y el fondo */
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f0f4f8; /* Un fondo gris claro */
        }
    </style>
</head>
<body class="flex items-center justify-center min-h-screen p-4">

    <!-- Contenedor principal de la página de reservas -->
    <div class="bg-white rounded-xl shadow-2xl p-8 max-w-2xl w-full">
        <!-- Título y descripción -->
        <header class="text-center mb-8">
            <h1 class="text-4xl font-extrabold text-gray-800">🏡 Green House San Ramón</h1>
            <p class="mt-2 text-lg text-gray-600">¡Reserva tu estancia y relájate!</p>
            <p class="mt-4 text-sm text-gray-500">
                El check-in es a partir de las <span class="font-bold">3:00 p.m.</span> y el check-out a las <span class="font-bold">11:00 a.m.</span> del día siguiente.
            </p>
        </header>

        <!-- Formulario de reserva -->
        <form id="reservation-form">
            <div class="grid md:grid-cols-2 gap-6 mb-6">
                <!-- Selector de fecha de entrada -->
                <div>
                    <label for="checkin" class="block text-sm font-medium text-gray-700">Fecha de Entrada</label>
                    <input type="date" id="checkin" name="checkin" class="mt-1 block w-full p-3 border border-gray-300 rounded-md shadow-sm focus:ring-green-500 focus:border-green-500" required>
                </div>
                <!-- Selector de fecha de salida -->
                <div>
                    <label for="checkout" class="block text-sm font-medium text-gray-700">Fecha de Salida</label>
                    <input type="date" id="checkout" name="checkout" class="mt-1 block w-full p-3 border border-gray-300 rounded-md shadow-sm focus:ring-green-500 focus:border-green-500" required>
                </div>
            </div>

            <div class="mb-6">
                <label for="name" class="block text-sm font-medium text-gray-700">Nombre Completo</label>
                <input type="text" id="name" name="name" placeholder="Ej: Juan Pérez" class="mt-1 block w-full p-3 border border-gray-300 rounded-md shadow-sm focus:ring-green-500 focus:border-green-500" required>
            </div>

            <div class="mb-6">
                <label for="email" class="block text-sm font-medium text-gray-700">Correo Electrónico</label>
                <input type="email" id="email" name="email" placeholder="Ej: tu.correo@ejemplo.com" class="mt-1 block w-full p-3 border border-gray-300 rounded-md shadow-sm focus:ring-green-500 focus:border-green-500" required>
            </div>

            <div class="mb-6">
                <label for="phone" class="block text-sm font-medium text-gray-700">Número de Teléfono</label>
                <input type="tel" id="phone" name="phone" placeholder="Ej: 8888-8888" class="mt-1 block w-full p-3 border border-gray-300 rounded-md shadow-sm focus:ring-green-500 focus:border-green-500" required>
            </div>

            <!-- Botón de envío del formulario -->
            <button type="submit" class="w-full bg-green-600 text-white font-bold py-3 px-4 rounded-md hover:bg-green-700 transition duration-300">
                Confirmar Reserva
            </button>
        </form>

        <hr class="my-8 border-gray-200">

        <!-- Sección de cancelación de reserva -->
        <div class="text-center">
            <h2 class="text-xl font-bold text-gray-800 mb-4">¿Necesitas cancelar tu reserva?</h2>
            <p class="text-sm text-gray-600 mb-4">Ingresa tu código de reserva para proceder con la cancelación.</p>
            <div class="flex flex-col md:flex-row gap-4">
                <input type="text" id="cancel-code" name="cancel-code" placeholder="Tu código de reserva" class="flex-grow p-3 border border-gray-300 rounded-md shadow-sm focus:ring-red-500 focus:border-red-500" required>
                <button type="button" id="cancel-button" class="bg-red-600 text-white font-bold py-3 px-4 rounded-md hover:bg-red-700 transition duration-300">
                    Cancelar Reserva
                </button>
            </div>
        </div>
    </div>

    <!-- Script de JavaScript para la interactividad del lado del cliente -->
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const form = document.getElementById('reservation-form');
            const checkinInput = document.getElementById('checkin');
            const checkoutInput = document.getElementById('checkout');
            const cancelButton = document.getElementById('cancel-button');
            const cancelCodeInput = document.getElementById('cancel-code');

            // Establecer la fecha mínima de entrada como el día de hoy
            const today = new Date().toISOString().split('T')[0];
            checkinInput.min = today;

            // Asegurarse de que la fecha de salida sea al menos un día después de la entrada
            checkinInput.addEventListener('change', (event) => {
                const checkinDate = new Date(event.target.value);
                const nextDay = new Date(checkinDate);
                nextDay.setDate(checkinDate.getDate() + 1);
                checkoutInput.min = nextDay.toISOString().split('T')[0];

                // Si la fecha de salida seleccionada es anterior a la nueva mínima, la actualiza
                if (checkoutInput.value < checkoutInput.min) {
                    checkoutInput.value = checkoutInput.min;
                }
            });

            // Manejar el envío del formulario de reserva
            form.addEventListener('submit', (event) => {
                event.preventDefault(); // Evita que el formulario se envíe de forma tradicional

                const formData = new FormData(form);
                const reservationData = Object.fromEntries(formData.entries());

                // Validar que la fecha de salida sea después de la de entrada
                if (new Date(reservationData.checkout) <= new Date(reservationData.checkin)) {
                    alert('La fecha de salida debe ser posterior a la fecha de entrada.');
                    return;
                }

                // --- ESTE ES EL PUNTO CLAVE PARA LA LÓGICA DEL BACKEND ---
                // En un entorno real, aquí se haría una llamada a una API (fetch) a tu servidor.
                // El servidor procesaría la reserva, la guardaría en una base de datos y enviaría el correo de confirmación.
                
                // Muestra un mensaje de éxito simulado
                const message = `¡Reserva para ${reservationData.name} confirmada!\n\n` +
                                `Fechas: ${reservationData.checkin} - ${reservationData.checkout}\n` +
                                `Recibirás un correo de confirmación en ${reservationData.email}.`;
                
                // Usamos un simple alert para la demostración
                alert(message);
                console.log("Datos de la reserva enviados al servidor:", reservationData);

                // Resetear el formulario después de la "reserva"
                form.reset();
            });

            // Manejar el clic en el botón de cancelar
            cancelButton.addEventListener('click', () => {
                const code = cancelCodeInput.value;
                if (!code) {
                    alert('Por favor, introduce tu código de reserva.');
                    return;
                }

                // --- LÓGICA DEL BACKEND PARA CANCELACIÓN ---
                // Aquí se haría otra llamada a la API para enviar el código al servidor.
                // El servidor validaría el código y procesaría la cancelación.

                // Muestra un mensaje de cancelación simulada
                alert(`Solicitud de cancelación para el código ${code} procesada. Recibirás una confirmación por correo.`);
                console.log("Solicitud de cancelación para el código:", code);

                // Limpiar el campo del código
                cancelCodeInput.value = '';
            });
        });
    </script>
</body>
</html>
