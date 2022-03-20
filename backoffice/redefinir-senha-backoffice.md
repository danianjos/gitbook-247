# Redefinir Senha Backoffice

### Proposta de Valor

{% hint style="info" %}
_**Como**_ um usuário registrado, _**eu quero**_ alterar a minha senha de acesso na Plataforma  _**então**_ manter a segurança do meu login
{% endhint %}

### Critérios de aceite <a href="#criterios-de-aceite" id="criterios-de-aceite"></a>

* O usuário precisa inserir a senha anterior correta
* A nova senha precisa ser confirmada em outro campo de Confirmação da senha.
* A nova senha precisa seguir o padrão das demais, de 6 a 20 caracteres.
* Não permitir alterar senha com campo vazio

### Screens <a href="#screens" id="screens"></a>

![](<../.gitbook/assets/My profile.png>)



### User Story Card  <a href="#user-story-card" id="user-story-card"></a>

**Actors:** Usuário registrado

| **Main Flow**:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <ol><li><p>O usuário clica no ícone de usuário na página de "Painel Gráfico logado"</p><ol><li><p>Sistema exibe a página "Meu Perfil"</p><ol><li>Usuário preenche sua senha atual</li></ol></li><li><p>O usuário preenche a nova senha e confirma a senha.</p><ol><li>Se nova senha diferente a confirmação de senha, sistema exibe aviso (2)</li><li>Se campos vazios, sistema exibe aviso (3)</li></ol></li><li><p>Usuário clica em "Salvar"</p><ol><li>Se senha incorreta, sistema exibe aviso (1)</li></ol></li><li><p>Sistema redefine senha do usuário</p><ol><li>Exibe mensagem de sucesso (1)</li></ol></li><li>Fim do caso de uso</li></ol></li></ol> |

**Postcondition 1:**&#x20;

Usuário redefine sua senha na plataforma.

**Messages:**

* aviso (1) - Senha incorreta!
* aviso (2) - Senha precisa ser igual a confirmar senha!
* sucesso (1) - Senha alterada com sucesso!&#x20;
* aviso (3) - Nova senha é obrigatório!

### Scenarios <a href="#scenarios" id="scenarios"></a>

```
@redefinir-senha
Feature: Redefinição de senha
    Como um usuário registrado eu quero redefinir minha senha.
 
    Background: acessar redefiniçao de senha
        Dado que visito a página do "painel gráfico logado"
        E clico no ícone de usuário
 
        Scenario: redefinir senha com a senha atual incorreta
            Quando visito a pagina "Meu Perfil"
            E digito <senha-atual> incorreta
            E digito <nova-senha> válida
            E digito <confirmar-senha> igual a <nova-senha>
            E clico no botão "Salvar"
            Então vejo uma mensagem de aviso "Senha incorreta!"
 
        Scenario: redefinir senha com a senha atual correta
            Quando visito a pagina "Meu Perfil"
            E digito <senha-atual> correta
            Então digito <nova-senha> válida
            E digito <confirmar-senha> igual a <nova-senha>
            E clico no botão "Salvar"
            E vejo uma mensagem de sucesso "Senha alterada com sucesso."
 
        Scenario: redefinir senha com a confirmação de senha incorreta
            Quando visito a pagina "Meu Perfil"
            E digito <senha-atual> correta
            Então digito <nova-senha> válida
            E digito <confirmar-senha> diferente de <nova-senha>
            E clico no botão "Salvar"
            E vejo uma mensagem de aviso "Senha deve ser igual a confirmar senha."
  
      Scenario: Alterar senha com nova senha ou confirmação de senha vazios
        Quando visito a pagina "Meu Perfil"
        E digito <senha-atual> correta
        E o campo <nova-senha> está <vazio>
        E o campo <confirmar-nova-senha> está <vazio>
        Então vejo uma mensagem "Nova senha é obrigatório!"                    
            
```
