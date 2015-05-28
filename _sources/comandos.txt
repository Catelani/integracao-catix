Lista de comandos
^^^^^^^^^^^^^^^^^

.. warning:: O usuário e a senha necessário para autenticação não é o usuário e a senha do ramal nem dos agentes, é um usuário especifico para a integração, por favor, solicite a Catelani o cadastro de um.



LOGIN_SINGLE_USER
"""""""""""""""""

**Descrição:** O modo Single User significa que apenas um agente vai utilizar aquela conexão. No momento do login será fornecido a qual agente pertence essa conexão e não será mais necessário informar esse agente nos comandos seguintes.

.. code-block:: javascript

    {
      "tipo": "ACAO",
      "comando": "LOGAR_SINGLE_USER",
      "agente": "12",
      "atributos": {
        "usuario": "zupao",
        "senha": "123456"
      },
      "messageId": "1"
    }

+-------------------+---------------------------------------------------------------------------+
| Campo             | Descrição                                                                 |
+===================+===========================================================================+
| agente            | ID do agente no Catix, vai relacioná-lo aquela conexão.                   |
+-------------------+---------------------------------------------------------------------------+
| atributos-usuario | Usuário configurado no Catix para autenticação no servidor de integração. |
+-------------------+---------------------------------------------------------------------------+
| atributos-senha   | Senha configurada para o usuário.                                         |
+-------------------+---------------------------------------------------------------------------+
| messageId         | Identificação da mensagem que será retornada junto com a resposta.        |
+-------------------+---------------------------------------------------------------------------+


LOGIN_MULTI_USER
""""""""""""""""

**Descrição:** O modo Multi User significa que vários agentes vão utilizar aquela conexão. No momento do login não é necessário informar o agente, porém em todos os comandos seguintes se faz necessário.


.. code-block:: javascript

    {
      "tipo": "ACAO",
      "comando": "LOGAR_MULTI_USER",
      "atributos": {
        "usuario": "zupao",
        "senha": "123456"
      },
      "messageId": "1"
    }

+-------------------+---------------------------------------------------------------------------+
| Campo             | Descrição                                                                 |
+===================+===========================================================================+
| atributos-usuario | Usuário configurado no Catix para autenticação no servidor de integração. |
+-------------------+---------------------------------------------------------------------------+
| atributos-senha   | Senha do usuario.                                                         |
+-------------------+---------------------------------------------------------------------------+
| messageId         | Identificação da mensagem que será retornada junto com a resposta.        |
+-------------------+---------------------------------------------------------------------------+


AGENTE_LOGAR
""""""""""""

**Descrição:** Envia uma solicitação de login para o agente, o ramal do agente deve estar disponível pois ele receberá uma ligação que solicitará a senha dele, caso tiver uma configurada para o agente, e após isso ele já estará logado.

.. code-block:: javascript

    {
     "tipo": "ACAO",
      "comando": "AGENTE_LOGAR",
      "agente": "12",
      "atributos": {
        "login-ramal": "100"
      },
      "messageId": "1"
    }

+-----------------------+--------------------------------------------------------------------+
| Campo                 | Descrição                                                          |
+=======================+====================================================================+
| agente                | ID do agente no Catix.                                             |
+-----------------------+--------------------------------------------------------------------+
| atributos-login-ramal | Ramal no qual o agente vai fazer login.                            |
+-----------------------+--------------------------------------------------------------------+
| messageId             | Identificação da mensagem que será retornada junto com a resposta. |
+-----------------------+--------------------------------------------------------------------+

AGENTE_DESLOGAR
"""""""""""""""

**Descrição:** Envia uma solicitação de logoff. O agente saíra do modo “logado como agente” e não estará mais apto a receber ligações do discador ou através do comando DISCAR.

.. code-block:: javascript

    {
     "tipo": "ACAO",
      "comando": "AGENTE_DESLOGAR",
      "agente": "12"
    }

+-----------------------+--------------------------------------------------------------------+
| Campo                 | Descrição                                                          |
+=======================+====================================================================+
| agente                | ID do agente no Catix.                                             |
+-----------------------+--------------------------------------------------------------------+
| messageId             | Identificação da mensagem que será retornada junto com a resposta. |
+-----------------------+--------------------------------------------------------------------+

DISCAR
""""""

**Descrição:** Envia uma solicitação de discagem ao servidor e direciona a chamada para o agente.

.. code-block:: javascript

    {
     "tipo": "ACAO",
      "comando": "DISCAR",
      "numeroDiscado": "099134567",
      "agente": "12",
      "messageId": "1"
    }


+---------------+------------------------------------------------------------------------------------+
| Campo         | Descrição                                                                          |
+===============+====================================================================================+
| numeroDiscado | Número que o sistema vai discar, deve começar com o 0 caso seja um numero externo. |
+---------------+------------------------------------------------------------------------------------+
| agente        | ID do agente no Catix, que vai receber aquela ligação.                             |
+---------------+------------------------------------------------------------------------------------+
| messageId     | Identificação da mensagem que será retornada junto com a resposta.                 |
+---------------+------------------------------------------------------------------------------------+

REDISCAR
""""""""

**Descrição:** Disca novamente para o último número que o agente discou.

.. code-block:: javascript

    {
     "tipo": "ACAO",
      "comando": "REDISCAR",
      "messageId": "1"
    }

PAUSAR
""""""

**Descrição:** Serve tanto para pausar quanto despausar o agente, controlado peo atributo ``PAUSA-ACAO``.

.. code-block:: javascript

    {
     "tipo": "ACAO",
      "comando": "PAUSAR",
      "agente": "12",
      "atributos": {
        "pausa-id": 1,
        "pausa-obs": "Almoço",
        "pausa-acao": "PAUSAR"
      },
      "messageId": "1"
    }

STATUS_AGENTE
"""""""""""""

**Descrição:** Retorna algumas informações do status do agente como, status, tempo, numero discado, observações.

.. code-block:: javascript

    {
     "tipo": "ACAO",
      "comando": "STATUS_AGENTE",
      "agente": "13",
      "messageId": "1"
    }

Exemplos de retornos:

.. code-block:: javascript

    > Agente somente logado

    {
      "tipo": "NOTIFICACAO",
      "informacao": "OK",
      "atributos": {
        "obs": "-",
        "tempo": "-",
        "nome": "Agente 200",
        "ramal_fisico": "200",
        "idAgente": "13",
        "numero_discado": "-",
        "status": "Disponível"
      }
    }

    > Agente discando

    {
      "tipo": "NOTIFICACAO",
      "informacao": "OK",
      "atributos": {
        "obs": "<b>Tipo Ligação:</b><i> Sainte</i> <b>Tronco:</b><i> 170017</i> <b>Tipo de Número:</b><i> Móvel DDD</i> ",
        "tempo": "00:00:05",
        "nome": "Agente 200",
        "ramal_fisico": "200",
        "idAgente": "13",
        "numero_discado": "(17) 99149-1234",
        "status": "Discando"
      }
    }

    > Agente em atedimento de ligação (Não Discador)

    {
      "tipo": "NOTIFICACAO",
      "informacao": "OK",
      "atributos": {
        "obs": "<b>Tipo Ligação:</b><i> Sainte</i> <b>Tronco:</b><i> 170017</i> <b>Tipo de Número:</b><i> Móvel DDD</i> ",
        "tempo": "00:00:01",
        "nome": "Agente 200",
        "ramal_fisico": "200",
        "idAgente": "13",
        "numero_discado": "(17) 99149-1234",
        "status": "Em ligação"
      }
    }

    > Agente em atendimento de ligação do discador

    {
      "tipo": "NOTIFICACAO",
      "informacao": "OK",
      "atributos": {
        "obs": "<b>Tipo Ligação:</b><i> Preditivo</i> <b>Tronco:</b><i> 170017</i> <b>Tipo de Número:</b><i> Móvel DDD</i> <b>Campanha:</b><i> teste</i> <b>Contato: </b><i> Contato 75</i> ",
        "tempo": "00:00:03",
        "nome": "Agente 200",
        "ramal_fisico": "200",
        "idAgente": "13",
        "numero_discado": "(17) 99149-1234",
        "status": "Em ligação"
      }
    }

    > Agente em pausa

    {
      "tipo": "NOTIFICACAO",
      "informacao": "OK",
      "atributos": {
        "obs": "Motivo: Almoço - Obs: Observação que o usuário digitou",
        "tempo": "00:15:07",
        "nome": "Agente 200",
        "ramal_fisico": "200",
        "idAgente": "13",
        "numero_discado": "-",
        "status": "Pausado"
      }
    }

    > Agente em pós atendimento

    {
      "tipo": "NOTIFICACAO",
      "informacao": "OK",
      "atributos": {
        "obs": "Pausa automática para pós atendimento.",
        "tempo": "00:00:08",
        "nome": "Agente 200",
        "ramal_fisico": "200",
        "idAgente": "13",
        "numero_discado": "-",
        "status": "Pós Atendimento"
      }
    }

+-----------+--------------------------------------------------------------------+
| Campo     | Descrição                                                          |
+===========+====================================================================+
| agente    | ID do agente no Catix que tera seu status consultado.              |
+-----------+--------------------------------------------------------------------+
| messageId | Identificação da mensagem que será retornada junto com a resposta. |
+-----------+--------------------------------------------------------------------+


DESLIGAR_CHAMADA
""""""""""""""""

**Descrição:** Desliga a chamada atual do agente.

.. code-block:: javascript

    {
     "tipo": "ACAO",
      "comando": "DESLIGAR_CHAMADA",
      "agente": "12",
      "messageId": "1"
    }

+-----------+--------------------------------------------------------------------+
| Campo     | Descrição                                                          |
+===========+====================================================================+
| agente    | ID do agente no Catix que a chamada vai ser desligada.             |
+-----------+--------------------------------------------------------------------+
| messageId | Identificação da mensagem que será retornada junto com a resposta. |
+-----------+--------------------------------------------------------------------+


BUSCAR_TIPOS_PAUSA
""""""""""""""""""

**Descrição:** Lista as pausas disponíveis no sistema.

.. code-block:: javascript

    {
     "tipo": "ACAO",
      "comando": "BUSCAR_TIPOS_PAUSA",
      "messageId": "1"
    }

    >> Retorno

    {
      "tipo": "NOTIFICACAO",
      "informacao": "OK",
      "messageId": "1",
      "atributos": {
        "pausas": [
          {
            "id": 1,
            "nome": "Almoço",
            "descricao": "Horario de almoço",
            "exigeObs": false
          },
          {
            "id": 2,
            "nome": "Outra tarefa",
            "descricao": "Atividade diferente do cargo",
            "exigeObs": true
          }
        ]
      }
    }


BUSCAR_RAMAIS
"""""""""""""

**Descrição:** Lista os ramais do sistema. Usado para disponibilizar para o agente em qual ramal o mesmo deseja efetuar login.

.. important:: | Formato do ramal no campo ``atributos`` do retorno: ``Alias do ramal: Nome do Ramal fisico``. 
               | Estas informações são cadastradas no Catix.

.. code-block:: javascript

    {
     "tipo": "ACAO",
      "comando": "BUSCAR_RAMAIS",
      "messageId": "1"
    }

    >> Retorno:

    {
      "tipo": "NOTIFICACAO",
      "informacao": "OK",
      "messageId": "1",
      "atributos": {
        "100": "100",
        "101": "101",
        "102": "102",
        "103": "103",
     }
    }   


TRANSFERIR
""""""""""

**Descrição:** Faz a transferência da ligação atual do agente para o destino que ela informar. Os destinos possíveis são os retornados pelo comando ``BUSCAR_OPCOES_TRANSFERENCIA``.

.. code-block:: javascript

    {
     "tipo": "ACAO",
      "comando": "TRANSFERIR",
      "agente": "12",
      "destino": "Ramal",
      "numeroDiscado": "1234",
      "idDestino": "1",
      "messageId": "1"
    }

+---------------+-----------------------------------------------------------------------------------------------------------------------+
| Campos        | Descrição                                                                                                             |
+===============+=======================================================================================================================+
| agente        | ID do Catix do agente que vai ter sua ligação transferida.                                                            |
+---------------+-----------------------------------------------------------------------------------------------------------------------+
| destino       | Tipo do destino, no momento o sistema somente faz transferências para ``Ramal``, mas é possível obter a lista de      |
|               | destinos disponíveis e suas opções através do comando ``BUSCAR_OPCOES_TRANSFERENCIA``. Esse campo é opcional caso se  |
|               | use o ``numeroDiscado``.                                                                                              |
+---------------+-----------------------------------------------------------------------------------------------------------------------+
| idDestino     | Id do destino a ser transferido, é usado em conjunto com o campo destino. *Ignorado quando o campo* ``numeroDiscado`` |
|               | *for informado.*                                                                                                      |
+---------------+-----------------------------------------------------------------------------------------------------------------------+
| numeroDiscado | Número do ramal a ser transferido, caso este campo esteja preenchido, o campo destino e IdDestino serão ignorados.    |
+---------------+-----------------------------------------------------------------------------------------------------------------------+
| messageId     | Identificação da mensagem que será retornada junto com a resposta.                                                    |
+---------------+-----------------------------------------------------------------------------------------------------------------------+

.. warning:: Na transferência temos duas opções: uma é informando o ``destino`` e o ``idDestino`` e a outra é passando o número do ramal no número discado.


BUSCAR_OPCOES_TRANSFERENCIA
"""""""""""""""""""""""""""

**Descrição:** Busca as opções de transferencia disponíveis no sistema.

.. code-block:: javascript

    {
     "tipo": "ACAO",
      "comando": "BUSCAR_OPCOES_TRANSFERENCIA",
      "messageId": "1"
    }

    >> Retorno:

    {
      "tipo": "NOTIFICACAO",
      "informacao": "OK",
      "messageId": "1",
      "atributos": {
        "ramal": [
          {
            "id": 2,
            "nome": "100"
          },
          {
            "id": 3,
            "nome": "101"
          },
          {
            "id": 5,
            "nome": "102"
          },
          {
            "id": 6,
            "nome": "103"
          },
          {
            "id": 7,
            "nome": "500"
          },
          {
            "id": 15,
            "nome": "123"
          }
        ]
      }
    }

SAIR
""""

**Descrição:** Fecha a comunicação com o sistema.

.. code-block:: javascript

    {
     "tipo": "ACAO",
      "comando": "SAIR"
    }

STATUS_SERVIDOR
"""""""""""""""

**Descrição:** Retorna informações sobre o servidor.

.. code-block:: javascript

    {
      "tipo": "ACAO",
      "comando": "STATUS_SERVIDOR",
      "messageId": "1"
    }

    >> Retorno: 

    {
       "informacao":"OK",
       "messageId":"1",
       "atributos":{
          "usuarios-multi-user":0,
          "requisicoes":2,
          "acoes-executadas":1,
          "tempo-rodando":"1 Minutos 36 Segundos 868 Milisegundos",
          "total-usuarios":1,
          "total-conexoes":1,
          "data-inicializacao":"25/03/2015 10:16:21",
          "versao":"1.1",
          "usuarios-single-user":1,
          "conexoes-recebidas":1
       }
    }

+----------------------+--------------------------------------------------------------------+
| Campo                | Descrição                                                          |
+======================+====================================================================+
| tempo-rodando        | Tempo em que o servidor está rodando.                              |
+----------------------+--------------------------------------------------------------------+
| acoes-executadas     | Quantidade de ações que o servidor já executou.                    |
+----------------------+--------------------------------------------------------------------+
| conexoes-recebidas   | Quantidade de conexões que o servidor já recebeu.                  |
+----------------------+--------------------------------------------------------------------+
| requisicoes          | Quantidade de requisições que o servidor já recebeu.               |
+----------------------+--------------------------------------------------------------------+
| data-inicializacao   | Data de inicialização do servidor.                                 |
+----------------------+--------------------------------------------------------------------+
| versao               | Versão atual do servidor.                                          |
+----------------------+--------------------------------------------------------------------+
| usuarios-single-user | Quantidade de usuarios SINGLE_USER logados.                        |
+----------------------+--------------------------------------------------------------------+
| usuarios-multi-user  | Quantidade de usuarios MULTI_USER logados.                         |
+----------------------+--------------------------------------------------------------------+
| total-usuario        | Total de usuarios conectados no servidor.                          |
+----------------------+--------------------------------------------------------------------+
| total-conexoes       | Total de conexões abertas com o servidor.                          |
+----------------------+--------------------------------------------------------------------+
| messageId            | Identificação da mensagem que será retornada junto com a resposta. |
+----------------------+--------------------------------------------------------------------+


INFORMACAO_PAUSA
""""""""""""""""

**Descrição:** Busca informações da pausa de um agente.

.. code-block:: javascript


    {
      "tipo": "ACAO",
      "comando": "STATUS_SERVIDOR",
      "agente": "12",
      "messageId": "1"
    }

    >> Retorno:

    {
      "informacao": "OK",
      "messageId": "1",
      "atributos": {
        "id-pausa": "3",
        "pausa": "Almoço",
        "descricao": "Pausa para o almoço",
        "tempo-limite": "60 minutos",
        "tempo-decorrido": "500",
        "obs": "Vou demorar mais no almoço pois vou ao banco"
      }
    }

+-----------------+---------------------------------------------------------------------------------------+
| Campo           | Descrição                                                                             |
+=================+=======================================================================================+
| id-pausa        | Id da pausa no Catix.                                                                 |
+-----------------+---------------------------------------------------------------------------------------+
| pausa           | Nome da pausa no Catix.                                                               |
+-----------------+---------------------------------------------------------------------------------------+
| descricao       | Descrição da pausa no Catix.                                                          |
+-----------------+---------------------------------------------------------------------------------------+
| tempo-limite    | Tempo em minutos da pausa no Catix, sempre no formato X minutos, onde x é um inteiro. |
+-----------------+---------------------------------------------------------------------------------------+
| tempo-decorrido | Inteiro representando o tempo em segundos decorrido desde que o agente pausou.        |
+-----------------+---------------------------------------------------------------------------------------+
| obs             | Observação informada pelo agente na hora de pausar.                                   |
+-----------------+---------------------------------------------------------------------------------------+
| messageId       | Identificação da mensagem que será retornada junto com a resposta.                    |
+-----------------+---------------------------------------------------------------------------------------+


BUSCAR_FILAS
""""""""""""

**Descrição:** Busca as filas disponíveis no Catix.

.. code-block:: javascript

    {
      "tipo": "ACAO",
      "comando": "BUSCAR_FILAS",
      "messageId": "1"
    }

    >> Retorno: 

    {
      "tipo": "NOTIFICACAO",
      "informacao": "OK",
      "messageId": "1",
      "atributos": {
        "filas": [
          {
            "id": 154,
            "nome": "RECEPCAO",
            "tipoFila": "Ramal"
          },
          {
            "id": 155,
            "nome": "COBRANCA_GERAL",
            "tipoFila": "Agente"
          }
        ]
      }
    }

+-----------+--------------------------------------------------------------------+
| Campo     | Descrição                                                          |
+===========+====================================================================+
| filas     | Array com as filas do sistema.                                     |
+-----------+--------------------------------------------------------------------+
| id        | Id da fila no Catix.                                               |
+-----------+--------------------------------------------------------------------+
| nome      | Nome da fila no Catix.                                             |
+-----------+--------------------------------------------------------------------+
| tipoFila  | Tipo da fila no Catix.                                             |
+-----------+--------------------------------------------------------------------+
| messageId | Identificação da mensagem que será retornada junto com a resposta. |
+-----------+--------------------------------------------------------------------+


BUSCAR_ESTRATEGIAS_CHAMADA
""""""""""""""""""""""""""

**Descrição:** Busca as estratégias de chamada cadastradas no Catix.

.. code-block:: javascript

    {
      "tipo": "ACAO",
      "comando": "BUSCAR_ESTRATEGIAS_CHAMADA",
      "messageId": "1"
    }

    >> Retorno: 

    {
      "tipo": "NOTIFICACAO",
      "informacao": "OK",
      "messageId": "1",
      "atributos": {
        "estrategias": [
          {
            "id": 1,
            "nome": "Teste"
          }
        ]
      }
    }

+-------------+--------------------------------------------------------------------+
| Campo       | Descricao                                                          |
+=============+====================================================================+
| estrategias | Array com as estratégias do sistema.                               |
+-------------+--------------------------------------------------------------------+
| id          | Id da estratégia no Catix.                                         |
+-------------+--------------------------------------------------------------------+
| nome        | Nome da estratégia no Catix.                                       |
+-------------+--------------------------------------------------------------------+
| messageId   | Identificação da mensagem que será retornada junto com a resposta. |
+-------------+--------------------------------------------------------------------+


BUSCAR_CAMPANHAS
""""""""""""""""

**Descrição:** Busca as campanhas cadastradas no Catix.

.. code-block:: javascript

    {
      "tipo": "ACAO",
      "comando": "BUSCAR_CAMPANHAS",
      "messageId": "1"
    }

    >> Retorno:

    {
      "tipo": "NOTIFICACAO",
      "informacao": "OK",
      "messageId": "1",
      "atributos": {
        "campanhas": [
          {
            "id": 7,
            "nome": "teste",
            "status": "Finalizada",
            "destinoTipo": "Fila",
            "destino": "151"
          },
          {
            "id": 8,
            "nome": "teste7",
            "status": "Pausada",
            "destinoTipo": "Fila",
            "destino": "151"
          }
        ]
      }
    }

+---------------------------------+-----------------------------------------------------------------------+
| Campo                           | Descrição                                                             |
+=================================+=======================================================================+
| campanhas                       | Array com as campanhas do sistema.                                    |
+---------------------------------+-----------------------------------------------------------------------+
| id                              | Id da campanha no Catix.                                              |
+---------------------------------+-----------------------------------------------------------------------+
| nome                            | Nome da campanha no Catix.                                            |
+---------------------------------+-----------------------------------------------------------------------+
| status                          | Status da campanha no Catix, que pode ser: Ativo, Finalizada, Pausada |
+---------------------------------+-----------------------------------------------------------------------+
| destinoTipo                     | Tipo do destino no Catix, Fila, Ramal, etc…                           |
+---------------------------------+-----------------------------------------------------------------------+
| destino                         | ID do destino no Catix.                                               |
+---------------------------------+-----------------------------------------------------------------------+
| messageId                       | Identificação da mensagem que será retornada junto com a resposta.    |
+---------------------------------+-----------------------------------------------------------------------+


IMPORTAR_MAILING
""""""""""""""""

**Descrição:** Importa um mailing novo, ou adiciona novos contatos a um mailing já existente.

.. code-block:: javascript

    {
      "tipo": "ACAO",
      "comando": "IMPORTAR_MAILING",
      "messageId": "1",
      "mailing": {
        "idMailing": 54,
        "nmNome": "Mailing Teste",
        "dsDescricao": "Importando mailing via integração",
        "contatos": [
          {
            "nmNome": "Contato 1",
            "dsRgIe": "1245645678",
            "dsCpfCnpj": "40002812345",
            "dsEndereco": "Rua teste",
            "cdContrato": "abc123",
            "numerosContatos": [
              {
                "cfNumero": "17991351234",
                "prioridade": 1
              }
            ],
            "agendamentos": [
              {
                "date": "01/01/2012 08:00:00",
                "agente": {
                  "idUsuario": 14
                },
                "numerosPrioritarios": [
                  {
                    "cfNumero": "17991351234",
                    "prioridade": 1
                  }
                ]
              }
            ]
          }
        ]
      }
    }

.. important:: O campo ``mailing`` é um objeto dentro da mensagem e não um atributo.

Exemplo de Retorno:

.. code-block:: javascript

    {
      "tipo": "NOTIFICACAO",
      "informacao": "OK",
      "messageId": "1",
      "atributos": {
        "mailing-id": 54,
        "mailing-total-contatos": 13,
        "mailing-total-contatos-adicionados": 1,
        "mailing-total-numeros": 25,
        "mailing-total-numeros-adicionados": 1,
        "mailing-total-agendamentos": 13,
        “mailing-total-agendamentos-adicionados": 1
      }
    }


+------------------------+------------------------------------------------------------------------------------------------------------------------+
| Campo                  | Descrição                                                                                                              |
+========================+========================================================================================================================+
| agente                 | Usuário que criou a campanha, não é necessário informar caso esteja usando o tipo de conexão ``SINGLE_USER``. Esse     |
|                        | parâmetro é apenas para fins de log.                                                                                   |
+------------------------+------------------------------------------------------------------------------------------------------------------------+
| campanha-descricao     | Descrição da campanha.                                                                                                 |
+------------------------+------------------------------------------------------------------------------------------------------------------------+
| campanha-data-inicial  | Data inicial da campanha no formato ``dd/MM/yyyy``.                                                                    |
+------------------------+------------------------------------------------------------------------------------------------------------------------+
| campanha-data-final    | Data final da campanha no formato ``dd/MM/yyyy``.                                                                      |
+------------------------+------------------------------------------------------------------------------------------------------------------------+
| campanha-hora-inicial  | Horário de inicio da campanha no formato ``hh:mm:ss``.                                                                 |
+------------------------+------------------------------------------------------------------------------------------------------------------------+
| campanha-hora-final    | Horário de fim da campanha no formato ``hh:mm:ss``.                                                                    |
+------------------------+------------------------------------------------------------------------------------------------------------------------+
| campanha-dias-semana   | Dias da semana que a campanha vai executar no formato curto respeitando maiúsculas e minúsculas separados por virgula. |
|                        | Opções: ``Seg``, ``Ter``, ``Qua``, ``Qui``, ``Sex``, ``Sab``, ``Dom``                                                  |
+------------------------+------------------------------------------------------------------------------------------------------------------------+
| campanha-estrategia-id | ID da estratégia que será usada, deve ser uma previamente cadastrada no Catix.                                         |
+------------------------+------------------------------------------------------------------------------------------------------------------------+
| campanha-destino       | Tipo do destino da campanha, atualmente o sistema suporta apenas ``Fila``.                                             |
+------------------------+------------------------------------------------------------------------------------------------------------------------+
| campanha-destino-id    | ID do destino, como o sistema atualmente só suporta fila é o ID da fila.                                               |
+------------------------+------------------------------------------------------------------------------------------------------------------------+
| campanha-mailing-id    | ID do mailing no Catix a ser usado com essa campanha.                                                                  |
+------------------------+------------------------------------------------------------------------------------------------------------------------+
| messageId              | Identificação da mensagem que será retornada junto com a resposta.                                                     |
+------------------------+------------------------------------------------------------------------------------------------------------------------+


RESULTADO_AGENDAMENTO
"""""""""""""""""""""

**Descrição:** Informa o Catix do resultado de um agendamento.

.. code-block:: javascript

    {
      "tipo": "ACAO",
      "comando": "RESULTADO_AGENDAMENTO",
      "agente": "13",
      "atributos": {
        "agendamento-id": "15",
        "agendamento-efetivo": "true",
        "agendamento-eficaz": "true"
      },
      "messageId": "1"
    }

+---------------------+--------------------------------------------------------------------+
| Campo               | Descrição                                                          |
+=====================+====================================================================+
| agendamento-id      | ID do agendamento no Catix que tera seu status atualizado.         |
+---------------------+--------------------------------------------------------------------+
| agendamento-efetivo | Flag (true, false, Sim, Nao) informa se o agendamento foi efetivo. |
+---------------------+--------------------------------------------------------------------+
| agendamento-eficaz  | Flag (true, false, Sim, Nao) informa se o agendamento foi eficaz.  |
+---------------------+--------------------------------------------------------------------+
| messageId           | Identificação da mensagem que será retornada junto com a resposta. |
+---------------------+--------------------------------------------------------------------+


RESULTADO_CONTATO_DISCADOR
""""""""""""""""""""""""""

**Descrição:** Informa o discador do resultado de uma ligação atendida.

.. code-block:: javascript

    {
    "tipo": "ACAO",
    "comando": "RESULTADO_CONTATO_DISCADOR",
    "messageId": "1",
    "atributos": {
      "eficaz": "Sim",
      "efetivo": "Sim",
      "contato-id": "15",
      "numero-contato-id": "1000",
      "campanha-id": "5",
      "agente-disponivel": "Sim"
    }
  }

+-------------------+----------------------------------------------------------------------------------------------------------------------+
| Campo             | Descrição                                                                                                            |
+===================+======================================================================================================================+
| eficaz            | Informa se houve negociação ou não para essa ligação                                                                 |
+-------------------+----------------------------------------------------------------------------------------------------------------------+
| efetivo           | Informa se a ligação foi atendida ou não                                                                             |
+-------------------+----------------------------------------------------------------------------------------------------------------------+
| contato-id        | ID do contato no Catix.                                                                                              |
+-------------------+----------------------------------------------------------------------------------------------------------------------+
| numero-contato-id | ID do numero do contato no Catix.                                                                                    |
+-------------------+----------------------------------------------------------------------------------------------------------------------+
| campanha-id       | ID da campanha que esse contato pertence no Catix.                                                                   |
+-------------------+----------------------------------------------------------------------------------------------------------------------+
| agente-disponivel | Flag para deixar o agente disponível ou não caso esteja usando a funcionalidade de pausa pós atendimento automatico. |
+-------------------+----------------------------------------------------------------------------------------------------------------------+
| messageId         | Identificação da mensagem que será retornada junto com a resposta.                                                   |
+-------------------+----------------------------------------------------------------------------------------------------------------------+
