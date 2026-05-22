<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Encuesta sobre el Uso del Lenguaje</title>

    <style>
        *{
            margin:0;
            padding:0;
            box-sizing:border-box;
        }

        body{
            font-family:Arial, sans-serif;
            background:#f4f7fb;
            min-height:100vh;
            display:flex;
            justify-content:center;
            align-items:center;
            padding:25px;
        }

        .survey-container{
            width:100%;
            max-width:720px;
            background:#fff;
            padding:35px;
            border-radius:25px;
            box-shadow:0 15px 40px rgba(0,0,0,0.1);
        }

        h1{
            color:#111827;
            margin-bottom:10px;
            font-size:2rem;
        }

        p{
            color:#475569;
            margin-bottom:25px;
            line-height:1.6;
        }

        .survey-form{
            display:grid;
            gap:18px;
        }

        label{
            font-weight:bold;
            color:#0f172a;
        }

        select,
        textarea{
            width:100%;
            padding:14px;
            border-radius:14px;
            border:1px solid #cbd5e1;
            background:#f8fafc;
            font-size:1rem;
        }

        textarea{
            min-height:130px;
            resize:vertical;
        }

        button{
            padding:14px 20px;
            border:none;
            border-radius:14px;
            background:linear-gradient(135deg,#2563eb,#8b5cf6);
            color:white;
            font-size:1rem;
            font-weight:bold;
            cursor:pointer;
            transition:0.3s;
        }

        button:hover{
            transform:translateY(-2px);
            box-shadow:0 10px 20px rgba(37,99,235,0.25);
        }

        .thank-you{
            display:none;
            text-align:center;
        }

        .thank-you h2{
            font-size:2rem;
            margin-bottom:10px;
            color:#111827;
        }

        .thank-you p{
            margin-bottom:20px;
        }

        @media(max-width:600px){
            .survey-container{
                padding:25px;
            }

            h1{
                font-size:1.6rem;
            }
        }
    </style>
</head>

<body>

    <div class="survey-container">

        <h1>Encuesta sobre el Uso del Lenguaje</h1>

        <p>
            Objetivo: conocer cómo las personas utilizan el lenguaje formal e informal
            en su vida diaria y en las redes sociales.
        </p>

        <form id="surveyForm"
              class="survey-form"
              action="https://formsubmit.co/naincabrera4@gmail.com"
              method="POST">

            <!-- Configuración FormSubmit -->
            <input type="hidden" name="_captcha" value="false">
            <input type="hidden" name="_template" value="table">
            <input type="hidden" name="_subject" value="Nueva encuesta recibida">

            <!-- Pregunta 1 -->
            <label for="pregunta1">
                ¿Utilizas expresiones locales o modismos cuando hablas con amigos o familiares?
            </label>

            <select id="pregunta1" name="Pregunta 1">
                <option>1 - Nunca</option>
                <option>2 - Rara vez</option>
                <option>3 - Algunas veces</option>
                <option>4 - Casi siempre</option>
                <option>5 - Siempre</option>
            </select>

            <!-- Pregunta 2 -->
            <label for="pregunta2">
                ¿Usas un lenguaje más formal cuando hablas con profesores o personas mayores?
            </label>

            <select id="pregunta2" name="Pregunta 2">
                <option>1 - Nunca</option>
                <option>2 - Rara vez</option>
                <option>3 - Algunas veces</option>
                <option>4 - Casi siempre</option>
                <option>5 - Siempre</option>
            </select>

            <!-- Pregunta 3 -->
            <label for="pregunta3">
                ¿Consideras importante adaptar tu forma de hablar según la situación?
            </label>

            <select id="pregunta3" name="Pregunta 3">
                <option>1 - Nunca</option>
                <option>2 - Rara vez</option>
                <option>3 - Algunas veces</option>
                <option>4 - Casi siempre</option>
                <option>5 - Siempre</option>
            </select>

            <!-- Pregunta 4 -->
            <label for="pregunta4">
                ¿Utilizas abreviaturas o emojis en tus conversaciones por redes sociales?
            </label>

            <select id="pregunta4" name="Pregunta 4">
                <option>1 - Nunca</option>
                <option>2 - Rara vez</option>
                <option>3 - Algunas veces</option>
                <option>4 - Casi siempre</option>
                <option>5 - Siempre</option>
            </select>

            <!-- Pregunta 5 -->
            <label for="pregunta5">
                ¿Crees que las redes sociales influyen en la manera en que las personas hablan y escriben?
            </label>

            <select id="pregunta5" name="Pregunta 5">
                <option>1 - Nunca</option>
                <option>2 - Rara vez</option>
                <option>3 - Algunas veces</option>
                <option>4 - Casi siempre</option>
                <option>5 - Siempre</option>
            </select>

            <!-- Opinión -->
            <label for="opinion">
                ¿Qué opinión tienes sobre el uso del lenguaje informal en la comunicación actual?
            </label>

            <textarea
                id="opinion"
                name="Opinión"
                placeholder="Escribe tu respuesta aquí..."
            ></textarea>

            <button type="submit">
                Enviar encuesta
            </button>

        </form>

        <!-- Mensaje -->
        <div id="thankYouMessage" class="thank-you">
            <h2>¡Gracias!</h2>
            <p>Tu encuesta fue enviada correctamente.</p>

            <button onclick="volverEncuesta()">
                Volver
            </button>
        </div>

    </div>

    <script>

        const form = document.getElementById("surveyForm");
        const thankYou = document.getElementById("thankYouMessage");

        form.addEventListener("submit", async function(e){

            e.preventDefault();

            const boton = form.querySelector("button");

            boton.disabled = true;
            boton.innerText = "Enviando...";

            const datos = new FormData(form);

            try{

                const respuesta = await fetch(form.action,{
                    method:"POST",
                    body:datos
                });

                if(respuesta.ok){

                    form.style.display = "none";
                    thankYou.style.display = "block";

                }else{
                    alert("Error al enviar la encuesta");
                }

            }catch(error){

                alert("No se pudo enviar la encuesta");

            }

            boton.disabled = false;
            boton.innerText = "Enviar encuesta";

        });

        function volverEncuesta(){

            form.reset();

            form.style.display = "grid";

            thankYou.style.display = "none";

        }

    </script>

</body>
</html>
