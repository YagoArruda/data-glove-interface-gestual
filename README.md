

# Desenvolvimento da *data glove*

A *data glove* foi desenvolvida com o objetivo de permitir a interação com o computador por meio dos movimentos e da inclinação da mão e da flexão dos dedos, funcionando como uma alternativa ao mouse óptico. O dispositivo utiliza um microcontrolador ESP32, dois *Flex Sensors* e um sensor inercial MPU6050 para captar os movimentos realizados pelo usuário e convertê-los em comandos de interação. A Figura 1 apresenta o diagrama de montagem do dispositivo, enquanto a Figura 2 representa a arquitetura de hardware e a relação entre os componentes utilizados.

**Figura 1 – Diagrama de montagem**

![Diagrama de montagem da data glove](images/Diagrama%20Montagem.png)

**Figura 2 – Diagrama de blocos**

![Diagrama de blocos da data glove](images/Diagrama%20de%20Blocos.png)

O ESP32 é responsável pela leitura dos sensores, pelo processamento dos dados e pela transmissão dos comandos ao computador por meio da comunicação *Bluetooth*. O MPU6050 fornece informações referentes à aceleração e à velocidade angular da mão, enquanto os *Flex Sensors* registram variações de resistência associadas à flexão dos dedos. A combinação dessas informações permite distinguir os movimentos utilizados para controlar o cursor daqueles empregados para executar ações de interação.

Para o controle do cursor, a inclinação da mão é convertida em deslocamentos horizontais e verticais na tela. Entretanto, os dados de inclinação estão sujeitos ao acúmulo de erros e a más interpretações caso o usuário incline a mão para um lado e mova para o outro ou tente mover a mão mantendo-a o mais reta e estável possível. Apesar disso, o sistema utiliza as variações de inclinação da mão como referência para determinar a direção do movimento do cursor, considerando uma zona neutra para reduzir deslocamentos involuntários e limites de sensibilidade para controlar sua velocidade. Dessa maneira, a inclinação funciona como um comando relativo de movimentação, sem exigir a estimativa contínua da posição absoluta da mão.

O processamento das informações ocorre de forma sequencial, desde a aquisição dos sinais dos sensores até a geração dos comandos enviados ao computador. Inicialmente, são realizadas as leituras dos sensores inercial e dos *Flex Sensors*. Em seguida, os valores obtidos são interpretados para identificar as inclinações e as flexões relevantes, aplicando-se os limiares definidos para distinguir os movimentos intencionais das pequenas variações dos sinais. Por fim, as informações processadas são convertidas em comandos de movimentação ou interação e transmitidas ao computador. A Figura 3 apresenta o fluxo de processamento adotado pelo sistema.

**Figura 3 – Fluxo de processamento**

![Fluxo de processamento](images/Fluxo%20de%20processamento.png)

A flexão dos dedos é utilizada para acionar comandos de interação, como os cliques dos botões do mouse. Para isso, as leituras dos *Flex Sensors* são comparadas a limiares previamente definidos, permitindo reconhecer a flexão correspondente a cada comando. O mapeamento dos gestos estabelece a relação entre os movimentos físicos realizados pelo usuário e as ações executadas no computador, conforme apresentado na Figura 4.

**Figura 4 – Mapeamento de gestos**

![Mapeamento de gestos](images/Mapeamento%20de%20gestos.png)

Para que a comparação experimental entre a *data glove* e o mouse óptico seja válida, os dois dispositivos devem oferecer funcionalidades equivalentes nas tarefas avaliadas. Além da movimentação do cursor e dos cliques, essa equivalência deve contemplar o clique e arraste e a rolagem, implementados por meio de gestos definidos para a luva. No caso do arraste, é necessário manter o botão lógico pressionado durante a movimentação do cursor e liberá-lo ao término do gesto. Para a rolagem, deve-se inclinar a mão em noventa graus, ou, em outras palavras, virar a palma da mão, que normalmente fica na horizontal, para a vertical, deixando-a apontada para a esquerda. Nessa posição, o sistema entende que está na função de rolagem. A movimentação é mantida seguindo a mesma lógica de inclinação, com um ajuste na tradução da inclinação, pois o que antes era cima e baixo passa a ser esquerda e direita, e vice-versa, para permitir um movimento intuitivo por parte do usuário. Quanto à função dos cliques, o que antes realizava a função de clique passa a controlar a rolagem, sendo o clique esquerdo para cima e o clique direito para baixo. Para sair do modo de rolagem, é necessário apenas voltar a mão para a posição horizontal usual.

Após a montagem e a integração dos componentes, foi obtido o protótipo físico da *data glove*, apresentado nas Figuras 5 e 6. As imagens permitem visualizar a disposição dos sensores e do sistema eletrônico na luva, evidenciando a implementação física do projeto descrito nos diagramas anteriores.

**Figura 5 – Protótipo da data glove na posição horizontal**

![Data glove na posição horizontal](images/Glove%20Horizontal.jpeg)

**Figura 6 – Protótipo da data glove na posição vertical**

![Data glove na posição vertical](images/Glove%20Vertical.jpeg)

