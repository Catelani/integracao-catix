Lista de Eventos
^^^^^^^^^^^^^^^^

.. note:: O campo ``informacao`` sempre vira com o nome do evento em questão.

.. note:: O campo ``tipo`` sempre será EVENT.

.. note:: O campo agente sempre virá com o ID do agente relacionado aquele evento, a menos que seja um evento que não é relacionado a nenhum agente.
    

AGENT_LOGIN
"""""""""""

**Descrição:** Evento enviado quando um agente loga no sistema.

.. code-block:: javascript

    {
      "tipo": "EVENT",
      "agente": "12",
      "informacao": "AGENT_LOGIN",
      "atributos" {
          "ramal-agente": "200"
      }
    }

+------------------------+-------------------------------------------------------+
| Campos                 | Descrição                                             |
+========================+=======================================================+
| agente                 | ID do agente, no Catix, que realizou o login.         |
+------------------------+-------------------------------------------------------+
| atributos-ramal-agente | Número do ramal fisico que o agente realizou o login. |
+------------------------+-------------------------------------------------------+


AGENT_LOGOFF
""""""""""""

**Descrição:** Evento enviado quando um agente desloga do sistema.

.. code-block:: javascript

    {
      "tipo": "EVENT",
      "agente": "12",
      "informacao": "AGENT_LOGOFF"
    }

+--------+------------------------------------------------+
| Campos | Descrição                                      |
+========+================================================+
| agente | ID do agente, no Catix, que realizou o logoff. |
+--------+------------------------------------------------+


AGENT_PAUSED
""""""""""""

**Descrição:** Evento enviado quando o agente é pausado.

.. code-block:: javascript

    {
      "tipo": "EVENT",
      "agente": "12",
      "informacao": "AGENT_PAUSED",
      "atributos": {
        "idPausa": 1,
        "pausa": "Almoço",
        "descricao": “Horário de Almoço",
        "obs": “Observação qualquer"
      }
    }

+---------------------+--------------------------------------------+
| Campos              | Descrição                                  |
+=====================+============================================+
| agente              | ID do Catix do agente que pausou.          |
+---------------------+--------------------------------------------+
| atributos-idPausa   | ID do Catix da Pausa que ele selecionou.   |
+---------------------+--------------------------------------------+
| atributos-pausa     | Nome da pausa no Catix.                    |
+---------------------+--------------------------------------------+
| atributos-descricao | Descrição da pausa no Catix.               |
+---------------------+--------------------------------------------+
| atributos-obs       | Observação que o agente colocou ao pausar. |
+---------------------+--------------------------------------------+


AGENT_UNPAUSED
""""""""""""""

**Descrição:** Evento enviado quando o agente é despausado.

.. code-block:: javascript

    {
      "tipo": "EVENT",
      "agente": "12",
      "informacao": "AGENT_UNPAUSED",
      "atributos": {
        "idPausa": 1,
        "pausa": "Almoço",
        "descricao": “Horário de Almoço"
      }
    }

+-------------------+------------------------------------------+
| Campos            | Descrição                                |
+===================+==========================================+
| agente            | ID do Catix do agente que despausou.     |
+-------------------+------------------------------------------+
| atributos-idPausa | ID do Catix da Pausa que ele selecionou. |
+-------------------+------------------------------------------+


AGENT_COMPLETE
""""""""""""""

**Descrição:** Evento enviado quando o agente termina de atender uma ligação.

.. code-block:: javascript

    {
      "tipo": "EVENT",
      "agente": "12",
      "informacao": "AGENT_COMPLETE"
    }

+--------+------------------------------------------------+
| Campos | Descrição                                      |
+========+================================================+
| agente | ID do Catix do agente que finalizou a ligação. |
+--------+------------------------------------------------+

DIALING
"""""""

**Descrição:** Evento enviado quando o sistema está discando para um número, que **NÃO** é do discador.


.. important:: Esse evento **somente** sera enviado caso a ligação seja partindo de um ``AGENTE``, se for do discador não será enviado, nem se for do Ramal.
Porém, a ligação do agente pode ser feita via integração ou via Painel do Agente no Catix.


.. code-block:: javascript

    {
      "tipo": "EVENT",
      "agente": "12",
      "informacao": "DIALING",
      "atributos": {
        "origem-tipo": "AGENTE",
        "origem-nome": "kennedy",
        "numero-discado": "17991762908",
        "rl": "5084",
        "linked-rl": "5084"
      }
    }

+-----------------------+--------------------------------------------------------------------------+
| Campo                 | Descrição                                                                |
+=======================+==========================================================================+
| agente                | ID do Catix do agente que fez a ligação.                                 |
+-----------------------+--------------------------------------------------------------------------+
| atributos-origem-nome | Nome do agente que fez a ligação.                                        |
+-----------------------+--------------------------------------------------------------------------+
| atributos-rl          | Identificação da chamada no Catix.                                       |
+-----------------------+--------------------------------------------------------------------------+
| atributos-linked-rl   | Identificação de todas as chamadas relacionadas a essa chamada no Catix. |
+-----------------------+--------------------------------------------------------------------------+


ANSWER
""""""

**Descrição:** Evento enviado quando um agente atende uma ligação, porém não deve se basear nesse evento quando estiver usando discadores.

.. hint:: Para atendimentos do discador, verificar o evento :ref:`atendeu_ligacao_preditivo`.

.. code-block:: javascript

    {
      "tipo": "EVENT",
      "agente": "12",
      "informacao": "ANSWER",
      "atributos": {
        "origem-tipo": "AGENTE",
        "origem-nome": "kennedy",
        "numero-discado": "17991762908",
        "rl": "5084",
        "linked-rl": "5084"
      }
    }

+-----------------------+--------------------------------------------------------------------------+
| Campo                 | Descrição                                                                |
+=======================+==========================================================================+
| agente                | ID do Catix do agente que atendeu a ligação.                             |
+-----------------------+--------------------------------------------------------------------------+
| atributos-origem-nome | Nome do agente que fez a ligação.                                        |
+-----------------------+--------------------------------------------------------------------------+
| atributos-rl          | Identificação da chamada no Catix.                                       |
+-----------------------+--------------------------------------------------------------------------+
| atributos-linked-rl   | Identificação de todas as chamadas relacionadas a essa chamada no Catix. |
+-----------------------+--------------------------------------------------------------------------+


HANGUP
""""""

**Descrição:** Evento enviado quando uma ligação é desligada.

.. code-block:: javascript

    {
      "tipo": "EVENT",
      "agente": "12",
      "informacao": "HANGUP",
      "atributos": {
        "origem-tipo": "AGENTE",
        "origem-nome": "kennedy",
        "numero-discado": "17991762908",
        "rl": "5084",
        "linked-rl": "5084"
      }
    }

+-----------------------+------------------------------------------------------------------+
| Campo                 | Descrição                                                        |
+=======================+==================================================================+
| agente                | ID do Catix do agente que desligou a ligação.                    |
+-----------------------+------------------------------------------------------------------+
| atributos-origem-nome | Nome do agente que fez a ligação.                                |
+-----------------------+------------------------------------------------------------------+
| atributos-rl          | Identificação da chamada no Catix.                               |
+-----------------------+------------------------------------------------------------------+
| atributos-linked-rl   | Identificação de todas são relacionadas aquela chamada no Catix. |
+-----------------------+------------------------------------------------------------------+


.. _atendeu_ligacao_preditivo:

AGENT_RECEIVED_DIALER_CALL
""""""""""""""""""""""""""

**Descrição:** Evento enviado quando um agente atende uma chamada que é do discador.

.. code-block:: javascript

    {
      "tipo": "EVENT",
      "agente": "12",
      "informacao": "AGENT_RECEIVED_DIALER_CALL",
      "atributos": {
        "contato-id": "387076",
        "contato-cpfcnpj": "2994",
        "contato-contrato": "123456",
        "numero-contato-id": "235041",
        "numero-contato": "1712345678",
        "campanha-id": "18",
        "rl": "5143",
        "linked-rl": "5141"
      }
    }


SCHEDULED_CALL_COMING
"""""""""""""""""""""

**Descrição:** Notificação de que uma ligação agendada está prestes a acontecer, em x tempo, esse tempo é configurado no Catix e é valido para todas as ligações agendadas.  

.. code-block:: javascript

    {
      "tipo": "EVENTO",
      "informacao": "SCHEDULED_CALL_COMMING",
      "atributos": {
        "agendamento-id": "15",
        "agendamento-data-hora": "08/04/2015 19:13:22",
        "agendamento-destino-tipo": "Agente",
        "agendamento-destino-tipo-id": "13"
      },
      "messageId": "1"
    }

+---------------------------------------+---------------------------------------------------------------------+
| Campo                                 | Descrição                                                           |
+=======================================+=====================================================================+
| atributos-agendamento-id              | Id do agendamento                                                   |
+---------------------------------------+---------------------------------------------------------------------+
| atributos-agendamento-data-hora       | Data e hora do agendamento                                          |
+---------------------------------------+---------------------------------------------------------------------+
| atributos-agendamento-destino-tipo    | Tipo do destino no Catix, atualmente o único possível é ``Agente``. |
+---------------------------------------+---------------------------------------------------------------------+
| atributos-agendamento-destino-tipo-id | Identificação no Catix do destino.                                  |
+---------------------------------------+---------------------------------------------------------------------+

SCHEDULED_CALL_ASNWER
"""""""""""""""""""""

**Descrição:** Notificação enviada quando um destino atende uma chamada que é agendada.

.. code-block:: javascript

    {
      "tipo": "EVENTO",
      "informacao": "SCHEDULED_CALL_ANSWER",
      "atributos": {
        "agendamento-id": "15",
        "agendamento-destino-tipo": "Agente",
        "agendamento-destino-tipo-id": "13",
        "agendamento-cod-referencia": "123456789",
        "contato-id": "15",
        "contato-cpfcnpj": "40002866749",
        "contato-contrato": "102346123",
        "numero-contato-id": "5678",
        "numero-contato": "17991234798",
        "numero-agendamento-id": “1234",     
        “numero-agendamento”:”17123456778”,
        "rl": "12345",
        "linked-rl": "12345"
      },
      "messageId": "1"
    } 

**Atributos**

+-----------------------------+-------------------------------------------------------------------------------------------------+
| Campo                       | Descrição                                                                                       |
+=============================+=================================================================================================+
| agendamento-id              | Identificação do agendamento no Catix                                                           |
+-----------------------------+-------------------------------------------------------------------------------------------------+
| agendamento-destino-tipo    | Tipo do destino no Catix, atualmente o único possível é ``Agente``                              |
+-----------------------------+-------------------------------------------------------------------------------------------------+
| agendamento-destino-tipo-id | Identificação no Catix do destino.                                                              |
+-----------------------------+-------------------------------------------------------------------------------------------------+
| agendamento-cod-referencia  | Código de referencia que pode ser fornecido na criação do agendamento, para ser usado no        |
|                             | retorno para identificar a quem pertence o agendamento.                                         |
+-----------------------------+-------------------------------------------------------------------------------------------------+
| contato-id                  | Id do contato do mailing, esse atributo e os outros relacionados ao contato e numero de contato |
|                             | só serão devolvidos caso o agendamento seja de um contato do mailing.                           |
+-----------------------------+-------------------------------------------------------------------------------------------------+
| numero-agendamento-id       | ID do número discado, esse atributo só será devolvido caso não seja um contato do mailing.      |
+-----------------------------+-------------------------------------------------------------------------------------------------+
| numero-agendamento          | Número discador caso não seja um contato do mailing.                                            |
+-----------------------------+-------------------------------------------------------------------------------------------------+

