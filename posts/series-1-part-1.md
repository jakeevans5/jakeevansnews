<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Jake Evans News - Article</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <link rel="icon" href="/favicon.ico" />
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/github-markdown-css/github-markdown.min.css" />

  <style>
    body {
      margin: 0;
      padding: 0;
      background: #f9fafb;
      font-family: ui-serif, Georgia, Cambria, "Times New Roman", Times, serif;
    }

    .jenews-wrap {
      max-width: 1040px;
      margin: 0 auto;
      padding: 18px 16px 28px;
    }

    .jenews-masthead {
      border-top: 3px solid #111827;
      border-bottom: 1px solid #d1d5db;
      padding: 14px 0 12px;
      margin-bottom: 14px;
      text-align: center;
    }

    .jenews-name {
      margin: 0;
      font-size: clamp(30px, 4vw, 54px);
      font-weight: 800;
    }

    .jenews-tagline {
      margin: 6px 0 0;
      color: #374151;
      font-size: 14.5px;
    }

    .jenews-nav {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 10px;
      padding: 12px 0 14px;
      border-bottom: 1px solid #e5e7eb;
      margin-bottom: 24px;
    }

    .jenews-nav ul {
      list-style: none;
      padding: 0;
      margin: 0;
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
    }

    .jenews-nav li {
      position: relative;
    }

    .jenews-nav a {
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      font-size: 13.5px;
      font-weight: 650;
      padding: 8px 12px;
      border-radius: 999px;
      border: 1px solid #bfdbfe;
      background: #eff6ff;
      color: #1e3a8a;
      text-decoration: none;
    }

    .jenews-nav a:hover {
      background: #1d4ed8;
      color: white;
      border-color: #1d4ed8;
    }

    .jenews-nav ul ul {
      display: none;
      flex-direction: column;
      position: absolute;
      top: 110%;
      left: 0;
      background: #eff6ff;
      padding: 10px;
      border-radius: 12px;
      z-index: 100;
    }

    #markdown-output {
      background: #fff;
      padding: 24px;
      border-radius: 12px;
      border: 1px solid #e5e7eb;
      box-shadow: 0 6px 16px rgba(17, 24, 39, 0.06);
    }
  </style>
</head>
<body>
  <div class="jenews-wrap">
    <!-- Header -->
    <header class="jenews-masthead">
      <h1 class="jenews-name">Jake Evans News</h1>
      <p class="jenews-tagline">Local updates • Civic preparation • Charter & Code • Upcoming meetings</p>
    </header>

    <!-- Navigation -->
    <nav class="jenews-nav">
      <ul>
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">About Jake Evans</a></li>
        <li><a href="preparing-to-serve.html">Preparing to Serve</a></li>
        <li>
          <a href="charter-code.html">Neosho Charter & Code ▾</a>
          <ul>
            <li><a href="the-neosho-city-charter-plain-english.html">Charter - Explained</a></li>
            <li><a href="city-code-explained.html">City Code - Explained</a></li>
            <li><a href="who-has-authority.html">Who Has Authority</a></li>
            <li><a href="how-to-look-up.html">How to Look Things Up</a></li>
          </ul>
        </li>
        <li><a href="meetings.html">Upcoming Meetings</a></li>
      </ul>
    </nav>

    <!-- Article Output -->
    <div id="markdown-output" class="markdown-body">
      <p>Loading article...</p>
    </div>
  </div>

  <!-- Marked Markdown Parser -->
  <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
  <script>
    // Get the markdown file name from the URL
    function getMarkdownFileFromURL() {
      const params = new URLSearchParams(window.location.search);
      return params.get("file") || "welcome.md";
    }

    const file = getMarkdownFileFromURL();
    const markdownPath = `posts/${file}`;

    fetch(markdownPath)
      .then(res => {
        if (!res.ok) throw new Error("Markdown file not found.");
        return res.text();
      })
      .then(md => {
        const html = marked.parse(md);
        document.getElementById('markdown-output').innerHTML = html;
      })
      .catch(err => {
        document.getElementById('markdown-output').innerHTML = `
          <h2>Error</h2>
          <p>Sorry, we couldn't load the article: <code>${file}</code></p>
        `;
        console.error(err);
      });
  </script>

  <!-- 🔁 Your Custom Link & Dropdown Script -->
  <script>
    document.querySelectorAll('a.jenews-link, a.jenews-pill').forEach(link => {
      link.setAttribute('target', '_self');
    });

    document.querySelectorAll('.jenews-nav li').forEach(li => {
      let timer;
      const submenu = li.querySelector('ul');

      if (submenu) {
        li.addEventListener('mouseenter', () => {
          clearTimeout(timer);
          submenu.style.display = 'flex';
        });

        li.addEventListener('mouseleave', () => {
          timer = setTimeout(() => {
            submenu.style.display = 'none';
          }, 300);
        });

        submenu.addEventListener('mouseenter', () => {
          clearTimeout(timer);
        });

        submenu.addEventListener('mouseleave', () => {
          timer = setTimeout(() => {
            submenu.style.display = 'none';
          }, 300);
        });
      }
    });
  </script>
</body>
</html>
