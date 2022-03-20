# Configurar 2FA

### Proposta de Valor

{% hint style="info" %}
_**Como**_ um usuário registrado, _**eu quero**_ mais segurança para acessar a Plataforma  _**então**_ vou configurar o meu login de dois fatores (2FA)
{% endhint %}

### Critérios de aceite <a href="#criterios-de-aceite" id="criterios-de-aceite"></a>

* O usuário usará um aplicativo autenticador para habilitar o acesso.
* Possibilidade de ativar e desativar a autenticação de 2 fatores.
* Para habilitar ou desabilitar é necessário inserir a senha da conta.

### Screens <a href="#screens" id="screens"></a>

![](<../.gitbook/assets/My profile 2fa activate.png>) ![](<../.gitbook/assets/My profile 2fa disable.png>)

![](<../.gitbook/assets/My profile.png>) ![](<../.gitbook/assets/My profile disabled.png>)

### User Story Card  <a href="#user-story-card" id="user-story-card"></a>

**Actors:** Usuário registrado

| **Main Flow**:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p></p><ol><li>O usuário clica no ícone de usuário, o sistema exibe a tela "Meu Perfil"</li><li><p>Se usuário está com o 2FA desabilitado, sistema exibe botão para ativar o 2FA</p><ol><li><p>Usuário clica no botão para ativar o 2FA, sistema exibe o modal para ativar o <em>2FA</em></p><ol><li>O usuário faz a leitura do QRCode</li><li>Preenche o campo <em>senha</em> com sua senha atual</li><li><p>Preenche o código 2FA que exibir em seu dispositivo após a leitura do QRCode e clica em "Confirmar"</p><ol><li>Se senha incorreta, sistema exibe aviso (1)</li><li>Se código incorreto, sistema exime aviso (2)</li></ol></li><li>Sistema ativa o 2FA e exibe mensagem de sucesso (1)</li></ol></li></ol></li><li><p>Se o usuário está com o 2FA habilitado, sistema exibe botão para desabilitar o 2FA</p><ol><li><p>Usuário clica no botão para desabilitar o 2FA, sistema exibe o modal para desabilitar o <em>2FA</em></p><ol><li>Preenche o campo <em>senha</em> com sua senha atual</li><li><p>Preenche o código 2FA que exibir em seu dispositivo após a leitura do QRCode e clica em "Confirmar"</p><ol><li>Se senha incorreta, sistema exibe aviso (1)</li><li>Se código incorreto, sistema exime aviso (2)</li></ol></li></ol></li><li>Sistema desabilita o 2FA e exibe mensagem de sucesso (1)</li></ol></li><li>Fim do caso de uso</li></ol> |

**Postcondition 1:**&#x20;

Usuário consegue habilitar ou desabilitar o 2FA.

**Messages:**

* aviso (1) - Senha incorreta!
* aviso (2) - Código 2FA incorreto.
* sucesso (1) - 2FA \<habilitado || desabilitado> com sucesso!

### Scenarios <a href="#scenarios" id="scenarios"></a>

```
@habilitar-2FA
Feature: habilitar o 2FA
    Visto que preciso de mais segurança para fazer o login
    Como um usuário regsitrado eu quero habilitar meu 2FA
 
    Background: acessar a configuração do 2FA
        Dado que visito a página do "painel grafico logado"
        E clico no icone de usuário
        E visito a página "Meu perfil"    
        E e seleciono o item "Enable 2FA"

        Scenario: Habilitar com código 2FA incorreto
            Quando vejo o modal "habilitar-2fa"
            E faço a leitura do <qr-code> da página
            E digito minha <senha> correta
            E digito o <code> 2FA incorreto
            Então vejo uma <mensagem> de alerta "Código 2FA incorreto!"
 
        Scenario: Habilitar com a senha incorreta
            Quando vejo o modal "habilitar-2fa"
            E faço a leitura do <qr-code> da página
            E digito minha <senha> incorreta
            E digito o <code> 2FA correto
            Então vejo uma <mensagem> de alerta "Senha incorreta!"
 
        Scenario: habilitar 2FA
            Quando vejo o modal "habilitar-2fa"
            E faço a leitura do <qr-code> da página
            E digito minha <senha> correta
            E digito o <code> 2FA correto
            Então vejo uma <mensagem> de sucesso "2FA habilitado!"
 
@disable_2FA
Feature: disable_2FA
    Visto que preciso desabilitar o meu login com 2FA
    Como um usuário registrado quero configurar o meu 2FA
 
    Background: acessar a configuração do 2FA
        Dado que visito a página do "painel grafico logado"
        E clico no icone de usuário
        E visito a página "Meu perfil"    
        E meu usuário está com 2FA <habilitado>
        E e seleciono o item "Disable 2FA"
 
        Scenario: Desabilitar com o código incorreto
            Quando visito o modal "desabilitar-2fa"
            E digito minha <senha> correta
            E digito o <code> 2FA incorreto
            Então vejo uma <mensagem> de alerta "Código 2FA incorreto!"
 
        Scenario: Desabilitar com a senha incorreta
            Quando visito o modal "desabilitar-2fa"
            E digito minha <senha> incorreta
            E digito o <code> 2FA correto
            Então vejo uma <mensagem> de alerta "Senha incorreta!"

        Scenario: Desabilitar o 2FA
            Quando visito o modal "desabilitar-2fa"
            E digito minha <senha> correta
            E digito o <code> 2FA correto
            Então vejo uma <mensagem> de sucesso "2FA desabilitado!"
```
