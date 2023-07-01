![[Pasted image 20230629231706.png]]
Os senhores aprenderam um pouco do vocabulário da AWS, alguns dos conceitos por trás da computação em nuvem bem como algumas das especificidades em torno da identidade na nuvem e do gerenciamento de acesso. Para relembrar, vamos dar uma olhada no diagrama da arquitetura que construiremos. Os senhores se lembrarão de que é bastante complicado à primeira vista. Há muitos serviços diferentes trabalhando juntos para hospedar essa solução e, para que tudo isso seja construído dessa forma , será necessário algum tempo e compreensão. Os senhores terão a oportunidade de ver como cada peça é construída ao longo das próximas lições.
# __
![[Pasted image 20230629231802.png]]
O que quero fazer agora é mostrar a vocês como vamos hospedar nosso aplicativo de diretório de funcionários usando um serviço chamado Amazon EC2 que já foi mencionado em vídeos anteriores. Acho que a melhor maneira de explicar aos senhores como esses serviços funcionam é mostrar como eles funcionam.
# __
Portanto, o que vamos fazer é chamar o Seth aqui para iniciar uma instância do Amazon EC2 e hospedar o aplicativo de diretório de funcionários usando os padrões fornecidos pela AWS. A AWS fornece algo chamado VPC padrão , que é uma rede privada para seus recursos da AWS. Toda instância do EC2 que você iniciar usando o AWS deve estar dentro de uma rede. Portanto, para concluir esta demonstração com a quantidade limitada de informações que mostramos sobre os serviços do AWS, usaremos a rede padrão fornecida pelo AWS e aceitaremos a maioria dos valores padrão para iniciar uma instância do EC2.
# __
Usaremos o VPC padrão para iniciar essa primeira instância, e configuraremos o mínimo necessário para colocar nosso aplicativo em funcionamento.
# __
![[Pasted image 20230629234108.png]]
Já estou no console de gerenciamento do EC2 e vou navegar até o serviço Amazon EC2.
# __
![[Pasted image 20230629234147.png]]
Como Morgan já mencionou, o Amazon EC2 é um serviço de computação que permite hospedar máquinas virtuais. Você aprenderá muito sobre esse tópico em breve mas, por enquanto, vamos simplesmente criar uma instância do EC2 para tentar ajudá-lo a entender como usar os serviços da AWS sob demanda. 
# __
![[Pasted image 20230629234523.png]]
A partir daqui, lançaremos uma nova instância do EC2.
# __
![[Pasted image 20230630195107.png]]
![[Pasted image 20230630195126.png]]
Uma instância é o que chamamos de uma única máquina virtual. Agora temos que selecionar as configurações para essa instância do EC2. Mais tarde, os senhores examinarão essas configurações em detalhes.
# __
![[Pasted image 20230630195236.png]]
Podemos dar um nome a essa instância, Vou chamá-la de employee-web-app e, em seguida, selecionaremos as opções elegíveis da camada gratuita usando uma AMI do Linux ou Amazon Machine Image. E, em seguida, rolando para baixo até a próxima seção , selecionaremos a camada gratuita elegível t2.micro para o tipo de instância.
# __
![[Pasted image 20230630195325.png]]
Em seguida, normalmente precisamos selecionar um par de chaves. Isso seria usado para SSH na instância , mas não precisaremos fazer isso, portanto, selecionarei proceed without a key pair e continuarei rolando até as configurações de rede.
# __
![[Pasted image 20230630195406.png]]
Aqui selecionaremos a rede. Então, olhando para as configurações de rede, clicaremos em Edit.
# __
![[Pasted image 20230630195449.png]]
Em seguida, podemos selecionar o VPC e a sub-rede para essa instância. E, como discutimos anteriormente, usaremos o VPC padrão e deixaremos a sub-rede em No preference (Sem preferência).
# __
![[Pasted image 20230630195603.png]]
O VPC padrão tem configurações em vigor que facilitam muito esse processo de experimentação quando você está começando a usar o AWS. Novamente, definiremos todas essas coisas mais tarde.  
# __
![[Pasted image 20230630195659.png]]
Continuando com as configurações de rede, criaremos um novo grupo de segurança que é um firewall no nível da instância que permitirá que o tráfego HTTP e HTTPS chegue à instância. 
# __
![[Pasted image 20230630195755.png]]
![[Pasted image 20230630195830.png]]
Portanto, adicionaremos regras de entrada para ambos.
# __
![[Pasted image 20230630195851.png]]
Agora vamos rolar a tela para baixo e expandir os detalhes avançados.
# __
![[Pasted image 20230630195937.png]]
Aceitaremos a maioria dos padrões aqui exceto o perfil da instância do IAM e os dados do usuário para os quais forneceremos um valor. Para o perfil da instância do IAM, usaremos a função do IAM que será usada pelo aplicativo, embora isso só entre em ação mais tarde quando tivermos criado nosso bucket S3. Mas, por enquanto, vamos clicar no menu suspenso e selecionar essa função do IAM.
# __
![[Pasted image 20230630200025.png]]
![[Pasted image 20230630200043.png]]
Agora, rolando para baixo até os dados do usuário, esse é um script que será executado quando a instância for inicializada. Vamos em frente e colar nosso script de dados do usuário. Esse script fará o download do código-fonte do aplicativo, iniciará o servidor da Web e iniciará o código do aplicativo para que ele esteja pronto para começar a lidar com as solicitações.
# __
Embora o senhor pudesse ter iniciado a instância e, em seguida, conectado a ela via SSH, configurado e iniciado o aplicativo manualmente. Decidimos usar um script para automatizar esse processo no lançamento.
# __
![[Pasted image 20230630201648.png]]
Muito bem, agora podemos clicar em Launch instance (Iniciar instância). Pode levar alguns minutos para que a instância seja inicializada, portanto, vamos aguardar.
# __
![[Pasted image 20230630201803.png]]
![[Pasted image 20230630201918.png]]
E agora ela está em funcionamento.
# __
![[Pasted image 20230630202021.png]]
![[Pasted image 20230630202352.png]]
E agora ela está em funcionamento. Para acessar a instância, copie o endereço IP dos detalhes listados abaixo, cole-o em uma nova guia do navegador e pronto.
# __
![[Pasted image 20230630202446.png]]
Ela está em funcionamento e pronta para ser usada.
# __
Morgan, o que o senhor acha? - Parece ótimo Ficou ótimo. É exatamente o que eu esperaria nesse momento porque não há dados sendo fornecidos por um banco de dados portanto, espero ver apenas uma página inicial sem informações. Então, isso é ótimo. Obrigado, Seth, por nos orientar. Nas próximas lições, discutiremos as especificidades não apenas do EC2, mas também da rede na AWS. E você entenderá como tudo que acabamos de mencionar funciona, portanto, fique atento.
# __