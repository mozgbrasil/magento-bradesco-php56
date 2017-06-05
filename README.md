[checkmark]: https://raw.githubusercontent.com/mozgbrasil/mozgbrasil.github.io/master/assets/images/logos/logo_32_32.png "MOZG"
![valid XHTML][checkmark]

[url-method]: http://www.bradesco.com.br/
[requerimentos]: http://mozgbrasil.github.io/requerimentos/
[contact-bradesco]: http://www.bradesco.com.br/bradesco/ecp/comunidade.do?app=portal&pg=20004&view=faleconosco
[tickets]: https://cerebrum.freshdesk.com/support/tickets/new
[preco]: http://www.cerebrum.com.br/preco/
[getcomposer]: https://getcomposer.org/
[uninstall-mods]: https://getcomposer.org/doc/03-cli.md#remove

# Mozg\Bradesco

## Sinopse

Integração ao [Bradesco][url-method]

## Demonstração

<a href="http://mozg.com.br/assets/images/docs/2017-03-20-magento-bradesco.pdf" target="_blank"><img src="http://mozg.com.br/assets/images/docs/2017-03-20-magento-bradesco.gif" /></a>

## Motivação

Atender o mercado de módulos para Magento oferecendo melhorias e um excelente suporte

## Suporte / Dúvidas

Para obter o devido suporte [Clique aqui][tickets], relatando o motivo da ocorrência o mais detalhado possível e anexe o print da tela para nosso entendimento

## Preço

[Clique aqui][preco]

## Quais os recursos do módulo

- [✓] Boleto
- [✓] Transferência Eletrônica
- [✓] Consulta

## Característica técnica

No checkout é feito o processo de autorização

Na página de sucesso é exibido a janela que acessa o tipo de pagamento

Via CRON deve ser processado a notificação da transação, caso o pagamento seja confirmado, deve ser alterado o status do pedido para "Completo", liberando as ações para processar a fatura e o envio

 Antes do envio da mercadoria, sempre confira as informações do pedido, se o status da transação está sendo exibido que o pagamento foi confirmado, inclusive junto a operadora financeira se a transação foi capturada, caso algo esteja inconsistente será necessário cancelar o pedido até a correção da ocorrência

## Setup Cron

Para o uso do método é necessário ativar a <a href="https://pt.wikipedia.org/wiki/Crontab">CRON</a> para o <a href="https://magento.com/">Magento</a>

<a href="https://mozg.com.br/dicas/dicas-magento1#como-ativar-a-cron-no-magento">Clique aqui</a> para visualizar o documento da MOZG

Certifique-se de que ação esteja sendo executado a cada minuto

Esse módulo usa o cronjob para processar as notificações

O módulo executa as notificações que foram recebidas há pelo menos 5 minutos. 

## Instalação - Atualização - Desinstalação - Desativação

Este módulo destina-se a ser instalado usando o [Composer][getcomposer]

Antes de executar os processos, [clique aqui][requerimentos] e leia os pré-requisitos e sugestões

--

Certique se da existencia do arquivo composer.json na raiz do projeto Magento e que o mesmo tenha os trechos "minimum-stability", "prefer-stable", "repositories" e '"magento-root-dir":"./"', conforme https://gist.github.com/mozgbrasil/0c9bb8792ea6273ea24aed30b0fbcfba

Caso não exista o arquivo composer.json na raiz do projeto Magento, efetue o download

        wget https://gist.githubusercontent.com/mozgbrasil/0c9bb8792ea6273ea24aed30b0fbcfba/raw/9b514bc896171b6d75833b6f165065356f62ca59/composer.json

--

Para qualquer atualização no Magento sempre mantenha o Compiler e o Cache desativado

--

### Para instalar o módulo execute o comando a seguir no terminal do seu servidor no diretório do seu projeto

        composer require mozgbrasil/magento-bradesco-php56:dev-master

Você pode verificar se o módulo está instalado, indo ao backend em:

        STORES -> Configuration -> ADVANCED/Advanced -> Disable Modules Output

--

### Para atualizar o módulo execute o comando a seguir no terminal do seu servidor no diretório do seu projeto

Antes de efetuar qualquer processo que envolva atualização no Magento é recomendado manter o Compiler e Cache desativado

        composer clear-cache && composer update

Na ocorrência de erro, renomeie a pasta /vendor/mozgbrasil e execute novamente

Para checar a data do módulo execute o seguinte comando

        grep -ri --include=*.json 'time": "' ./vendor/mozgbrasil

--

### Para [desinstalar][uninstall-mods] o módulo execute o comando a seguir no terminal do seu servidor no diretório do seu projeto

        composer remove mozgbrasil/magento-bradesco-php56 && composer clear-cache && composer update

--

### Para desativar o módulo

Renomeie a pasta do módulo

Cada módulo tem a sua pasta no diretório /vendor/mozgbrasil/

## Como configurar o método de pagamento

Para configurar o método de pagamento, acesse no backend em:

        STORES -> Configuration -> Sales/Payment Methods -> Bradesco (powered by MOZG)

Você terá os campos a seguir

### Bradesco Meios de Pagamentos - Configurações Padrão

#### Configurações necessárias

##### • **Modo Teste ou Produção**

Deve ser informado o devido ambiente

##### • **Merchant ID ou "MID" para o ambiente de teste**

Ao se logar em

https://homolog.meiosdepagamentobradesco.com.br/gerenciadorapi/login.jsp

Na parte superior direita temos essa informação como MID

##### • **Merchant Key ou "Chave de Segurança" Ambiente de teste**

Em

https://homolog.meiosdepagamentobradesco.com.br/gerenciadorapi/meiopagamento/form

É possivel gerar a chave de segurança caso não tenha definido

##### • **Merchant ID para o ambiente de produção**

A informação deve ser fornecido pelo Bradesco

##### • **Merchant Key Ambiente de produção**

A informação deve ser fornecido pelo Bradesco

#### Avançado: Processamento de Pedidos Magento

##### • **Status do pedido: ordem de criação**

Status dos pedidos recém-criados, antes da confirmação de resultado de pagamento via notificações de servidor da operadora

##### • **Status do pedido: autorização de pagamento**

Status dos pedidos após autorização confirmada por uma notificação de AUTORIZAÇÃO da operadora

##### • **Status do pedido: pagamento confirmado**

Status dos pedidos após captura confirmada por uma notificação de AUTORIZAÇÃO da operadora

##### • **Status do pedido: cancelamento de pedido**

Status dos pedidos após cancelamento confirmada por uma notificação de CANCELAMENTO da operadora

Se as encomendas já estiverem faturadas, não poderão ser canceladas

##### • **Status do pedido: captura de pagamento (produtos virtuais)**

Selecione somente o status atribuído ao estado concluído, deixe vazio para usar o mesmo que os produtos normais

##### • **Status do pedido: Reembolsado**

Status dos pedidos após reembolso confirmada por uma notificação de REEMBOLSO da operadora

##### • **Status do pedido: Reembolsado Parcial**

Status dos pedidos após reembolso (parcial) confirmada por uma notificação de REEMBOLSO_PARCIAL da operadora. Recomendamos que não defina este status e deixe Magento decidir o status.

##### • **Status do pedido: pedidos pendentes**

Status dos pedidos após notificação de PENDENCIA da operadora

##### • **Tipo de Captura**

Imediato é o padrão

Defina como manual se você quiser executar a captura de fundos manualmente mais tarde

##### • **Criar uma fatura pendente (apenas para captura manual)**

Isso criará uma fatura pendente se a notificação de AUTORIZAÇÃO for recebida.

 Nota: isto fará com que Magento empurre todas as encomendas para o estado: 'Processamento' uma vez que a factura é criada, ignorando todas as outras definições.

##### • **Status do pedido: Capturar no embarque**

Se você habilitar esta função será feito uma solicitação de captura para a operadora se você fizer o envio

##### • **Ativar Descancelar pedido**

Se uma pedido é cancelada por algum motivo, mas recebeu uma notificação de que o pagamento é autorizado, isso cancelará automaticamente o pedido

##### • **Cancelamento\Reembolso automático quando o pedido é cancelado**

Ativar / Desativar reembolso automático ao cancelar um pedido

##### • **E-mail da fatura**

Ativar / desativar atualizações de e-mails

##### • **Receber e-mail de atualização do status do pedido**

Ativar / desativar e-mails de atualização para todas as alterações no status do pedido para o cliente

##### • **Ativar log de depuração**

Deve ser armazenado os processos do módulo em var/log/

O arquivo 

DATE_mozg.log

se trata de log do módulo sendo um log mais detalhado contendo todos os processos inclusive das execuções realizadas pelas bibliotecas externas do módulo

O arquivo

payment_METHOD.log

#### Avançado: Bradesco Notificações

##### • **Ignorar notificação de reembolso**

Se o reembolso for feito na operadora, e a mesma enviar uma notificação de reembolso para o Magento, deve ser criado automaticamente uma nota de crédito. Se você definir essa configuração como 'Sim', isso não acontecerá porque ele não processará nenhuma das notificações de REEMBOLSO recebidas.

<!--
#### Avançado: Contratos de faturamento

##### • **Tipo de Contrato**

Quando ativado, os usuários podem salvar seus cartões de crédito e suas autorizações 

ONECLICK exigirá a entrada do CVC para pagamentos subsequentes, enquanto RECURRING não.
-->

#### Avançao: Experiência de Checkout

##### • **Redirecionar o destino após o cancelamento**

Determina como os compradores são redirecionados após cancelar um pagamento.

##### • **Método de pagamento método de renderização**

Determina se os métodos de pagamento serão exibidos com seu logotipo ou apenas o nome.

##### • **Idioma local (opcional)**

Isso substituirá o local do cliente padrão do armazenamento do Magento. 

Deixe vazio para deixar Magento decidir (Ex: nl_NL)

##### • **Código do país ISO (opcional)**

Isso irá substituir o país do endereço de faturamento do comprador ao determinar quais métodos de pagamento serão exibidos.

### Boleto Bradesco

#### • **Ativar**

Para "ativar" ou "desativar" o uso do método

#### • **Ordem de exibição**

É a ordem apresentada em métodos de entrega no passo de fechamento de pedido

#### • **Título**

Nome do método que deve ser exibido

#### • **Pagamentos aplicáveis aos países**

Você pode definir se o método deve funcionar para "Todos os Países aceito" ou "Especificar Países "

#### • **Pagamentos específicos aos países**

Você deve selecionar os países que o método deve ser funcional

#### • **Nome do beneficiário/cedente**

Nome do beneficiário/cedente

#### • **Carteira**

Carteira

#### • **Vencimento**

Vencimento

#### • **Logo**

Logo

O tamanho da imagem deve ser de 120px largura por 80px de altura

#### • **Mensagem de cabeçalho exibida no topo do boleto**

Mensagem de cabeçalho exibida no topo do boleto

#### • **Instruções (máximo de três linhas)**

Instruções (máximo de três linhas)

#### • **Status do pedido não pago**

Com Boleto é possível pagar menos do que o valor total. Selecione aqui o status, se este for o caso. Se você deixar isso em branco, ele tomará o status de pedido de pagamento autorizado como status padrão

#### • **Status do pedido pago em excesso**

Com Boleto é possível pagar mais do que o valor total. Selecione aqui o status, se este for o caso. Se você deixar isso em branco, ele tomará o status de pedido de pagamento autorizado como status padrão

#### • **Visível em**

Determine a visibilidade desse método de pagamento no frontend e/ou backend do Magento

### Transferência Eletrônica Bradesco

#### • **Ativar**

Para "ativar" ou "desativar" o uso do método

#### • **Ordem de exibição**

É a ordem apresentada em métodos de entrega no passo de fechamento de pedido

#### • **Título**

Nome do método que deve ser exibido

#### • **Pagamentos aplicáveis aos países**

Você pode definir se o método deve funcionar para "Todos os Países aceito" ou "Especificar Países "

#### • **Pagamentos específicos aos países**

Você deve selecionar os países que o método deve ser funcional

#### • **Tipos de Transferência Eletrônica**

Selecione as bandeiras liberadas pela operadora

#### • **Status do pedido não pago**

Com Boleto é possível pagar menos do que o valor total. Selecione aqui o status, se este for o caso. Se você deixar isso em branco, ele tomará o status de pedido de pagamento autorizado como status padrão

#### • **Status do pedido pago em excesso**

Com Boleto é possível pagar mais do que o valor total. Selecione aqui o status, se este for o caso. Se você deixar isso em branco, ele tomará o status de pedido de pagamento autorizado como status padrão

#### • **Visível em**

Determine a visibilidade desse método de pagamento no frontend e/ou backend do Magento

## Perguntas mais frequentes "FAQ"

#### Como é criado o cabeçalho de autorização para a transação

Abaixo temos uma transação com o seguinte cabeçalho de autorização

        --header 'Authorization: Basic MTAwMDA2ODczOm1WeWFuZzZpZm9GNjNkMWE1UFFqd25GQ3ZrWDM0bV9ZMWVQREpjQms3clE='

Que equivale ao recurso "base64_encode(merchantId:chaveSeguranca)"

Podemos usar o seguinte serviço para codificar a informação

Acesse

https://www.base64encode.org/ 

e informe

seu_merchantId:sua_chaveSeguranca

No meu caso é os dados a seguir

"100006873:mVyang6ifoF63d1a5PQjwnFCvkX34m_Y1ePDJcBk7rQ"

#### Simulação de transação para boleto

    curl --request POST "https://homolog.meiosdepagamentobradesco.com.br/apiboleto/transacao" --header 'Content-Type: application/json' --header 'Authorization: Basic MTAwMDA2ODczOm1WeWFuZzZpZm9GNjNkMWE1UFFqd25GQ3ZrWDM0bV9ZMWVQREpjQms3clE=' --data '{
       "merchant_id":"100006873",
       "meio_pagamento":"300",
       "pedido":{
          "numero":"145000639",
          "valor":10000,
          "descricao":"Compra pelo site http://127.0.0.1/public_html/magento-1.9.3.1-dev34/root/"
       },
       "comprador":{
          "nome":"Eula Jackson",
          "documento":"25739569000102",
          "endereco":{
             "cep":"08215070",
             "logradouro":"Avenida Córrego do Jacuu",
             "numero":"12",
             "complemento":"ap. 23 B",
             "bairro":"Itaquera",
             "cidade":"São Paulo",
             "uf":"CE"
          },
          "ip":"127.0.0.1",
          "user_agent":"Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:53.0) Gecko/20100101 Firefox/53.0"
       },
       "boleto":{
          "beneficiario":"ACME (American Company Makes Everything)",
          "carteira":"25",
          "nosso_numero":"145000639",
          "data_emissao":"2017-05-25",
          "data_vencimento":"2017-06-01",
          "valor_titulo":10000,
          "url_logotipo":"",
          "mensagem_cabecalho":"mensagem de cabecalho",
          "tipo_renderizacao":"2",
          "instrucoes":{
             "instrucao_linha_1":"- instrucao_linha_1",
             "instrucao_linha_2":"- instrucao_linha_2",
             "instrucao_linha_3":"- instrucao_linha_3"
          },
          "registro":null
       },
       "token_request_confirmacao_pagamento":"a784f7b1e854b967da7fc2e2bc91ef2465712196"
    }' --verbose

#### Simulação de transação para transferência eletrônica *** que parou de funcionar, em contato com o Bradesco

    curl --request POST "https://homolog.meiosdepagamentobradesco.com.br/transf/transacao" --header 'Content-Type: application/json' --header 'Authorization: Basic MTAwMDA2ODczOm1WeWFuZzZpZm9GNjNkMWE1UFFqd25GQ3ZrWDM0bV9ZMWVQREpjQms3clE=' --data '{
       "merchant_id":"100006873",
       "meio_pagamento":"800",
       "pedido":{
          "numero":"145000641",
          "valor":10000,
          "descricao":"Compra pelo site http://127.0.0.1/public_html/magento-1.9.3.1-dev34/root/"
       },
       "comprador":{
          "nome":"Eula Jackson",
          "documento":"25739569000102",
          "endereco":{
             "cep":"08215070",
             "logradouro":"Avenida Córrego do Jacuu",
             "numero":"12",
             "complemento":"ap. 23 B",
             "bairro":"Itaquera",
             "cidade":"São Paulo",
             "uf":"CE"
          },
          "ip":"127.0.0.1",
          "user_agent":"Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:53.0) Gecko/20100101 Firefox/53.0"
       },
       "token_request_confirmacao_pagamento":"a784f7b1e854b967da7fc2e2bc91ef2465712196"
    }' --verbose

### Sobre o retorno "Erro no tratamento da resposta do pagamento. Entre em contato com a loja" que é exibido no uso do ambiente de teste

A Scopus menciona o seguinte

Prezado (a),

Verificamos que a sua URL de Notificação está apresentando erro no Ambiente de Teste, o qual estamos verificando para lhe posicionar.

Em contrapartida a fim de agilizar e para que possa seguir para o Ambiente de Produção o qual a sua URL funcionará corretamente, disponibilizamos a URL: 

https://homolog.meiosdepagamentobradesco.com.br/lojatesteapi/

para que possa incluir no campo URL DE NOTIFICAÇÃO do gerenciador.
 
### Como configurar a URL de notificação

http://SEU_DNS/index.php/mozg_bradesco/process/notification/

### Como alterar a imagem do método

Pode ser adicionado a imagem, contendo qualquer uma das nomenclaturas a seguir

- method-boleto.png
- method-eletronictransfer.png

E adicione a imagem no diretório do seu template

/skin/frontend/<TEMPLATE>/default/images/mozg_bradesco

### Dados de contato - SCOPUS TECNOLOGIA

Sistema de Pagamento Seguro  
Suporte Técnico  
Scopus Tecnologia  
(11) 3909-3482  
(11) 3909-3637  
kit@scopus.com.br

## Manual

https://homolog.meiosdepagamentobradesco.com.br/manual/Manual_BoletoBancario.pdf
 
https://homolog.meiosdepagamentobradesco.com.br/manual/Manual_ConsultaPedidos.pdf
 
https://homolog.meiosdepagamentobradesco.com.br/manual/Manual_API_Transferencia.pdf

## Contribuintes

Equipe Mozg

## License

[Comercial License](LICENSE.txt)

## Badges

[![Join the chat at https://gitter.im/mozgbrasil](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/mozgbrasil/)
[![Latest Stable Version](https://poser.pugx.org/mozgbrasil/magento-bradesco-php56/v/stable)](https://packagist.org/packages/mozgbrasil/magento-bradesco-php56)
[![Total Downloads](https://poser.pugx.org/mozgbrasil/magento-bradesco-php56/downloads)](https://packagist.org/packages/mozgbrasil/magento-bradesco-php56)
[![Latest Unstable Version](https://poser.pugx.org/mozgbrasil/magento-bradesco-php56/v/unstable)](https://packagist.org/packages/mozgbrasil/magento-bradesco-php56)
[![License](https://poser.pugx.org/mozgbrasil/magento-bradesco-php56/license)](https://packagist.org/packages/mozgbrasil/magento-bradesco-php56)
[![Monthly Downloads](https://poser.pugx.org/mozgbrasil/magento-bradesco-php56/d/monthly)](https://packagist.org/packages/mozgbrasil/magento-bradesco-php56)
[![Daily Downloads](https://poser.pugx.org/mozgbrasil/magento-bradesco-php56/d/daily)](https://packagist.org/packages/mozgbrasil/magento-bradesco-php56)
[![Reference Status](https://www.versioneye.com/php/mozgbrasil:magento-bradesco-php56/reference_badge.svg?style=flat-square)](https://www.versioneye.com/php/mozgbrasil:magento-bradesco-php56/references)
[![Dependency Status](https://www.versioneye.com/php/mozgbrasil:magento-bradesco-php56/1.0.0/badge?style=flat-square)](https://www.versioneye.com/php/mozgbrasil:magento-bradesco-php56/1.0.0)

:cat2: