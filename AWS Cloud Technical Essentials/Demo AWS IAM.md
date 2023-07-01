vamos criar a função de IAM para o nosso aplicativo de diretório de funcionários e também veremos como criar usuários, e as diferentes chaves de acesso do AWS, que são usadas para acesso programático às APIs do AWS.
![[Pasted image 20230629201306.png]]
# __
![[Pasted image 20230629201704.png]]
Para começar, vamos criar a função para o nosso aplicativo selecionando Roles na navegação à esquerda do painel do IAM, e, em seguida, clicaremos em Create role (Criar função).
# __
![[Pasted image 20230629201809.png]]
Nessa página, precisamos selecionar qual é o tipo de entidade confiável para assumir essa função. Sabemos que as funções permitem que você obtenha acesso a credenciais temporárias que são usadas para fazer chamadas para as chamadas de API da AWS. É importante certificar-se de que está restringindo quem pode assumir essa função. Não é qualquer um que pode assumir essa função, certo? Então, no tipo de entidade confiável , temos o serviço da AWS.
##### AWS Service
Um serviço da AWS seria algo como uma instância do EC2, uma função Lambda, outros serviços que estão assumindo uma função para fazer chamadas à API da AWS.
##### AWS Account
Você pode ter uma conta da AWS, isso permitiria que você permitisse o acesso entre contas às permissões dos recursos da sua conta.
##### Web Identity
Você também pode selecionar uma identidade da Web, que permitiria que os usuários federados assumissem uma função.
##### SAML 2.0 federation
Você tem uma federação SAML 2.0, portanto, se tiver um diretório corporativo que esteja no local e que use SAML, você pode usá-lo como seu tipo de entidade confiável ou pode criar uma política de Confiança personalizada.
# __
![[Pasted image 20230629202258.png]]
Vamos selecionar o serviço AWS para esse e, em seguida, selecionar EC2, já que nosso aplicativo de diretório de funcionários será executado no EC2. Em seguida, podemos selecionar o botão Next (Avançar) e seremos levados à página Add permissions (Adicionar permissões).
# __
![[Pasted image 20230629202349.png]]
Isso lista as diferentes políticas de permissões que estão no IAM, e, no momento, está puxando as políticas gerenciadas da AWS que existem nessa conta por padrão. E o que é uma política gerenciada é uma política criada e gerenciada pela AWS,  o que quero dizer com isso é: Vamos dar uma olhada na política para o S3.
# __
![[Pasted image 20230629202516.png]]
![[Pasted image 20230629202542.png]]
então, se eu digitar S3 na barra de pesquisa e pressionar Enter, vou expandir essa política de acesso total do Amazon S3 e podemos ver o JSON, que são as permissões para essa política. Podemos ver que o efeito é Allow, que será Allow ou Deny. Não há outra opção além de Permitir ou Negar, e, em seguida, há a ação, que definirá quais chamadas à API da AWS podem ser feitas. Assim, podemos ver que temos S3:* e S3-object-lambda:* . Esse é um curinga para determinar todas as chamadas de API permitidas para esse serviço, e também temos o recurso aqui, que também está definido como "asterisco". Portanto, seriam todos os recursos do S3. Essa é uma política muito permissiva. No mundo real, é provável que o senhor queira alterá-la para permitir apenas as chamadas de API de que seu aplicativo precisa, nada mais, e apenas os recursos aos quais pretende relacionar essa política.
# __
![[Pasted image 20230629203005.png]]
Para isso, o senhor teria de criar uma política personalizada. Portanto, se eu rolar a tela para cima, o senhor poderá clicar nesse botão Política personalizada, que o levará a uma nova página onde poderá criar sua política personalizada.
# __
![[Pasted image 20230629203108.png]]
Por enquanto, usaremos as políticas gerenciadas da AWS e marcarei a caixa de seleção para AmazonS3FullAccess.
# __
![[Pasted image 20230629203144.png]]
E também vou digitar DynamoDB, e sair do filtro S3, e, em seguida, selecionar a política AmazonDynamoDBFullAccess aqui também.
# __
![[Pasted image 20230629203228.png]]
Porque, mais tarde no curso, vamos usar o DynamoDB como banco de dados para esse aplicativo. Portanto, para preparar a função, selecionei S3FullAccess e DynamoDBFullAccess.
# __
![[Pasted image 20230629203313.png]]
Agora vamos clicar em Next. Em seguida, podemos dar um nome a isso. Vou chamar de EmployeeWebApp, e depois vou rolar para baixo.
# __
![[Pasted image 20230629203403.png]]
Podemos ver as entidades confiáveis aqui, portanto, essa é nossa política de confiança. Estamos autorizando a chamada de API STS AssumeRole, e quem tem permissão para assumir essa função? ec2.amazonaws.com. Portanto, uma instância do EC2 terá permissão para assumir somente essa função.
# __
![[Pasted image 20230629203444.png]]
Muito bem, agora posso rolar para baixo e clicar em Create role.
# __
![[Pasted image 20230629203515.png]]
![[Pasted image 20230629203540.png]]
Depois que a função for criada, o senhor poderá clicar na função
# __
![[Pasted image 20230629203622.png]]
o que o levará à página , onde poderá ver as informações sobre essa função, como o ARN, o Amazon Resource Name, e também poderá rolar para baixo, para ver as permissões anexadas,
# __
![[Pasted image 20230629203635.png]]
e poderá adicionar novas permissões, se quiser.
# __
![[Pasted image 20230629203755.png]]
É possível simular as permissões
# __
![[Pasted image 20230629203832.png]]
visualizar as relações de confiança
# __
![[Pasted image 20230629203925.png]]
visualizar também as tags associadas, que são pares de valores-chave.
# __
![[Pasted image 20230629203943.png]]
Portanto, é aqui que o senhor pode obter todas as informações sobre a sua função e gerenciá-la. A seguir, quero criar um usuário.
# __
![[Pasted image 20230629204039.png]]
Então, vou clicar em users (usuários) na navegação à esquerda

![[Pasted image 20230629204051.png]]
e depois em Add users (adicionar usuários)

![[Pasted image 20230629204100.png]]
e vamos dar um nome a esse usuário. Digamos que seja EC2Admin.

![[Pasted image 20230629210153.png]]
e depois quero clicar na caixa de seleção para habilitar o acesso ao console.

![[Pasted image 20230629211615.png]]
Isso significa que quero permitir que esse usuário possa fazer login no console de gerenciamento do AWS. Observe que, por padrão, essa opção estava desmarcada, o que significa que o fato de criar um usuário não significa que ele tenha acesso ao console. Vou marcar essa opção, e, em seguida, vou permitir que seja criada uma senha gerada automaticamente, e, em seguida, quero deixar marcada a caixa de seleção para que os usuários criem uma senha no próximo login. Isso permitirá que eles alterem a senha assim que fizerem login pela primeira vez. Agora, vamos clicar em Next (Avançar)
# __
![[Pasted image 20230629211711.png]]
Em seguida, o que quero fazer, é adicionar os usuários a um grupo. No momento, não temos nenhum grupo, portanto, vou clicar em Create group (Criar grupo)

![[Pasted image 20230629211843.png]]
Em seguida, o que quero fazer é adicionar um nome de grupo. Digamos que seja EC2Admins

![[Pasted image 20230629211906.png]]
Em seguida, quero anexar uma política a esse grupo, porque sabemos que é uma prática recomendada anexar políticas a grupos, não a usuários diretamente.

![[Pasted image 20230629212151.png]]
Então, vou selecionar a política AmazonEC2FullAccess, e, em seguida, vou rolar para baixo e clicar em Create user group.

![[Pasted image 20230629212236.png]]
E agora posso selecionar esse grupo de usuários para adicionar esse usuário.

![[Pasted image 20230629212318.png]]
Em seguida, posso clicar em next

![[Pasted image 20230629214732.png]]
Então, podemos rolar para baixo. Podemos ver as permissões que esse usuário tem atualmente. Ele herdará as permissões do grupo EC2Admins, e também terá diretamente anexada a ele a permissão IAMUserChangePassword, que permitirá que esse usuário altere sua senha. Portanto, agora podemos clicar em Create user

![[Pasted image 20230629225429.png]]
e podemos seguir em frente e clicar em Return to users list.

![[Pasted image 20230629230211.png]]
Não baixamos a senha para esse usuário, tudo bem. Não pretendo usar esse usuário. É apenas para fins de demonstração, Portanto, vamos clicar em Continue (Continuar).

![[Pasted image 20230629230301.png]]
e agora, se eu clicar nesse usuário

![[Pasted image 20230629230337.png]]
É apenas para fins de demonstração, Portanto, vamos clicar em Continue (Continuar), e agora, se eu clicar nesse usuário, o que quero fazer a seguir é clicar em na guia Security Credentials (Credenciais de segurança)

![[Pasted image 20230629230419.png]]
e, se rolarmos a tela para baixo, os senhores poderão ver que temos esse painel aqui chamado Access keys (Chaves de acesso). As chaves de acesso permitirão que seus usuários façam chamadas programáticas para a AWS usando coisas como a linha de comando da AWS, os kits de desenvolvimento de software da AWS, onde talvez estejam desenvolvendo localmente em seus laptops, e precisam que seu código seja capaz de entrar em contato com a AWS

![[Pasted image 20230629230530.png]]
Então, vou criar uma chave de acesso aqui

![[Pasted image 20230629230604.png]]
![[Pasted image 20230629230621.png]]
Em seguida, quero usar isso para a linha de comando, e, em seguida, vou clicar na caixa de seleção para "I understand the above recommendation." O que isso está dizendo é: "Ei, há outro serviço no navegador que o senhor pode usar para usar a CLI do AWS, chamado AWS CloudShell." Vamos criar as chaves de acesso de qualquer forma. Vou marcar essa caixa de seleção e clicar em Next (Avançar)

![[Pasted image 20230629230745.png]]
E depois clicar em Next (Avançar) novamente, e clicar em Create access key (Criar chave de acesso).

![[Pasted image 20230629230835.png]]
Tudo bem, então aqui o senhor pode ver, que temos nossa chave de acesso, e depois temos nossa chave de acesso secreta, que não está sendo mostrada no momento nesta página, mas o senhor pode clicar em mostrar e copiá-la, e usar essa chave de acesso e a chave de acesso secreta para poder configurar a linha de comando localmente. Agora vou clicar em Done (Concluído)

![[Pasted image 20230629230932.png]]
e depois em Continue (Continuar).

![[Pasted image 20230629231010.png]]
![[Pasted image 20230629231040.png]]

![[Pasted image 20230629231115.png]]
![[Pasted image 20230629231131.png]]
![[Pasted image 20230629231141.png]]
Então, agora, para uma pequena limpeza, vou selecionar Actions (Ações) e depois vou clicar em Deactivate (Desativar) e depois em Deactivate (Desativar), e depois vou clicar em Actions (Ações) e depois em Delete (Excluir), e depois podemos copiar e colar o ID da chave de acesso aqui, e depois clicar em Delete (Excluir).