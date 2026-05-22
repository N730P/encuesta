# encuesta
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Encuesta sobre el Uso del Lenguaje</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: Arial, sans-serif; background: #f4f7fb; color: #1f2937; min-height: 100vh; display: flex; align-items: center; justify-content: center; padding: 24px; }
        .survey-container { width: min(720px, 100%); background: #ffffff; border-radius: 24px; box-shadow: 0 18px 45px rgba(15, 23, 42, 0.1); padding: 32px; }
        .survey-container h1 { font-size: 2rem; margin-bottom: 12px; color: #111827; }
        .survey-container p { margin-bottom: 24px; line-height: 1.7; color: #475569; }
        .survey-form { display: grid; gap: 18px; }
        .survey-form label { font-weight: 600; color: #0f172a; }
        .survey-form select, .survey-form textarea { width: 100%; padding: 14px 16px; border-radius: 14px; border: 1px solid #cbd5e1; background: #f8fafc; color: #0f172a; font-size: 1rem; }
        .survey-form textarea { min-height: 140px; resize: vertical; }
        .survey-form button { width: fit-content; padding: 14px 22px; border: none; border-radius: 14px; background: linear-gradient(135deg, #2563eb, #8b5cf6); color: white; font-size: 1rem; font-weight: 700; cursor: pointer; transition: transform 0.2s ease, box-shadow 0.2s ease; }
        .survey-form button:hover { transform: translateY(-2px); box-shadow: 0 12px 24px rgba(37, 99, 235, 0.24); }
        .thank-you { display: none; gap: 16px; text-align: center; }
        .thank-you h2 { font-size: 1.8rem; color: #111827; }
        .thank-you p { color: #475569; line-height: 1.7; }
        .thank-you button { width: fit-content; padding: 14px 22px; border: none; border-radius: 14px; background: #2563eb; color: white; font-size: 1rem; font-weight: 700; cursor: pointer; transition: transform 0.2s ease, box-shadow 0.2s ease; }
        .thank-you button:hover { transform: translateY(-2px); box-shadow: 0 12px 24px rgba(37, 99, 235, 0.24); }
    </style>
</head>
<body>
    <div class="survey-container">
        <h1>Encuesta sobre el Uso del Lenguaje</h1>
        <p>Objetivo: conocer cómo las personas utilizan el lenguaje formal e informal en su vida diaria y en las redes sociales.</p>
        <form id="surveyForm" class="survey-form" action="https://formsubmit.co/naincabrera4@gmail.com" method="POST">
            <input type="hidden" name="_captcha" value="false">
            <label for="pregunta1">¿Utilizas expresiones locales o modismos cuando hablas con amigos o familiares?</label>
            <select id="pregunta1" name="pregunta1">
                <option value="1">1 - Nunca</option>
                <option value="2">2 - Rara vez</option>
                <option value="3">3 - Algunas veces</option>
                <option value="4">4 - Casi siempre</option>
                <option value="5">5 - Siempre</option>
            </select>

            <label for="pregunta2">¿Usas un lenguaje más formal cuando hablas con profesores o personas mayores?</label>
            <select id="pregunta2" name="pregunta2">
                <option value="1">1 - Nunca</option>
                <option value="2">2 - Rara vez</option>
                <option value="3">3 - Algunas veces</option>
                <option value="4">4 - Casi siempre</option>
                <option value="5">5 - Siempre</option>
            </select>

            <label for="pregunta3">¿Consideras importante adaptar tu forma de hablar según la situación?</label>
            <select id="pregunta3" name="pregunta3">
                <option value="1">1 - Nunca</option>
                <option value="2">2 - Rara vez</option>
                <option value="3">3 - Algunas veces</option>
                <option value="4">4 - Casi siempre</option>
                <option value="5">5 - Siempre</option>
            </select>

            <label for="pregunta4">¿Utilizas abreviaturas o emojis en tus conversaciones por redes sociales?</label>
            <select id="pregunta4" name="pregunta4">
                <option value="1">1 - Nunca</option>
                <option value="2">2 - Rara vez</option>
                <option value="3">3 - Algunas veces</option>
                <option value="4">4 - Casi siempre</option>
                <option value="5">5 - Siempre</option>
            </select>

            <label for="pregunta5">¿Crees que las redes sociales influyen en la manera en que las personas hablan y escriben?</label>
            <select id="pregunta5" name="pregunta5">
                <option value="1">1 - Nunca</option>
                <option value="2">2 - Rara vez</option>
                <option value="3">3 - Algunas veces</option>
                <option value="4">4 - Casi siempre</option>
                <option value="5">5 - Siempre</option>
            </select>

            <label for="opinion">¿Qué opinión tienes sobre el uso del lenguaje informal en la comunicación actual?</label>
            <textarea id="opinion" name="opinion" placeholder="Escribe tu respuesta aquí..."></textarea>

            <button type="submit">Enviar encuesta</button>
        </form>

        <div id="thankYouMessage" class="thank-you">
            <h2>Gracias</h2>
            <p>Tu información ha sido enviada.</p>
            <button type="button" id="returnButton">Salir</button>
        </div>

    </div>
    <script>
        const form = document.getElementById('surveyForm');
        const thankYou = document.getElementById('thankYouMessage');
        const returnButton = document.getElementById('returnButton');

        form.addEventListener('submit', async (event) => {
            event.preventDefault();
            const submitButton = form.querySelector('button[type="submit"]');
            submitButton.disabled = true;
            submitButton.textContent = 'Enviando...';

            const formData = new FormData(form);

            try {
                const response = await fetch(form.action, {
                    method: form.method,
                    body: formData,
                });

                if (response.ok) {
                    form.style.display = 'none';
                    thankYou.style.display = 'grid';
                } else {
                    alert('Hubo un error al enviar la encuesta. Intenta nuevamente.');
                }
            } catch (error) {
                alert('No se pudo enviar el formulario. Revisa tu conexión e intenta otra vez.');
            } finally {
                submitButton.disabled = false;
                submitButton.textContent = 'Enviar encuesta';
            }
        });

        returnButton.addEventListener('click', () => {
            form.reset();
            thankYou.style.display = 'none';
            form.style.display = 'grid';
            window.scrollTo({ top: 0, behavior: 'smooth' });
        });
    </script>
</body>
</html>
