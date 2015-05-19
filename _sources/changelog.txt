Change Log
==========

Versão 1.1.0 (Atual)
------------------

Melhorias internas
^^^^^^^^^^^^^^^^^^

* Adicionando validações de dependências (Asterisk Manager, Agente Online, Transações).
* Mensagens mais informativas sobre as validações e erros.
* Caso tentar se logar com o agente e ele já estiver logado, vai retornar uma mensagem de erro avisando que o agente já está logado, ``error cod 1007``.
* Logs dos usuarios conectando.
  
Melhorias nos eventos
^^^^^^^^^^^^^^^^^^^^^

* Adicionado o atributo ``ramal-agente`` no evento ``AGENT_LOGIN``, contém o ramal que o agente efetuou login, lembrando que é o ramal físico e não o alias para o mesmo.
* ``AGENTE_UNPAUSED``, Devolve o tempo total em segundos que o agente ficou naquela pausa.

Melhorias nos comandos
^^^^^^^^^^^^^^^^^^^^^^

* ``DISCAR``, Caso o parametro numeroDiscado for inválido retorno um erro (error cod 1001).

Novos comandos
^^^^^^^^^^^^^^

* ``STATUS_SERVIDOR``, retorna informações sobre o servidor como versão, quantidade de usuários conectados, tempo que o servidor está online, etc.
* ``INFORMACAO_PAUSA``, Retorna as informações da pausa do agente.
* ``BUSCAR_FILAS``, Lista as filas cadastradas no Catix.
* ``BUSCAR_ESTRATEGIAS_CHAMADA``, Lista as estratégias de chamada cadastradas no Catix.
* ``BUSCAR_CAMPANHAS``, Lista as campanhas cadastradas no Catix.
* ``CAMPANHA_CRIAR``, Cria uma nova campanha.
* ``CAMPANHA_INICIAR``, Inicia uma campanha já existente no Catix.
* ``CAMPANHA_PAUSAR``, Pausa uma campanha em execução no Catix.
* ``IMPORTAR_MAILING``, Cria um novo mailing ou adiciona contatos a um mailing já existente.
* ``RESULTADO_CONTATO_DISCADOR``, Informa o Catix do resultado de uma ligação do discador pelo agente, Efetivo e Eficaz.
* ``RESULTADO_AGENDAMENTO``, Informa o Catix do resultado de um agendamento

Novos eventos
^^^^^^^^^^^^^

* ``SCHEDULED_CALL_COMING``, notificação de que uma ligação agendada está prestes a ser iniciada dentro de x tempo. (x tempo configurado no Catix)
* ``SCHEDULED_CALL_ANSWER``, notificação de que um agente atendeu uma ligação agendada.

Novas mensagens de erro
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. tip:: Consulte a :ref:`lista_erros` para saber mais. 

* 1008
* 1009
* 1010
* 3000
* 3001
* 3002
* 3003

Versão 1.0.0
----------

*Release inicial*
