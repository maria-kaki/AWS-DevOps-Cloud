Olá a todos. Vamos iniciar o aplicativo de diretório de funcionários em uma instância do Amazon EC2 usando o VPC padrão.
# __
![[Pasted image 20230701133507.png]]
![[Pasted image 20230701133541.png]]
Assim, os senhores podem ver que já estou no console da AWS e vou navegar até o painel do EC2.
# __
![[Pasted image 20230701133617.png]]
A partir daqui, quero iniciar uma nova instância. Então, vou selecionar launch instance e, em seguida, selecionar launch instance novamente.
# __
![[Pasted image 20230701133846.png]]
E agora isso nos leva a uma página em que podemos fornecer as configurações para nossa instância do EC2.
# __
![[Pasted image 20230701133945.png]]
Vou dar um nome a isso, employee directory app e, em seguida, podemos rolar para baixo e ver qual AMI queremos escolher.
# __
![[Pasted image 20230701134112.png]]
A AMI é a imagem da máquina da Amazon e é um modelo que contém a configuração de software para sua instância na inicialização como o sistema operacional, qualquer tipo de servidor de aplicativos ou quaisquer aplicativos que você queira ter pré-instalados quando iniciar sua instância. Vamos usar a AMI do Amazon Linux 2023 para isso, embora o senhor possa navegar no marketplace da AWS para ter acesso aos diferentes tipos de AMIs que os fornecedores oferecem. Portanto, se estiver usando algum tipo de software de terceiros que deseja lançar em uma instância do EC2, eles podem ter uma AMI disponível que o senhor pode usar para simplificar um pouco a sua vida. O senhor também pode criar e gerenciar suas próprias AMIs e compartilhá-las internamente dentro de sua organização para dizer que só pode iniciar uma instância do EC2 usando uma de nossas AMIs aprovadas que podem ter alguma segurança específica ou pacotes de conformidade pré-instalados. Essa é outra opção.
# __
![[Pasted image 20230702202830.png]]
Então, deixando a AMI do Amazon Linux 2023 selecionada , vou rolar para baixo e, em seguida, podemos selecionar nosso tipo de instância. O tipo de instância determinará quanta CPU, quanta memória, que tipos de hardware estão disponíveis para o senhor nessa instância. Algumas instâncias vêm com uma GPU, por exemplo. Nesse caso, vamos usar o tipo de instância EC2 elegível de camada livre, T2 micro que é o padrão selecionado. Portanto, vamos deixar isso como está.
# __
![[Pasted image 20230702203628.png]]
Em seguida, podemos rolar para baixo e selecionar se queremos usar um par de chaves. O par de chaves permitirá que o senhor tenha acesso a essa instância fazendo algo como SSH. Vou selecionar prosseguir sem um par de chaves porque, se eu precisar me conectar a essa instância, usarei o botão de conexão no console da AWS, onde não preciso ter um par de chaves para me conectar a essa instância para visualizar coisas como logs.
# __
![[Pasted image 20230702204104.png]]
Em seguida, rolando para baixo mais um pouco podemos definir nossas configurações de rede. Isso está usando uma VPC padrão e uma sub-rede padrão. Essa VPC padrão terá sub-redes que têm acesso à Internet, o que significa que há um gateway de Internet anexado a essa VPC que permite que o tráfego da Internet flua para essa VPC padrão. Os senhores aprenderão mais sobre VPCs daqui a pouco, mas entendam que essa VPC padrão permite o acesso público à Internet , o que é bom para o nosso caso de uso, mas pode não ser ótimo para outros casos de uso em que os senhores provavelmente colocariam a instância atrás de algo como um balanceador de carga e usariam sub-redes privadas. Mas queremos poder acessar essa instância diretamente. Então, com isso em mente, vamos usar a VPC padrão e também vamos deixar esse IP público atribuído automaticamente para ativar e isso permitirá que nossos incidentes de EC2 tenham um endereço IP acessível publicamente assim que forem iniciados. Em seguida, rolando um pouco mais para baixo, temos de configurar nosso firewall. Esse será nosso grupo de segurança. Os grupos de segurança são firewalls no nível da instância. Queremos desativar o tráfego de SSH porque não vamos precisar dele.
# __
![[Pasted image 20230702204329.png]]
Em seguida, vamos permitir HTTPS e HTTP. Em nosso aplicativo, vamos usar HTTP diretamente.
# __
![[Pasted image 20230702204424.png]]
Em seguida, rolando para baixo, podemos configurar algum armazenamento. Vamos deixar nosso volume raiz aqui, as não vamos adicionar mais nenhum volume EBS.
# __
![[Pasted image 20230702204558.png]]
Em seguida, podemos expandir a seção de detalhes avançados e precisamos selecionar um perfil de instância de IM. Nesse caso, selecionarei a função employee web app e essa função tem permissões anexadas para permitir que quem estiver usando a função faça chamadas para o S3 ou para o Dynamo DB. Sabemos que nosso aplicativo tem algum código em execução que fará chamadas de API para o S3 e o Dynamo DB. Precisamos permitir que o SDK do AWS tenha acesso a essas credenciais, e a maneira de fazer isso é por meio do perfil da instância IM. Portanto, estamos associando essa função ao perfil da instância que permitirá que nosso código tenha acesso a essas credenciais temporárias.
# __
![[Pasted image 20230702205112.png]]
![[Pasted image 20230702205133.png]]
Em seguida, rolando mais um pouco para baixo, chegaremos à seção de dados do usuário, e é aqui que o senhor pode fornecer um script bash que será executado na inicialização. Portanto, esse script aqui é o que será usado para baixar e instalar nosso aplicativo. Nosso aplicativo foi escrito em Python usando Flask como servidor da Web, e esse será o para nosso aplicativo de diretório de funcionários. Portanto, na primeira linha, estamos apenas declarando que se trata de um script Bash. Em seguida, estamos usando o Wget para baixar um arquivo zip do S3. Assim, hospedamos o arquivo zip em um bucket do S3 para que ele seja baixado. Em seguida, estamos descompactando o arquivo e mudando os diretórios para esse novo diretório. Em seguida, estamos usando o Yum para instalar o Python 3 e o PIP. Em seguida, estamos usando o PIP para instalar quaisquer dependências para nosso aplicativo Flask, que serão listadas em um arquivo chamado requirements.txt, que foi baixado desse arquivo zip. Em seguida, vamos instalar um pacote chamado stress. Esse pacote de stress será usado para simular um pico de CPU nessa instância, o que nos permitirá simular o escalonamento automático sempre que usarmos o escalonamento automático do Amazon EC2 em uma lição futura. Em seguida, temos três variáveis de ambiente diferentes. Uma para o nosso bucket de fotos, pois usaremos o S3 para armazenar nossas fotos. Ainda não temos esse valor, portanto, vamos deixar esse espaço reservado aqui. Temos a região padrão em que estamos operando do Oregon e, em seguida, temos nosso modo Dynamo em , o que significa que queremos que nosso aplicativo use o Dynamo DB e, em seguida, estamos executando esse aplicativo e hospedando-o na porta 80.
# __
![[Pasted image 20230702205402.png]]
![[Pasted image 20230702205442.png]]
Agora, podemos selecionar launch instance (iniciar instância) e isso começará a criar as diferentes coisas de que precisamos como nosso grupo de segurança e podemos ver que nossa instância foi iniciada.
# __
![[Pasted image 20230702220136.png]]
Agora, se eu selecionar esse ID de instância
# __
![[Pasted image 20230702221112.png]]
![[Pasted image 20230702223225.png]]
isso nos levará a uma página em que podemos selecionar nossa instância e visualizar algumas informações sobre ela. Podemos ver coisas como nosso endereço IP público , nosso endereço IP privado e nosso nome DNS público. Mas ainda não podemos acessar isso diretamente. Podemos ver que nosso estado instantâneo está em execução.
# __
![[Pasted image 20230702223251.png]]
Mas se eu atualizá-lo, os senhores poderão ver que temos algumas verificações de status que ainda estão sendo inicializadas. Quero esperar até que essas duas verificações de status sejam aprovadas.
# __
![[Pasted image 20230702223404.png]]
podemos ver que nosso estado instantâneo está em execução e que as verificações de status foram aprovadas.
# __
![[Pasted image 20230702223414.png]]
![[Pasted image 20230702223424.png]]
se eu selecionar essa instância novamente, poderemos abrir nosso endereço IP em uma nova guia.
# __
![[Pasted image 20230702223540.png]]
podemos ver que nosso aplicativo de diretório de funcionários foi aberto em uma nova guia e temos um diretório de funcionários vazio. Isso é exatamente o que esperaríamos neste momento , pois não temos um lugar para armazenar nossas fotos ou as informações dos funcionários com nosso bucket S3 ou tabela Dynamo DB. Vamos ver como criar uma rede personalizada para o bucket do S3 e a tabela do Dynamo DB e tornar tudo isso altamente disponível em uma próxima lição. Portanto, fique atento.
# __