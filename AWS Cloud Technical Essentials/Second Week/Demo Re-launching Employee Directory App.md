vamos criar uma VPC, criar quatro sub-redes, criar uma tabela de rotas para as sub-redes públicas, e, em seguida, vamos anexar um gateway de Internet à VPC e relançar o aplicativo de diretório de funcionários na nova VPC. 
# __
![[Pasted image 20230706110805.png]]
Assim, os senhores podem ver primeiro que estou no painel da VPC aqui, e vou clicar em Create VPC. 
# __
![[Pasted image 20230706112707.png]]
Agora quero selecionar, este é um assistente que vai ajudá-los a criar suas VPCs, suas sub-redes, coisas assim. Por enquanto, vou criar apenas a VPC. 
# __
![[Pasted image 20230706112815.png]]
Portanto, vou selecionar VPC only (somente VPC), e vou dar um nome a essa VPC. Vamos chamá-la de app-vpc. E depois quero inserir o intervalo CIDR para essa VPC. Para fazer isso, vou dar ao intervalo CIDR o valor 10.1.0.0/16. E depois vou rolar para baixo e clicar em Create VPC. 
# __
![[Pasted image 20230706112840.png]]
Agora que temos nossa VPC, a próxima coisa que quero fazer é criar as sub-redes. 
# __
![[Pasted image 20230706112903.png]]
Agora vou selecionar as sub-redes na navegação à esquerda e depois vou clicar em Create subnet. 
# __
![[Pasted image 20230706112940.png]]
Em seguida, selecionaremos uma VPC para isso. E selecionaremos a VPC que acabamos de criar, app-vpc. 
# __
![[Pasted image 20230706113028.png]]
E agora, para a nossa primeira sub-rede. Daremos a ela um nome, Public Subnet 1. E, em seguida, selecionaremos a zona de disponibilidade que será us-west-2a. E, em seguida, daremos a ela um intervalo CIDR que será 10.1.1.0/24. E, em seguida, podemos adicionar nossa próxima sub-rede. 
# __
![[Pasted image 20230706113110.png]]
Portanto, teremos uma sub-rede pública e uma privada em cada zona de disponibilidade. Portanto, criaremos a nossa sub-rede privada em seguida. Portanto, Sub-rede privada 1, zona de disponibilidade , a mesma us-west-2a. 
# __
![[Pasted image 20230706113156.png]]
E, em seguida, fornecendo o intervalo CIDR, diremos que é 10.1.2.0/24. E agora podemos adicionar nossas sub-redes à outra zona de disponibilidade. 
# __
![[Pasted image 20230706113252.png]]
Portanto, esta será a Public Subnet 2. E, desta vez, vamos dizer que queremos colocá-la em us-west-2b. E, para o intervalo de sub-rede, podemos dizer 10.1.3.0/24. 
# __
![[Pasted image 20230706113355.png]]
E, por fim, criaremos mais uma sub-rede , que será a Sub-rede Privada 2. E, selecionando a zona de disponibilidade, diremos que é us-west-2b, e daremos a ela o intervalo CIDR de 10.1.4.0/24. Assim, os senhores podem ver que temos, se eu rolar de volta para o topo, quatro sub-redes diferentes sendo criadas com intervalos CIDR não sobrepostos. Todos esses intervalos CIDR são um subconjunto do intervalo CIDR que criamos para nossa VPC. Portanto, temos 10.1.1.0, 10.1.2.0, 10.1.3.0 e 10.1.4.0. Muito bem, agora podemos ir em frente e clicar em Create subnet e isso criará todas as quatro. 
# __
![[Pasted image 20230706113429.png]]
Muito bem, agora temos quatro sub-redes, Public Subnet 1 e 2 e Private Subnet 1 e 2. Em seguida, quero criar um gateway de Internet. 
# __
![[Pasted image 20230706113455.png]]
Portanto, selecionarei gateways de Internet na navegação à esquerda e clicarei em Create internet gateway. 
# __
![[Pasted image 20230706113520.png]]
Daremos um nome a ele. Digamos que seja app-igw e clicaremos em Create internet gateway. 
# __
![[Pasted image 20230706113538.png]]
Em seguida, podemos voltar à página de gateways de Internet , onde podemos visualizar todos os nossos gateways de Internet. 
# __
![[Pasted image 20230706113606.png]]
Atualmente, temos um gateway de Internet anexado à nossa VPC padrão. O que queremos fazer é selecionar o novo gateway de Internet que acabamos de criar 
![[Pasted image 20230706113633.png]]
e anexá-lo a uma VPC. 
# __
![[Pasted image 20230706113648.png]]
Em seguida, selecionaremos nossa VPC de aplicativo e clicaremos em Attach to internet gateway. 
# __
![[Pasted image 20230706113725.png]]
Para gateways de Internet e um gateway de Internet só pode ser anexado a uma VPC. Portanto, é uma relação de um para um. Muito bem, o próximo passo a ser dado é configurar nossas tabelas de rota. Para isso, vou clicar em route tables na navegação à esquerda. 
# __
![[Pasted image 20230706113814.png]]
E os senhores podem ver que já temos duas tabelas de rotas. Temos as principais tabelas de rotas para ambas as VPCs, nossa VPC padrão e nossa app-vpc, que podemos rolar para a direita , expandir e ler essa VPC. Essa é a nossa app-vpc. Agora, rolando de volta, vou clicar em create route table (criar tabela de rotas) e daremos um nome a essa tabela de rotas. 
# __
![[Pasted image 20230706113900.png]]
Salvaremos public-route-table. E quero associá-la à nossa app-vpc e clicar em Create route table (criar tabela de rotas). 
# __
![[Pasted image 20230706113932.png]]
Agora temos uma tabela de rotas criada , mas queremos adicionar uma rota que permita qualquer sub-rede que tenha essa tabela de rotas associada a ela. 
# __
![[Pasted image 20230706114002.png]]
![[Pasted image 20230706114034.png]]Queremos adicionar uma rota que permita o tráfego da Internet, 0.0.0.0/0. Para onde? O gateway da Internet. 
# __
![[Pasted image 20230706114103.png]]
E o gateway da Internet que queremos escolher é aquele que acabamos de criar e, em seguida, clicamos em Save changes (Salvar alterações). 
# __
![[Pasted image 20230706114150.png]]
Agora, voltando para baixo, ainda não terminamos. Agora, o que temos de fazer é associar essas sub-redes a essa tabela de rotas. Então, vou clicar em Subnet associations (Associações de sub-rede) e, rolando para baixo, podemos ver que, no momento, temos essa associada a nenhuma sub-rede. 
# __
![[Pasted image 20230706114211.png]]
Vou clicar em Edit subnet associations (Editar associações de sub-rede) 
![[Pasted image 20230706114250.png]]
e selecionar apenas nossas duas primeiras sub-redes públicas. Portanto, não há nada inerente a uma sub-rede que a torne pública ou privada. A única coisa que a torna pública ou privada é se ela tem ou não uma associação de tabela de rotas que inclua uma rota dessa sub-rede para o gateway da Internet. Tudo bem, então vamos em frente e clicar em Save associations aqui. 
# __
![[Pasted image 20230706114340.png]]
E então podemos rolar para baixo, clicar na guia subnet association, 
![[Pasted image 20230706114403.png]]
e agora podemos ver que temos nossas duas sub-redes públicas associadas a essa tabela de rotas. 
# __
![[Pasted image 20230706114440.png]]
E então, novamente, revisando as rotas, clicando novamente na guia routes. Podemos ver que temos nossa rota local e nossa rota para a Internet por meio do gateway da Internet. 
# __
![[Pasted image 20230706114512.png]]
Agora, o último passo é relançar nosso aplicativo de diretório de funcionários. Então, vou navegar até o console do EC2. 
# __
![[Pasted image 20230706115243.png]]
A partir daqui, vou clicar no link de instâncias, 
![[Pasted image 20230706115313.png]]
e podemos ver que temos nosso aplicativo de diretório de funcionários ainda em execução. E se eu selecioná-lo, posso rolar para baixo e ver onde ele está sendo executado, que é nosso VPC padrão.
# __
![[Pasted image 20230706121654.png]]
Então, o que vou fazer é manter essa opção marcada e, em seguida, selecionar ações e, depois, Imagem e modelos. E, em seguida, selecionar Iniciar mais assim. 
# __
![[Pasted image 20230706121720.png]]
E o que isso faz é levá-lo a uma página que tem muitas das configurações para essa instância original pré-preenchidas aqui, para que o senhor não precise acessar e selecionar novamente todas as configurações. Assim, podemos ver em que temos o Employee Directory App pré-preenchido. 
# __
![[Pasted image 20230706121758.png]]
Vou chamar isso de Employee Directory App 2. 
# __
![[Pasted image 20230706121822.png]]
Podemos ver que temos o Linux 2 AMI selecionado aqui 
![[Pasted image 20230706121845.png]]
e também temos o t2.micro selecionado. 
# __
![[Pasted image 20230706121907.png]]
Para o par de chaves, temos de selecionar que queremos prosseguir sem um par de chaves novamente. 
# __
![[Pasted image 20230706122012.png]]
E aqui, em configurações de rede , é onde faremos a maioria das alterações. Vamos selecionar o novo app-vpc que acabamos de criar, e, em seguida, vamos selecionar em qual sub-rede pública queremos iniciar, Public Subnet 1 ou Public Subnet 2. Vamos selecionar a sub-rede pública 1. 
# __
![[Pasted image 20230706122047.png]]
E também vamos garantir que esse IP público atribuído automaticamente esteja definido como ativado, o que é o caso. 
# __
![[Pasted image 20230706122211.png]]
Agora, rolando para baixo, os senhores podem ver que podemos selecionar nosso grupo de segurança. No momento, temos o grupo de segurança que foi criado anteriormente associado a essa instância e está dando um erro dizendo que não podemos usar o grupo de segurança com essa sub-rede. Isso ocorre porque o grupo de segurança está vinculado à VPC. Portanto, precisamos criar um novo grupo de segurança que será associado a essa nova VPC, não à VPC padrão. Portanto, o que queremos fazer aqui é clicar em Create security group e, 
![[Pasted image 20230706122325.png]]
em seguida, deixaremos o nome como padrão 
![[Pasted image 20230706122439.png]]
e faremos a mesma coisa que fizemos com o quando criamos o grupo de segurança original, ou seja, 
![[Pasted image 20230706122503.png]]
queremos permitir o tráfego HTTP na porta 80 da Internet e adicionar uma segunda regra, 
![[Pasted image 20230706122526.png]]
para permitir o tráfego HTTPS na porta 443 de qualquer lugar. 
# __
![[Pasted image 20230706122554.png]]
Agora, rolando para baixo, podemos rolar para baixo até os detalhes avançados e expandir isso aqui. Podemos ver que a função foi preenchida previamente, o que é ótimo. E, se rolarmos para baixo mais um pouco, vamos dar uma olhada nos dados do usuário. 
# __
![[Pasted image 20230706122655.png]]
Podemos ver que eles também estão pré-preenchidos. 
# __
![[Pasted image 20230706122710.png]]
Agora podemos clicar em Launch instance (Iniciar instância). 
# __
![[Pasted image 20230706122740.png]]
Podemos clicar no ID da instância, ver que ela está no estado pendente. 
# __
![[Pasted image 20230706125625.png]]
Agora vamos aguardar alguns minutos e voltar para tentar acessá-la por meio desse endereço IP público. E se conseguirmos acessá-lo, significa que todas as nossas configurações de rede foram configuradas corretamente. 
# __
![[Pasted image 20230706125700.png]]
Certo, agora estamos de volta e podemos ver que as instâncias estão em estado de execução. 
# __
![[Pasted image 20230706133449.png]]
Se copiarmos esse endereço IP 
![[Pasted image 20230706133555.png]]
e o colarmos em uma nova guia fora da tela, e arrastarmos essa guia para cima, veremos que agora podemos acessar o aplicativo Employee Directory no endereço IP da nova instância que foi iniciada em nosso novo app-vpc.
# __