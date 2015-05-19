Mensagem de Erro
^^^^^^^^^^^^^^^^

As mensagens de erro retornadas pelo sistema seguem o padrão abaixo:

.. code-block:: javascript

    {
	  "tipo": "ERRO",
	  "informacao": “Agente não encontrado no sistema",
	  "erroCod": "9999",
	  "messageId": "1"
	}


+-----------------+-----------------------------------------------------------------------------+
| Campo	Descrição |                                                                             |
+=================+=============================================================================+
| informacao      | Descrição do erro.                                                          |
+-----------------+-----------------------------------------------------------------------------+
| erroCod         | Código do erro. Existe uma tabela com os códigos dos erros neste documento. |
+-----------------+-----------------------------------------------------------------------------+
| messageId       | Identificação da mensagem que será retornada junto com a resposta.          |
+-----------------+-----------------------------------------------------------------------------+

.. hint:: Consulte a lista de erros para verificar os códigos de erros e suas possiveis causas! :ref:`lista_erros`

