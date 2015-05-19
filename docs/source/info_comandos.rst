Informações dos comandos
^^^^^^^^^^^^^^^^^^^^^^^^

.. important:: Os exemplos ``JSON`` serão formatados em várias linhas para facilitar a legibilidade, porém, no momento da troca de mensagem, devem ser enviados em uma única linha, da mesma forma que os ``JSONs`` enviados pelo servidor ao cliente sempre serão em uma única linha.

.. important:: O campo ``MessageId`` é sempre opcional, ele guarda uma identificação na mensagem (qualquer valor adicionado manualmente) e que será devolvida junto com a resposta, utilizado normalmente para identificar a resposta de uma requisição em um ambiente multithread.

.. important:: O campo ``agente`` é opcional quando estiver logado com o comando ``LOGIN_SINGLE_USER``, pois esse campo é atribuído automaticamente à mensagem a partir do agente especificado junto com o ``LOGIN_SINGLE_USER`` no momento de iniciar a conexão.

.. important:: O tipo ``ACAO`` é opcional nas mensagens de comando, caso tenha o comando preenchido o sistema entende que a mensagem é do tipo ``comando``.

.. danger:: Os comandos e as resposta são **asincronos**, o que significa que, para identificar corretamente a resposta de uma mensagem é de necessario enviar o campo ``messageId`` com um identificador único mantido pelo cliente (você), que você usará para identificar corretamente as mensagens.
            Ex::

				Cliente 1 >> envia comando de discar (MessageId = 1)
				Cliente 2 >> Enviar comando de desligar a ligação (MessageId = 2)
				Servidor >> Responde o comando de desligar (MessageId = 2)
				Servidor >> Responde o comando de discar (MessageId = 1)
