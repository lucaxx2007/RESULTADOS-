<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Portfólio de Resultados</title>
  <meta name="description" content="Portfólio de alta performance com resultados visuais impressionantes." />
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Inter', sans-serif;
      margin: 0;
      padding: 0;
      background: #111;
      color: #fff;
    }
    header {
      background: linear-gradient(90deg, #0f2027, #203a43, #2c5364);
      padding: 2rem;
      text-align: center;
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.4);
    }
    header h1 {
      font-size: 2.5rem;
      margin: 0;
    }
    main {
      max-width: 1200px;
      margin: 2rem auto;
      padding: 0 1rem;
    }
    form {
      background: #1e1e1e;
      padding: 2rem;
      border-radius: 12px;
      box-shadow: 0 0 16px rgba(255, 255, 255, 0.05);
      margin-bottom: 3rem;
    }
    input, textarea, button {
      width: 100%;
      margin-bottom: 1rem;
      padding: 0.8rem;
      border: none;
      border-radius: 8px;
      font-size: 1rem;
    }
    input, textarea {
      background: #2a2a2a;
      color: #fff;
    }
    button {
      background: #00bcd4;
      color: #000;
      font-weight: 600;
      cursor: pointer;
      transition: background 0.3s ease;
    }
    button:hover {
      background: #00acc1;
    }
    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 2rem;
    }
    .card {
      background: #1a1a1a;
      padding: 1rem;
      border-radius: 10px;
      box-shadow: 0 0 12px rgba(0, 255, 255, 0.1);
      transition: transform 0.3s ease, box-shadow 0.3s ease;
    }
    .card:hover {
      transform: scale(1.03);
      box-shadow: 0 0 20px rgba(0, 255, 255, 0.2);
    }
    .before-after {
      display: flex;
      gap: 1rem;
    }
    .before-after img {
      width: 50%;
      border-radius: 8px;
    }
    .card p {
      margin-top: 1rem;
      font-size: 1rem;
      color: #ccc;
    }
    @media (max-width: 600px) {
      .before-after {
        flex-direction: column;
      }
      .before-after img {
        width: 100%;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>Portfólio de Resultados Profissionais</h1>
  </header>
  <main>
    <form id="uploadForm">
      <input type="file" id="beforeImage" accept="image/*" required />
      <input type="file" id="afterImage" accept="image/*" required />
      <textarea id="descriptionInput" placeholder="Descrição do resultado..." required></textarea>
      <button type="submit">Publicar Resultado</button>
    </form>

    <div class="gallery" id="gallery"></div>
  </main>

  <script>
    const form = document.getElementById('uploadForm');
    const beforeImage = document.getElementById('beforeImage');
    const afterImage = document.getElementById('afterImage');
    const descriptionInput = document.getElementById('descriptionInput');
    const gallery = document.getElementById('gallery');

    form.addEventListener('submit', function (e) {
      e.preventDefault();
      const beforeFile = beforeImage.files[0];
      const afterFile = afterImage.files[0];
      const description = descriptionInput.value;

      if (!beforeFile || !afterFile || !description) {
        alert('Por favor, envie as duas imagens e a descrição.');
        return;
      }

      const beforeReader = new FileReader();
      const afterReader = new FileReader();

      beforeReader.onload = function (beforeEvent) {
        afterReader.onload = function (afterEvent) {
          const card = document.createElement('div');
          card.className = 'card';

          const container = document.createElement('div');
          container.className = 'before-after';

          const beforeImg = document.createElement('img');
          beforeImg.src = beforeEvent.target.result;
          beforeImg.alt = 'Antes';

          const afterImg = document.createElement('img');
          afterImg.src = afterEvent.target.result;
          afterImg.alt = 'Depois';

          container.appendChild(beforeImg);
          container.appendChild(afterImg);

          const desc = document.createElement('p');
          desc.textContent = description;

          card.appendChild(container);
          card.appendChild(desc);
          gallery.prepend(card);

          form.reset();
        };
        afterReader.readAsDataURL(afterFile);
      };
      beforeReader.readAsDataURL(beforeFile);
    });
  </script>
</body>
</html>
