Já criamos e modificamos o aplicativo e criamos e testamos o upload para o bucket S3. Portanto, para que o aplicativo esteja totalmente funcional, ou em um estágio totalmente funcional, a próxima coisa a fazer é iniciar um banco de dados. Mas antes de iniciar o banco de dados, quero iniciar uma instância que esteja pronta para usar esse banco de dados para que possamos testá-lo assim que estiver pronto. 
# __
![[Pasted image 20230707185009.png]]
Portanto, para iniciar essa instância, vou acessar o EC2. 
# __
![[Pasted image 20230707185039.png]]
E ir até as instâncias. E, assim como da última vez, vou usar o atalho em que lanço um clone de uma instância que já foi lançada. Então, para fazer isso, vou selecionar meu employee-directory-app-s3, porque essa é a versão mais atualizada desse aplicativo. 
# __
![[Pasted image 20230707185112.png]]
E, em seguida, vou para ações, imagem e modelos. E, em seguida, vou iniciar mais assim.
# __
![[Pasted image 20230707185156.png]]
Agora que estou na página de lançamento, o que quero fazer, apenas para saber que estou na instância correta e que estou usando a instância correta. Em vez de anexar -s3 a isso, vou anexar -dynamodb para que eu saiba que essa é a instância do aplicativo que está testando com o banco de dados e não apenas se conectando ao bucket. 
# __
![[Pasted image 20230707185247.png]]
Agora que ajustei isso, posso rolar para baixo. Vejo que a maioria das minhas configurações ainda está lá. Quero ter certeza de que ainda estou usando a mesma chave caso precise acessar a instância. 
# __
E também quero apenas verificar, mesmo sabendo que isso funciona, quero apenas verificar se ainda estou usando a função. Outra coisa que quero ter certeza de fazer é garantir que a instância seja iniciada com um IP público. E rolei para a direita sobre isso. 
# __
![[Pasted image 20230707185347.png]]
Então, rolando para trás, vou para as configurações de rede e para o IP público atribuído automaticamente, e me certifico de clicar em Enable (Ativar). Dessa forma, a instância terá um IP público, e eu poderei acessá-lo e testá-lo assim que a instância e o banco de dados forem totalmente iniciados. 
# __
![[Pasted image 20230707185413.png]]
Portanto, agora que fiz isso, posso ver que meus dados de usuário estão exatamente onde os deixei depois de adicionar o bucket. 
# __
![[Pasted image 20230707185441.png]]
E agora posso clicar em Launch instance (Iniciar instância).
# __
![[Pasted image 20230707185505.png]]
Como sempre, dê um tempo para que ela seja iniciada. E posso ir até as instâncias e, ocasionalmente, atualizá-las para ter certeza de que minha instância foi iniciada. Portanto, vou aguardar alguns minutos enquanto espero que a instância seja iniciada e me certifico de que onde atualmente está escrito "Initializing" (Inicializando), estará escrito "2/2 checks passed" (2/2 verificações aprovadas)."
# __
![[Pasted image 20230707185600.png]]
Posso ver que duas das duas verificações foram aprovadas.
# __
![[Pasted image 20230707185614.png]]
Então, vou selecionar minha instância rotulada como dynamodb e copiar seu endereço IP público, só porque quero ter certeza de que o aplicativo está em funcionamento antes de prosseguir. 
# __
![[Pasted image 20230707185640.png]]
Se não estivesse em execução, como podemos ver que está, se não estivesse, então eu voltaria e veria onde cometi um erro ao iniciar a instância. E assim que o aplicativo estivesse em execução com sucesso, então eu seguiria em frente com a criação do banco de dados. 
# __
![[Pasted image 20230707185710.png]]
Como posso ver que o aplicativo de diretório básico de funcionários está funcionando, posso prosseguir com a criação da tabela do DynamoDB. 
# __
![[Pasted image 20230707185742.png]]
Para fazer isso, vou até a barra de pesquisa, digito dynamo e clico no serviço DynamoDB. 
# __
![[Pasted image 20230707185806.png]]
E, quando estiver aqui, vou em frente e clico em Create table (Criar tabela). Como não tenho nenhuma tabela em execução no momento, é a maneira mais fácil de chegar a essa tela de criação de tabela. 
# __
![[Pasted image 20230707185837.png]]
Para o nome da tabela, vou colocar Employees porque o aplicativo está configurado para trabalhar com um banco de dados chamado Employees. Portanto, isso facilitará muito a utilização dessa chave. 
# __
![[Pasted image 20230707185912.png]]
E, para a chave de partição, vou colocar id. E isso porque, novamente, o aplicativo está configurado para utilizá-la para a organização dentro da tabela. E, então, vou manter esse tipo como uma string. 
# __
![[Pasted image 20230707185936.png]]
Depois de fazer isso, todas as configurações padrão podem permanecer, e vou clicar em Create table (Criar tabela). E isso leva apenas um pouco de tempo, e a tabela será criada em pouco tempo. Portanto, vou esperar alguns segundos. 
# __
![[Pasted image 20230707190028.png]]
A tabela foi criada com sucesso. Agora que a tabela foi criada, em vez de adicionar itens diretamente a essa tabela, o que quero fazer é testar o aplicativo novamente. 
# __
![[Pasted image 20230707190111.png]]
Portanto, vou copiar o endereço IP público da minha instância.
# __
![[Pasted image 20230707190146.png]]
Então, vou até minhas instâncias e selecionarei a instância que foi iniciada para isso e copiarei seu endereço IP. 
# __
![[Pasted image 20230707190225.png]]
E, em seguida, em uma nova guia, vou colar esse endereço. E posso ver que o aplicativo Employee Directory ainda está em execução e, no momento, é um diretório vazio. Mas posso ir em frente e adicionar um funcionário a esse diretório só para ter certeza de que tudo está conectado. 
# __
![[Pasted image 20230707190244.png]]
Então, o que farei é clicar em Add. 
# __
![[Pasted image 20230707190334.png]]
E vou colocar meu nome aqui, e, em seguida, minha localização, e meu cargo. Também selecionarei algumas dessas opções aqui, para que possamos ver como fica à medida que tudo é adicionado a essa tabela e a esse diretório. Portanto, como sou morador de Seattle, também sou fã de Seattle, e definitivamente sou um esnobe do café. Também não vou apenas colocar essas informações na tabela, mas vou adicionar um arquivo. Vou adicionar a foto do meu funcionário e abri-la. 
# __
![[Pasted image 20230707190418.png]]
E depois que tudo isso tiver sido adicionado, posso ir em frente e clicar em Salvar. 
# __
![[Pasted image 20230707190440.png]]
E, como podemos ver, agora tenho uma entrada no Employee Directory. E podemos ver que agora estou no diretório. Mas quero mostrar que isso não é apenas algo que foi adicionado a esse local. Portanto, o que farei é mostrar que esses itens foram adicionados na tabela e no bucket do S3. 
# __
![[Pasted image 20230707191206.png]]
Então, começando pelo S3, irei para o S3.
# __
![[Pasted image 20230707191227.png]]
E, em seguida, abrirei o bucket que criei. E, como podemos ver, minha foto de funcionário foi adicionada, e é a foto de funcionário que carreguei. Embora tenha seu próprio nome designado aqui, esse é o objeto que foi carregado por meio desse aplicativo. 
# __
![[Pasted image 20230707191428.png]]
E também posso acessar o DynamoDB, 
![[Pasted image 20230707191511.png]]
visualizar minha tabela de funcionários, e explorar os itens da tabela. 
# __
![[Pasted image 20230707193500.png]]
E também posso ver que os itens dos meus funcionários que foram adicionados por meio do diretório estão aqui. 
# __
![[Pasted image 20230707193541.png]]
Mostra quais crachás associei a mim mesmo, meu nome, meu cargo, minha localização. Mostra o nome do objeto que foi carregado por meio do diretório, e mostra o ID específico dessa tabela, e a chave de partição que estabelecemos. 
# __
![[Pasted image 20230707193642.png]]
Portanto, agora que tudo isso foi feito, o que quero fazer é seguir em frente e manter a tabela em execução. 
# __
![[Pasted image 20230707194202.png]]
Mas quero voltar ao EC2 e interromper a instância para que eu não acumule nenhuma cobrança adicional enquanto me preparo para passar para o próximo estágio do desenvolvimento da infraestrutura do aplicativo. 
# __
![[Pasted image 20230707194231.png]]
Portanto, vou parar essa instância, e é aí que vou encerrar este passo a passo. E vejo os senhores no próximo.