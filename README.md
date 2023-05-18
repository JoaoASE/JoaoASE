<!DOCTYPE html>
<html>
<head>
  <title>Dashboard de Linguagens</title>
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script>
    // Função para buscar as linguagens utilizadas nos repositórios
    function getLanguages() {
      // Fazer uma requisição GET para a API do GitHub
      axios.get('https://api.github.com/users/JoaoASE/repos')
        .then(response => {
          // Array para armazenar as linguagens
          let languages = {};

          // Iterar sobre os repositórios
          response.data.forEach(repo => {
            // Verificar se o repositório possui uma linguagem definida
            if (repo.language) {
              // Adicionar a linguagem ao objeto languages e incrementar a contagem
              if (languages[repo.language]) {
                languages[repo.language]++;
              } else {
                languages[repo.language] = 1;
              }
            }
          });

          // Exibir as linguagens no dashboard
          const dashboard = document.getElementById('dashboard');
          for (let language in languages) {
            const languageItem = document.createElement('div');
            languageItem.textContent = `${language}: ${languages[language]}`;
            dashboard.appendChild(languageItem);
          }
        })
        .catch(error => {
          console.error(error);
        });
    }
  </script>
</head>
<body onload="getLanguages()">
  <h1>Dashboard de Linguagens</h1>
  <div id="dashboard"></div>
</body>
</html>
