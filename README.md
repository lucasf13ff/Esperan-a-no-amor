<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Esperança no Amor</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet">
  <style>
    body { font-family: 'Inter', sans-serif; margin: 0; padding: 0;
      background: #fafafa; display: flex; flex-direction: column; align-items: center; }
    header { padding: 20px; text-align: center; background-color: #f06292;
      color: white; width: 100%; }
    main { padding: 40px; text-align: center; }
    button { padding: 10px 20px; font-size: 16px;
      background-color: #ec407a; color: white; border: none; border-radius: 6px;
      cursor: pointer; }
    button:hover { background-color: #d81b60; }
  </style>
</head>
<body>
  <header>
    <h1>Esperança no Amor ❤️</h1>
  </header>
  <main id="main-content">
    <p>Encontre pessoas com interesses parecidos. Cadastre-se para conversar!</p>
    <button onclick="loginGoogle()">Entrar com Google</button>
  </main>

  <script type="module">
    import { createClient } from 'https://esm.sh/@supabase/supabase-js'

    const supabaseUrl = 'https://SEU_SUPABASE_URL.supabase.co';
    const supabaseKey = 'SUA_CHAVE_PUBLIC_ANON';
    const supabase = createClient(supabaseUrl, supabaseKey);

    window.loginGoogle = async () => {
      const { error } = await supabase.auth.signInWithOAuth({ provider: 'google' });
      if (error) alert('Erro ao logar: ' + error.message);
    };

    // Se já estiver logado, mostra boas-vindas
    supabase.auth.getUser().then(({ data: { user } }) => {
      if (user) {
        document.getElementById('main-content').innerHTML = `
          <h2>Bem-vindo, ${user.user_metadata.full_name || user.email}!</h2>
          <p>Seu login via Google funcionou 😊</p>
        `;
      }
    });
  </script>
</body>
</html>

