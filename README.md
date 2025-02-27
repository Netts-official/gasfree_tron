# Documentation of the new GasFree functionality from Tron

v 1.1

<!doctype html>
<html lang="ru">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GasFree Developer Documentation</title>
  <!-- Подключаем внешний CSS -->
  <link rel="stylesheet" href="assets/css/styles.css">
  <!-- Подключаем шрифт Open Sans -->
  <link href="https://fonts.googleapis.com/css?family=Open+Sans:400,600,700&display=swap" rel="stylesheet">
</head>

<body>
  <header>
    <div class="container">
      <h1>GasFree Developer Documentation</h1>
      <div class="version-switcher">
        <label for="version-select">Версия:</label>
        <select id="version-select" onchange="location = this.value;">
          <option value="index.html" selected>1.0.0</option>
          <!-- Пример для более ранней версии -->
          <option value="ver/v0.9/index.html">0.9.0</option>
        </select>
      </div>
    </div>
  </header>

  <nav class="sidebar">
    <h2>Содержание</h2>
    <!-- Содержание можно взять из исходного TOC -->
    <div class="table-of-contents">
      <!-- Сохранённый исходный блок Table of Contents -->
      <p><span>Table of Contents</span></p>
      <ol>
        <li>
          <p><a href="#overview"><strong><span>Overview</span></strong></a></p>
        </li>
        <li>
          <p><a href="#authorization-process"><strong><span>Authorization Process</span></a></strong></p>
        </li>
        <li>
          <p><a href="#signature-algorithm-and-provider-endpoint"><strong><span>Signature Algorithm and Provider
                  Endpoint</span></strong></a></p>
          <ol>
            <li>
              <p><a href="#31-parameters"><span>3.1 Parameters</span></a></p>
            </li>
            <li>
              <p><a href="#32-authorization-construction-and-signature"><span>3.2 Authorization Construction and
                    Signature</span></a></p>
            </li>
            <li>
              <p><a href="#33-provider-endpoint"><span>3.3 Provider Endpoint</span></a></p>
            </li>
          </ol>
        </li>
        <li>
          <p><a href="#notes"><strong><span>Notes</span></strong></a></p>
        </li>
        <li>
          <p><a href="#apis"><strong><span>APIs</span></strong></a></p>
          <ol>
            <li>
              <p><a href="#api-authentication"><span>API Authentication</span></a></p>
            </li>
            <li>
              <p><a href="#api-format-definition"><span>API Format Definition</span></a></p>
            </li>
            <li>
              <p><a href="#get-apiv1configtokenall"><span>GET /api/v1/config/token/all</span></a></p>
            </li>
            <li>
              <p><a href="#get-apiv1configproviderall"><span>GET /api/v1/config/provider/all</span></a></p>
            </li>
            <li>
              <p><a href="#get-apiv1addressaccountaddress"><span>GET /api/v1/address/{accountAddress}</span></a></p>
            </li>
            <li>
              <p><a href="#post-apiv1gasfreesubmit"><span>POST /api/v1/gasfree/submit</span></a></p>
            </li>
            <li>
              <p><a href="#get-apiv1gasfreetraceid"><span>GET /api/v1/gasfree/{traceId}</span></a></p>
            </li>
          </ol>
        </li>
      </ol>
    </div>
  </nav>

  <main class="content">
    <div class="container">
      <!-- Здесь вставляем весь оригинальный контент (без изменений) -->
      <!-- Например, можно обернуть его в article -->
      <article id="doc-content">
        <!-- Начало исходного содержимого -->
        <h1 id="gasfree-developer-documentation">
          <span>GasFree Developer Documentation</span>
        </h1>
        <p style="text-align: center; margin-bottom: 100px; white-space: unset;">
          <span>Ver: 1.0.0 </span><br />
        </p>
        <div class="table-of-contents">
          <p><span>Table of Contents</span></p>
          <ol>
            <li>
              <p><a href="#overview"><strong><span>Overview</span></strong></a></p>
            </li>
            <li>
              <p><a href="#authorization-process"><strong><span>Authorization Process</span></strong></a></p>
            </li>
            <li>
              <p><a href="#signature-algorithm-and-provider-endpoint"><strong><span>Signature Algorithm and Provider
                      Endpoint</span></strong></a></p>
              <ol>
                <p style="white-space:normal"><a href="#31-parameters"><span>3.1 Parameters</span></a></p>
                <p style="white-space:normal"><a href="#32-authorization-construction-and-signature"><span>3.2
                      Authorization Construction and Signature</span></a></p>
                <p style="white-space:normal"><a href="#33-provider-endpoint"><span>3.3 Provider Endpoint</span></a></p>
              </ol>
            </li>
            <li>
              <p><a href="#notes"><strong><span>Notes</span></strong></a></p>
            </li>
            <li>
              <p><a href="#apis"><strong><span>APIs</span></strong></a></p>
              <p><a href="#api-authentication"><span>API Authentication</span></a></p>
              <p><a href="#api-format-definition"><span>API Format Definition</span></a></p>
              <p><a href="#get-apiv1configtokenall"><span>GET /api/v1/config/token/all</span></a></p>
              <p><a href="#get-apiv1configproviderall"><span>GET /api/v1/config/provider/all</span></a></p>
              <p><a href="#get-apiv1addressaccountaddress"><span>GET /api/v1/address/{accountAddress}</span></a></p>
              <p><a href="#post-apiv1gasfreesubmit"><span>POST /api/v1/gasfree/submit</span></a></p>
              <p><a href="#get-apiv1gasfreetraceid"><span>GET /api/v1/gasfree/{traceId}</span></a></p>
            </li>
          </ol>
        </div>
        <!-- Далее продолжается оригинальный контент документации -->
        <!-- ... (весь исходный HTML с инструкциями, примерами, таблицами, кодом, и т.д.) -->
      </article>
    </div>
  </main>

  <footer>
    <div class="container">
      <p>&copy; 2025 GasFree. Все права защищены.</p>
    </div>
  </footer>

  <!-- Можно добавить JS для интерактивных элементов, если потребуется -->
  <script>
    // Пример: можно реализовать динамическое сворачивание разделов или обработку переключателя версий
  </script>
</body>

</html>
