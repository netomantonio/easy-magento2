<p align="center">
    <img src="https://static.magento.com/sites/all/themes/magento/logo.svg" width="300px" alt="Magento Commerce" />
</p>

##  MAGENTO 2 - EASY DOCKER DEVELOPMENT

o projeto atual é baseado no projeto [echo-magento/docker-magento2](https://github.com/echo-magento/docker-magento2.git) e foi ajustado para funcionar com a versão 8.1 do PHP.

<details>
    <summary> <b>English:</b> </summary>
    The current project is based on the <a href="https://github.com/echo-magento/docker-magento2.git">echo-magento/docker-magento2</a> repository and has been adjusted to work with PHP version 8.1.
</details>
<details>
    <summary> <b>Spanish:</b> </summary>
    El proyecto actual se basa en el repositorio <a href="https://github.com/echo-magento/docker-magento2.git">echo-magento/docker-magento2</a> y ha sido ajustado para funcionar con la versión 8.1 de PHP.
</details>

### Características

- Magento 2.4.4
- Apache
- PHP 8.1
- Xdebug 3.2.2
- MariaDB 10.4.13
- Elasticsearch 7.6
- Varnish 6.4
- Redis
- ~~MailHog~~
- n98-magerun

| PHP Version  | Composer  | [Prestissimo](https://github.com/hirak/prestissimo) |
|---|---|---|
|8.1|2.6.5|Yes|

### Requisitos

**Linux:**

Instalar [Docker](https://docs.docker.com/engine/install/) e [Docker compose](https://docs.docker.com/compose/install/linux/#install-using-the-repository).


### Antes de começar
> <cite>Observe que para o Elasticsearch você precisa de pelo menos 262.144 memória.</cite> 

Checar:
> more /proc/sys/vm/max_map_count

A vm.max_map_count configuração deve ser definida permanentemente em `/etc/sysctl.conf`:

> vm.max_map_count=262144

Depois de definir, execute:

> sudo sysctl -p

Agora é necessário adicionar as informações de autenticação do repositório do magento 2, para isso
execute:
___
<details id="credenciais-section">
    <summary> <b>PEGAR CREDENCIAIS</b> </summary>
    <h6> Criar conta: </h6>
    Pode ser usado o email profissional (recomendado) para criar uma conta magento, basta acessar o link abaixo e seguir os passos no site clicando em <i><b>Sign in with Adobe ID</b></i> e depois em <i><b>Crie uma conta</b></i>:
    <br>
    Criar uma conta Magento -> <a href="https://account.magento.com/customer/account/login">Magento Account</a>
    <br>
    <h6> Criar chaves de acesso: </h6>
    Para criar uma chave de acesso clique no botão <i><b>Create A New Access Key</b></i> de um nome para o par de chaves que será criado e depois clique em <i><b>OK</b></i> e poderá copiar as chaves de acesso e substituir no passo seguinte:
    <br>
    Criar uma chave de acesso -> <a href="https://commercemarketplace.adobe.com/customer/accessKeys/">Access Keys</a>

</details>

_____ 

<cite><sub>**Não Esqueça de subistituir as credenciais da sua conta adobe**</sup></cite>
Para isso caso ainda não saiba ou não tenha use <a href="#credenciais-section">PEGAR CREDENCIAIS</a>

>```
> echo '{"http-basic":{"repo.magento.com":{"username":"<your_public_key>","password":"<your_private_key>"}}}' > ~/.composer/auth.js


Agora execute o comando abaixo para que possa permitir a escrita por parte do container que compartilha a pasta ~/.composer do host



### Como usar
Execute todos os containers com o comando abaixo

>```
>bin/start


Para instalar o magento 2 na versão de compatibilidade execute os comandos abaixo:

>```shell
> bin/shell
> rm index.php
> install-magento2 2.4.4

Se quiser usar o Varnish use o `docker-compose.varnish.yml`
Se você não quiser usar Varnish e Elasticsearch use `docker-compose.light.yml`

### Painéis

**Web server:** http://localhost/

~~**Local emails:** http://localhost:8025~~

### Comandos de recursos

| Comandos  | Descrição  | Opções & exemplos |
|---|---|---|
| `bin/init`  | Se você não usou o comando de configuração CURL acima, use este comando alterando o nome do projeto.  | `./init MYMAGENTO2` |
| `bin/start`  | Se você continuar sem usar o CURL, poderá iniciar seu contêiner manualmente  | |
| `bin/stop`  | Pare os contêineres do seu projeto  | |
| `bin/kill`  | Interrompe contêineres e remove contêineres, redes, volumes e imagens criadas para o projeto específico  | |
| `bin/shell`  | Acesse seu contêiner  | `./shell root` | |
| `bin/magento`  | Use o poder do Magento CLI  | |
| `bin/magento-basic`  | Todos os comandos básicos do Magento CLI (setup:upgrade, setup:di:compile, setup:static-content:deploy -f, cache:clean, cache:flush)  | |
| `bin/n98`  | Use os comandos Magerun como quiser | |
| `bin/grunt-init`  | Prepare-se para usar o Grunt  | |
| `bin/grunt`  | Use o Grunt especificamente no seu tema ou completamente, ele fará o deploy e o watcher.  | `./grunt luma` |
| `bin/xdebug`  |  Habilitar/Desabilitar o XDebug | |
| `bin/composer`  |  Usar comandos do Composer | `./composer update` |
