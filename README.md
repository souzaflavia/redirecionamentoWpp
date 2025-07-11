<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Redirecionando para o WhatsApp...</title>
  <script>
    async function redirecionar() {
      const urlParams = new URLSearchParams(window.location.search);
      const utm_source = urlParams.get("utm_source") || "";
      const utm_medium = urlParams.get("utm_medium") || "";
      const utm_campaign = urlParams.get("utm_campaign") || "";
      const utm_content = urlParams.get("utm_content") || "";
      const utm_term = urlParams.get("utm_term") || "";

      // ✅ COLA AQUI O SEU LINK DO APPS SCRIPT:
      const scriptUrl = "https://script.google.com/macros/s/AKfycbzaq3ZF771vuXcTOLnGvDGFhJG0w2YFtPkmLE8NyLj8RfkFaqcYxH8OFj0CGuQPa4Yn/exec" +
        `?utm_source=${utm_source}&utm_medium=${utm_medium}&utm_campaign=${utm_campaign}&utm_content=${utm_content}&utm_term=${utm_term}`;

      try {
        const response = await fetch(scriptUrl);
        const html = await response.text();

        // Converte o HTML da resposta para extrair o link
        const parser = new DOMParser();
        const doc = parser.parseFromString(html, "text/html");
        const meta = doc.querySelector("meta[http-equiv='refresh']");

        if (meta) {
          const content = meta.getAttribute("content"); // "0; url=LINK"
          const link = content.split("url=")[1];
          window.location.href = link;
        } else {
          document.body.innerHTML = "Erro: link de redirecionamento não encontrado.";
        }

      } catch (error) {
        document.body.innerHTML = "Erro ao redirecionar. Verifique o link ou o script.";
        console.error(error);
      }
    }

    redirecionar();
  </script>
</head>
<body>
  <p style="font-family: sans-serif;">Aguarde, redirecionando para o WhatsApp...</p>
</body>
</html>
