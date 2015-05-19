Informações de Conexão
----------------------

Tecnologia usada: ``Socket``.

Troca de mensagens no formato JSON. Ex:

.. code-block:: javascript

    {"tipo":"ACAO","comando":"DISCAR","numeroDiscado":"099123456","agente":"12","messageId":"1"}

As mensagens são em uma linha, com uma quebra de linha ao final.

Porta de conexão configurável pelo sistema Catix, verificar com o suporte da Catelani caso precise trocar a porta ou usar uma especifica. O procedimento é rápido.

A quantidade de conexões que o sistema suporta varia de acordo com o hardware do servidor.

A comunicação ocorre na forma de troca de mensagens do tipo ``Comando`` e ``Eventos``. Os comandos são enviados pelo cliente ao servidor para executar uma ação e responde o cliente na forma de uma ``Notificação``, e os eventos são enviados do servidor para os clientes de acordo com o que está acontecendo, e não precisam de uma ação para serem enviados.

A integração suporta basicamente dois formatos de comunicação: um em que apenas uma conexão é aberta para o servidor, e todas as mensagens são enviadas com as identificações dos agentes - ideal para aplicações webs, chamada de ``LOGIN_MULTI_USER``; e outra que é uma conexão por agente, onde o agente se identifica no momento de conectar e não é necessário enviar a identificação nos comandos após o login - ideal para aplicações desktop, chamada de ``LOGIN_SINGLE_USER``.Ver mais informações na lista de comandos nas opções de login.


Formato das mensagens
---------------------

.. code-block:: javascript

    {
	 "tipo": "ACAO",
	  "comando": "LOGAR_SINGLE_USER",
	  "agente": "12",
	  "numeroDiscado": "12345678",
	  "informacao": "OK",
	  "destino": "1",
	  "idDestino": "",
	  "erroCod": "",
	  "atributos": {
	    "usuario": "zupao",
	    "senha": "123456"
	  },
	 "messageId": "1"
    }

.. attention:: Os campos são requeridos ou não, dependendo da ação que estiver sendo executada, consule a lista de ações para verificar.

Descrição dos campos
""""""""""""""""""""

+---------------+--------------------------------------------------------------------------------------------------------------------------+
| Campo         | Descrição                                                                                                                |
+===============+==========================================================================================================================+
| Tipo          | Tipo da mensagem. ``ACAO``, ``NOTIFICACAO``, ``ERRO``, ``KEEP_ALIVE`` e ``EVENT``.                                       |
+---------------+--------------------------------------------------------------------------------------------------------------------------+
| Comando       | Usado em conjunto com o tipo ACAO, descreve a ação a ser executado.                                                      |
+---------------+--------------------------------------------------------------------------------------------------------------------------+
| Agente        | Usado no modo ``MULTI_LOGIN`` para informar a qual usuário a ação deve ser enviada.                                      |
+---------------+--------------------------------------------------------------------------------------------------------------------------+
| NumeroDiscado | Usado na ação de discar, informa o numero que deve ser discado                                                           |
+---------------+--------------------------------------------------------------------------------------------------------------------------+
| Informacao    | Mostra informações variadas dependendo da mensagem, em respostas normalmente informa ‘OK’ ou a descrição do erro e em    |
|               | eventos alguma informação relacionada ao evento.                                                                         |
+---------------+--------------------------------------------------------------------------------------------------------------------------+
| Destino       | Tipo de destino a ser transferido, valores suportados no momento: ``Ramal``.                                             |
+---------------+--------------------------------------------------------------------------------------------------------------------------+
| idDestino     | ID do Catix do destino, utilizado na transferência, pode ser recuperado através da ação ``BUSCAR_OPCOES_TRANSFERENCIA``. |
+---------------+--------------------------------------------------------------------------------------------------------------------------+
| ErroCod       | Código de erro, enviado apenas do servidor para o cliente quando ocorre algum problema ao processar a solicitação.       |
+---------------+--------------------------------------------------------------------------------------------------------------------------+
| Atributos     | Parâmetros no formato de Mapa, Chave -> Valor, são utilizados por diversos comandos e notificações para informações      |
|               | variadas, consulta a lista de comandos e eventos para verificar quais e quando são aplicáveis.                           |
+---------------+--------------------------------------------------------------------------------------------------------------------------+
| MessageId     | Identificador da mensagem, o servidor devolve as resposta para uma mensagem com o id igual ao da mensagem que originou,  |
|               | usado para identificar as resposta em um ambiente multi thread.                                                          |
+---------------+--------------------------------------------------------------------------------------------------------------------------+