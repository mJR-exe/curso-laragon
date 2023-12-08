## 1 - Criar projeto laravel
Utilizar o comando `composer create-project laravel/laravel example-app`

## 2 - Estuturação de pastas:
- app: Esta pasta contém a lógica central da sua aplicação. Os controllers, models, middlewares e outros componentes relacionados àlógica de negócios estão organizados aqui.
- bootstrap: Contém os scripts iniciais para carregar o ambiente de aplicação e iniciar o processo de inicialização do Laravel.
- config: Aqui ficam os arquivos de configuração da aplicação como as configurações do banco de dados, cache, serviços...
- database: utilizado para armazenar as migrações do banco de dados e as sementes (seeders), que ajudam a controlar a estrutura dobanco de dados e fornecem dados iniciais.
- public: ponto de entrada para a aplicação e contém o arquivo index.php. Todo o conteúdo público, como imagens, CSS e JS, deve sercolocado aqui para ser acessível publicamente.
- resources: Armazena ativos não processados, como arquivos Blade (para as views), folhas de estilo SASS, arquivos de linguagem earquivos de template.
- routes: Contém os arquivos de rota da aplicação. O arquivo web.php geralmente lida com as rotas da interface do usuário, enquanto oarquivo api.php trata das rotas da API.
- storage: Armazena arquivos temporários gerados pela aplicação, como arquivos de log, arquivos de sessão e arquivos de cache.
- tests: É o diretório onde você pode colocar seus testes automatizados para garantir que o código funcione conforme o esperado.
- vendor: Esta pasta é gerada pelo Composer e contém todas as dependências do projeto.
- .env: Este arquivo contém as configurações específicas da aplicação, como informações do banco de dados, chaves de API e outrasconfigurações sensíveis.
- artisan: O Artisan é a interface de linha de comando incluída no Laravel. Ele fornece várias ferramentas úteis para automatizartarefas comuns de desenvolvimento.
	
## 3 - Artisan comandos
- `php artisan serve`: inicia um servidor
- `down`: coloca a aplicação em modo de manutenção
- `up`: coloca a aplicação no ar
	
## 4 - Rotas (web.php)
- As views estão na pasta resources/views e são sites que podem somente ser acessados pelo método **get**
- Exemplo de uma view:
    ```php
	Route::get('/empresa', function () {
		return return view("empresa");
	});
    ```
- Exemplo de uma view dentro de uma pasta:
    ```php
	Route::get('/empresa', function () {
        return view("site/empresa");
    });
    ```
    Essa mesma view pode ser simplificada com o seguinte código:
    ```php
    Route::view('/empresa', 'site/empresa');
    ```

- Exemplo de uma rota que define os tipos de acessos:
    ```php
	Route::match(['get', 'post'], '/match', function () {
        return "Permite acessos definidos";
    });
    ```
- Exemplo de uma rota GET com parâmetro com verificação se existe, caso não exista, ID padrão é 0:
    ```php
	Route::get('/produto/{id?}', function ($id = '0') {
        return 'O id é: '. $id;
    });
    ```
- Exemplo de um redirecionamento:
    ```php
    Route::redirect('/sobre', '/empresa');
    ```
- Exemplo de rota nomeada:
    ```php
    Route::view('/news', '/news')->name('noticias');

    Route::get('/novidades', function (){
        return redirect()->route('noticias');
    });
    ```
- Exemplo de grupo de rotas (também é possível agrupar por nome com `Route::name`). Seria como se as rotas dentro do escopo tivessem o *admin/* antes:
    ```php
    Route::prefix('admin')->group(function (){
        Route::get('dashboard', function () {
            return 'dashboard';
        });

        Route::get('users', function () {
            return 'users';
        });

        Route::get('clientes', function () {
            return 'clientes';
        });
    })
    ```
