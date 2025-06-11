<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calendario Ordinario</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f0f0f0;
            color: #333;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 30px;
        }

        h1 {
            margin-bottom: 10px;
        }

        .clock {
            font-size: 2em;
            margin-bottom: 30px;
        }

        .calendar {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 10px;
            max-width: 500px;
            margin-top: 20px;
        }

        .day {
            background: #fff;
            padding: 15px;
            text-align: center;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        .header {
            font-weight: bold;
            background: #007bff;
            color: white;
        }

        .month-year {
            font-size: 1.5em;
            margin: 20px 0;
        }
    </style>
</head>
<body>

    <h1>Calendario Ordinario</h1>
    <div class="clock" id="clock">00:00:00</div>
    <div class="month-year" id="monthYear"></div>

    <div class="calendar" id="calendar">
        <!-- Aquí se insertan los días con JavaScript -->
    </div>

    <script>
        function updateClock() {
            const now = new Date();
            const hours = String(now.getHours()).padStart(2, '0');
            const minutes = String(now.getMinutes()).padStart(2, '0');
            const seconds = String(now.getSeconds()).padStart(2, '0');
            document.getElementById('clock').textContent = `${hours}:${minutes}:${seconds}`;
        }

        setInterval(updateClock, 1000);
        updateClock();

        function renderCalendar() {
            const calendar = document.getElementById('calendar');
            const monthYear = document.getElementById('monthYear');
            calendar.innerHTML = '';

            const now = new Date();
            const year = now.getFullYear();
            const month = now.getMonth(); // 0 = Enero
            const firstDay = new Date(year, month, 1).getDay(); // Día de la semana
            const daysInMonth = new Date(year, month + 1, 0).getDate();

            const dayNames = ['Dom', 'Lun', 'Mar', 'Mié', 'Jue', 'Vie', 'Sáb'];
            dayNames.forEach(day => {
                const header = document.createElement('div');
                header.className = 'day header';
                header.textContent = day;
                calendar.appendChild(header);
            });

            // Espacios vacíos al inicio
            for (let i = 0; i < firstDay; i++) {
                const emptyCell = document.createElement('div');
                emptyCell.className = 'day';
                calendar.appendChild(emptyCell);
            }

            // Días del mes
            for (let day = 1; day <= daysInMonth; day++) {
                const dayCell = document.createElement('div');
                dayCell.className = 'day';
                dayCell.textContent = day;
                calendar.appendChild(dayCell);
            }

            const monthNames = [
                'Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio',
                'Julio', 'Agosto', 'Septiembre', 'Octubre', 'Noviembre', 'Diciembre'
            ];

            monthYear.textContent = `${monthNames[month]} ${year}`;
        }

        renderCalendar();
    </script>
</body>
</html>

