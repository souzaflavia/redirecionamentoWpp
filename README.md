# redirecionamentoWpp
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Redirecionando...</title>
  <script>
    async function redirecionar() {
      const urlParams = new URLSearchParams(window.location.search);
      const utm_source = urlParams.get("utm_source") || "";
      const utm_medium = urlParams.get("utm_medium") || "";
      const utm_campaign = urlParams.get("utm_campaign") || "";
      const utm_content = urlParams.get("utm_content") || "";
      const utm_term = urlParams.get("utm_term") || "";

      const scriptUrl = "https://script.google.com/macros/s/AKfycbzaq3ZF771vuXcTOLnGvDGFhJG0w2YFtPkmLE8NyLj8RfkFaqcYxH8OFj0CGuQPa4Yn/exec" +
        `?utm_source=${utm_source}&utm_medium=${utm_medium}&utm_campaign=${utm_campaign}&utm_content=${utm_content}&utm_term=${utm_term}`;

      try {
        const response = await fetch(scriptUrl);
        const texto = await response.text();
        const link = texto.match(/url=(.*?)"/)[1];
        window.location.href = link;
      } catch (error) {
        document.body.innerHTML = "Erro ao redirecionar.";
      }
    }

    redirecionar();
  </script>
</head>
<body>
  Redirecionando para o WhatsApp...
</body>
</html>

