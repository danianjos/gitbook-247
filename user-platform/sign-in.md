# Sign in

### Proposta de Valor

{% hint style="info" %}
_**Como**_ um usuário cadastrado, _**eu quero**_ utilizar meu e-mail e senha ou minha conta Google e _**então**_ acessar a aplicação 24/7 Tradebots.
{% endhint %}

### Critérios de aceite <a href="#criterios-de-aceite" id="criterios-de-aceite"></a>

* O sign in só pode ser feito após cadastro do usuário.
* O usuário faz o sign in com E-mail e senha cadastradas
* Não é permitido fazer o sign in com o campo e-mail ou password em branco.
* Incluir validação para e-mail válido.
* Incluir opção de sign in with Google (integração).
* Usuário com 2FA ativado solicita o código de validação no sign in.
* A tela de sign in deve existir rota para sign up e redefinir senha.

### Draft Screens <a href="#screens" id="screens"></a>

![](<../.gitbook/assets/Sign in.png>) ![](<../.gitbook/assets/Sign in 2FA code.png>)

### User Story Card  <a href="#user-story-card" id="user-story-card"></a>

**Actors:** Usuários cadastrados na plataforma

| **Main Flow**:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p></p><ol><li><p>Acessar a plataforma, exibe a tela “Painel Gráfico“, usuário clica no botão "Sign in"</p><ol><li>Sistema redireciona para a tela de "sign in"</li></ol></li><li><p>Rotas de acesso do usuário</p><ol><li>Se usuário clicar no link "Sing up", sistema redireciona para cadastro do usuário.</li><li>Se usuário clicar no link "Esqueci a senha", sistema redireciona para recuperação de senha.</li></ol></li><li><p>Sign in na aplicação usando e-mail e senha</p><ol><li><p>Preenche o campo <em><strong>e-mail</strong></em> com o e-mail cadastrado</p><ol><li>Se e-mail inválido, exibe mensagem de alerta (1)</li><li>Se campo e-mail vazio, exibe mensagem de alerta (5)</li></ol></li><li><p>Preenche o campo <em><strong>senha</strong></em> com a senha cadastrada</p><ol><li>Se senha inválida, exibe mensagem de alerta (2) e usuário não acessa a plataforma.</li></ol></li></ol></li><li><p>Sign in with</p><ol><li><p>Usuário clica na opção de "Entrar com Google"</p><ol><li>Sistema redireciona para Google sign in </li></ol></li><li>Usuário seleciona sua conta Google para fazer o sign in</li></ol></li><li><p>Autenticação do usuário</p><ol><li>Se e-mail não cadastro exibe mensagem de alerta (3)</li><li>Se senha incorreta, exibe mensagem de alerta (4)</li><li><p>Se e-mail e senha corretos</p><ol><li>Sistema verifica se usuário possui 2FA configurado</li><li>Se não possui, usuário acessa plataforma</li><li><p>Se sim, exibe tela solicitando código 2FA</p><ol><li>Se código inválido, sistema exibe mensagem de alerta (6)</li></ol></li><li>Usuário faz sign in na aplicação</li></ol></li></ol></li><li><p>Primeiro acesso</p><ol><li>Sistema exibe rota <em>Definir Plano,</em> usuário pode <em>definir plano</em> ou <em>definir depois</em></li><li>Sistema redireciona para "Tutorial Configurar Robô", usuário pode pular tutorial</li></ol></li><li><p>Acesso a Painel Logado</p><ol><li>Usuário cadastrado e autenticado acessa o Painel Gráfico logado.</li></ol></li><li>Fim do caso de uso</li></ol> |

**Postcondition 1:**&#x20;

* Usuário cadastrado no primeiro acesso define plano para acessar a plataforma ou escolhe definir depois.
* Usuário cadastrado no primeiro acesso visualiza o Tutorial de Configuração dos robôs ou escolhe visualizar depois.
* Usuário cadastrado acessa a plataforma.

**Messages:**

* aviso (1) - E-mail inválido!
* alerta (2) - Senha inválida!
* alerta (3) - Usuário não cadastrado!
* alerta (4) - E-mail ou senha incorreta!
* alerta (5) - E-mail é obrigatório!
* alerta (6) -Código inválido!

### Scenarios <a href="#scenarios" id="scenarios"></a>

```
@signin
Feature: Sign in na plataforma
    Como um usuário registrado quero fazer o meu login 
        na plataforma 24/7 Tradebots usando o meu e-mail e senha.

Scenario: Sign in com usuário não cadastrado
    Dado que visito a tela de "signin"
    E sou um usuário não cadastrado
    Quando preencho o campo <email> com um valor válido
    E preencho campo <senha> com um valor válido
    E clico no botão "Entrar"
    Então vejo uma mensagem de alerta "Você não possui cadastro."

Scenario: Sign in com e-mail inválido
    Dado que visito a tela de "signin"
    Quando preencho o campo <email> com um valor inválido
    Então vejo uma mensagem de alerta "E-mail é inválido"

Scenario: Sign in com e-mail vazio
    Dado que visito a tela de "signin"
    Quando deixo o campo <email> vazio
    E seleciono o campo <senha>
    Então vejo uma mensagem de alerta "E-mail é obigatório"

Scenario: Sign in com senha inválida
    Dado que visito a tela de "signin"
    E sou um usuário não cadastrado
    Quando preencho o campo <email> com um valor válido
    E preencho campo <senha> com um valor inválido
    E clico no botão "Entrar"
    Então vejo uma mensagem de alerta "Senha inválida."

Scenario: Sign in com senha vazia
    Dado que visito a tela de "signin"
    Quando deixo o campo <senha> vazio
    E o campo <email> com valor válido
    Então vejo uma mensagem de alerta "Senha é obrigatório."

Scenario: Sign in com senha vazia e email vazio
    Dado que visito a tela de "signin"
    Quando deixo o campo <senha> vazio
    E o campo <email> vazio
    E clico no botão "Entrar"    
    Então vejo as mensagens de alerta "Senha é obrigatório." e "E-mail é obrigatório."   
```

```
@2FA_signin
Feature: Signin com 2FA
    Como um usuário registrado e com o 2FA configurado 
    eu quero logar na plataforma com mais segurança usando o código 2FA.

Background: Signin com senha e usuário corretos e válidos
    Dado que visito a tela de "Signin"
    E preencho o campo <email> com valor válido
    E preencho o campo  <senha> com valor válido
    E visito a tela "code-2fa"

Scenario: Login com código 2FA inválido
    Quando digito o <2fa-code> inválido
    E clico no botão "Verify"
    Então vejo uma mensagem "Código é inválido."

Scenario: Login com código 2FA vazio
    Quando deixo o campo <2fa-code> vazio
    E clico no botão "Verify"
    Então vejo uma mensagem "Código é obigatório."
```
