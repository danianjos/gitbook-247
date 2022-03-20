# Sign up Backoffice

### Proposta de Valor

{% hint style="info" %}
_**Como**_ um novo usuário, _**eu quero**_ criar minha conta na Plataforma 24/7 Tradebots e _**então**_ definir meus Tradebots.
{% endhint %}

### Critérios de aceite <a href="#criterios-de-aceite" id="criterios-de-aceite"></a>

* O usuário deve informar os campos:
  * Nome
  * E-mail
* A senha deve ser forte:
  * Caracteres alfabéticos maiúsculos e minúsculos
  * Números
  * Caracteres especiais
  * Mínimo de 7 caracteres
* O usuário deve aceitar os termos de uso e política de privacidade da 24/7 Tradebots
* O sistema deve enviar um e-mail com um código de 5 dígitos para o usuário confirmar o cadastro e criar a senha de acesso.
* Após a confirmação do cadastro e criação da senha, o acesso é liberado para o usuário.
* Possibilitar o reenvio do código

### Screens <a href="#screens" id="screens"></a>

![](<../.gitbook/assets/Sign up.png>)

![](<../.gitbook/assets/Sign up - Verify account.png>) ![](<../.gitbook/assets/Sign up - Verify account success.png>)

### User Story Card  <a href="#user-story-card" id="user-story-card"></a>

**Actors:** Usuário

| **Main Flow**:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p></p><ol><li><p>Acessar a plataforma, exibe a tela “Painel Gráfico“, usuário clica no botão "Sign up"</p><ol><li>Sistema redireciona para a tela de "sign up"</li></ol></li><li><p>Rotas de acesso do usuário</p><ol><li>Se usuário clicar no link "Terms &#x26; Conditions", sistema exibe modal com as regras.</li><li>Se usuário clicar no link "Sign in", sistema redireciona para tela de 'sign in'.</li></ol></li><li><p>Sign up na aplicação usando e-mail e senha</p><ol><li><p>Preenche o campo <em><strong>nome</strong></em></p><ol><li>Se campo nome vazio, exibe mensagem de alerta (2).</li></ol></li><li><p>Preenche o campo <em><strong>e-mail</strong></em> com o e-mail</p><ol><li>Se e-mail inválido, exibe mensagem de alerta (1)</li><li>Se campo e-mail vazio, exibe mensagem de alerta (3)</li></ol></li><li><p>Usuário clica no botão "Sign up"</p><ol><li>Sistema envia código de ativação da conta para e-mail do usuário</li><li>Sistema exibe a tela de "Verificar conta"</li></ol></li></ol></li><li><p>Sign up with</p><ol><li><p>Usuário clica na opção de "Sign up with Google"</p><ol><li>Sistema redireciona para Google sign up</li></ol></li><li>Usuário seleciona sua conta Google para fazer o sign up</li></ol></li><li><p>Ativação da conta</p><ol><li>Usuário digita <em><strong>código de ativação</strong></em> </li><li><p>Usuário digita uma <em><strong>senha</strong></em></p><ol><li>Se senha inválida, exibe mensagem de alerta (4)</li><li>Se campo senha vazio, exibe mensagem de alerta (5)</li></ol></li><li><p>Usuário digita <em><strong>confirmação da senha</strong></em></p><ol><li>Se campo confirme senha diferente de campo senha, exibe mensagem de alerta (6)</li></ol></li><li><p>Usuário clica em "Verify"</p><ol><li>Se <em><strong>código de ativação</strong></em> inválido, exibe mensagem de alerta (7)</li></ol></li></ol></li><li>Fim do caso de uso</li></ol> |

**Postcondition 1:**&#x20;

Usuário cria a conta e ativa a conta para acessar a 24/7 Plataforma

**Messages:**

* aviso (1) - E-mail inválido!
* alerta (2) - Nome é obrigatório
* alerta (3) - E-mail é obrigatório!
* alerta (4) - Senha deve conter 7 caracteres, uma letra maiúscula e um caractere especial!
* alerta (5) - Senha é obrigatório!
* alerta (6) - Campo confirmar senha deve ser igual a senha!
* alerta (7) - Código inválido!

### Scenarios <a href="#scenarios" id="scenarios"></a>

```
@Signup com email
Feature: Criar conta com o email
    Como um usuário quero criar uma conta para usar 
    o 24/7 Tradebots utilizando o meu email.

    Scenario: criar conta com nome vazio
        Dado que visito a tela de "signup"
        E o campo "Nome" permanece vazio
        Quando clico em outro campo
        Então o botão "Sign up" fica desabilitado
        E vejo uma mensagem de alerta "Nome é obigatório."

    Scenario: criar conta com email vazio
        Dado que visito a tela de "signup"
        E o campo "E-mail" permanece vazio
        Quando clico em outro campo
        Então o botão "Sign up" fica desabilitado
        E vejo uma mensagem de alerta "E-mail é obigatório."       

    Scenario: criar conta com email inválido
        Dado visito a tela "signup"
        Quando preencho o campo "E-mail" com <email> inválido
        Então vejo uma mensagem de alerta "E-mail é inválido."
        E o botão "Sign up" fica desabilitado 
        
    Scenario: criar conta com email
        Dado visito a tela "signup"
        E preencho o campo "Name" com <name>
        E preencho o campo "E-mail" com <email> válido
        Quando clico no botão "Sign up"
        Então vejo uma mensagem de sucesso "Você recebeu um e-mail com código de validação"
        E o sistema redireciona para a página "signup-validate"
        
@Ativação_conta
Feature: Ativar e validar a conta do usuário
    Como um usuário quero receber um código para ativar e validar 
    o meu cadastro e assim garantir segurança.
    
    Scenario: confirmar a conta com código vazio
        Dado que visito a tela "signup-validate"
        E o campo "Code" permanece vazio
        Quando clico em outro campo <campo>
        Então o botão "Verify" fica desabilitado 
        E vejo uma mensasem de alerta "Código é obrigatório."

    Scenario: confirmar a conta com código inválido
         Dado que visito a tela "signup-validate"
         E preencho o campo "Code" com <codigo> inválido
         Quando clico em outro campo <campo>
         Então o botão "Verify" fica desabilitado 
         E vejo uma mensasem de alerta "Código é inválido."
         
    Scenario: confirmar a conta com campo senha vazio
        Dado que visito a tela "signup-validate"
        E o campo "Password" permanece vazio
        Quando clico em outro campo <campo>
        Então o botão "Verify" fica desabilitado 
        E vejo uma mensasem de alerta "Senha é obrigatório."
        
      Scenario: confirmar a conta com campo senha inválido
        Dado que visito a tela "signup-validate"
        Quando preencho o campo "Code" com o valor <code> inválido
        Então vejo uma mensasem <mensagem> de alerta para cada parâmetro válidos do password <alerta-parametro>
        E o botão "Verify" fica desabilitado 
            Exemplo:
            | mensagem                              | alerta-parametro                       |
            | Senha deve ter no mínimo 7 caracteres | quantidade caracteres abaixo do limite |
            | Senha deve ter 1 caractere especial   | verificar se possui caracter especial  |
            | Senha seve ter numeros e texto        | verificar se alfanumérico              |   

    Scenario: confirmar a conta com campo confirmar senha vazio
         Dado que visito a tela "signup-validate"
         E o campo "Confirm Password" permanece vazio
         Quando clico em outro campo <campo>
         Então o botão "Verify" fica desabilitado 
         E vejo uma mensasem de alerta "Confirmar senha é obrigatório."  
         
    Scenario: confirmar a conta com campo senha e confirmar senha diferentes
         Dado que visito a tela "signup-validate"
         E preencho o campo "Code" com <codigo> válido
         E preencho o campo "Password" com <password> válido
         Quando preencho o campo "Confirm Password" com valor <confirm-password> diferente de <password>
         Então o botão "Verify" fica desabilitado 
         E vejo uma mensasem de alerta "Senha e Confirmar senha devem ser iguais."                        
```

