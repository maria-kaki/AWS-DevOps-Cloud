Sejam bem-vindos ao nosso exercício passo a passo sobre a criação de um bucket S3 e, em seguida, a modificação da instância do EC2 que contém o aplicativo para utilizar esse bucket S3. 
# __
![[Pasted image 20230707154235.png]]
Como os senhores podem ver, já estou no console de gerenciamento do AWS e estou conectado como o usuário administrador que foi criado anteriormente. Portanto, a primeira coisa que preciso fazer é criar o bucket S3 que será utilizado pelo aplicativo. Para fazer isso, vou até a barra de pesquisa aqui e digito S3 e, em seguida, clico no serviço S3 para ser levado ao console S3. 
# __
![[Pasted image 20230707154330.png]]
Agora que estou no console S3, vou clicar em Create Bucket. 
# __
![[Pasted image 20230707154400.png]]
E para o nome do meu bucket, vou usar employee-photo-bucket-sr, como minhas iniciais, e, em seguida, um traço e apenas três dígitos aleatórios. Portanto, vou usar 963. Quero ter certeza de que meu bucket está na mesma região que o restante da minha infraestrutura, portanto, vou mantê-lo como a região de Oregon ou US West 2, e depois vou manter todos os outros padrões como estão. 
# __
![[Pasted image 20230707154448.png]]
A partir daí, vou clicar em Create Bucket. 
# __
![[Pasted image 20230707154517.png]]
E, como os senhores podem ver, meu bucket foi criado com sucesso. 
# __
![[Pasted image 20230707154553.png]]
Agora que o bucket foi criado com sucesso, quero testar o upload de um objeto só para ter certeza de que tudo está funcionando. Então, clicarei no nome do bucket, o que me levará à página de detalhes do bucket.
# __
![[Pasted image 20230707155900.png]]
E para fazer upload de um arquivo, posso clicar no botão de upload que está no centro da página aqui, mas, na maioria das vezes, usarei o que está no canto superior direito. Então, clico no botão de upload e, em seguida, 
![[Pasted image 20230707155937.png]]
clico em Add Files, 
![[Pasted image 20230707160221.png]]
e faço o upload dessa foto do funcionário dois. Depois de adicionar esse arquivo, posso clicar em Upload. 
# __
![[Pasted image 20230707160259.png]]
E, como os senhores podem ver, o upload do arquivo foi bem-sucedido. Então, vou clicar em Close (Fechar).
# __
![[Pasted image 20230707160408.png]]
E, em uma demonstração anterior, os senhores devem ter visto uma maneira de tornar esse objeto acessível ao público, mas, para esse bucket e para os exercícios a seguir, não queremos que esse bucket seja totalmente aberto ao mundo, queremos que esse bucket e esses objetos sejam acessados especificamente pelo aplicativo. Para fazer isso, precisamos ajustar as permissões desse bucket, especificamente a política do bucket. Como já estou na página de detalhes do bucket, vou clicar na guia Permissions (Permissões). 
# __
![[Pasted image 20230707160435.png]]
E quero ajustar a política do bucket para esse bucket. Então, vou rolar para baixo até a política do bucket e clicar no botão editar, o que me levará a um local onde posso criar uma política de bucket. 
# __
![[Pasted image 20230707160510.png]]
Portanto, para criar essa política de bucket, vou pegar a política que está nas instruções do exercício e colá-la aqui. 
```json
{ 
	"Version": "2012-10-17", 
	"Statement": [ 
		{ 
			"Sid": "AllowS3ReadAccess", 
			"Effect": "Allow", 
			"Principal": { 
				"AWS": "arn:aws:iam::<INSERT-ACCOUNT-NUMBER>:role/S3DynamoDBFullAccessRole" 
			}, 
			"Action": "s3:*", 
			"Resource": [ 
				"arn:aws:s3:::<INSERT-BUCKET-NAME>", 
				"arn:aws:s3:::<INSERT-BUCKET-NAME>/*" 
			] 
		} 
	] 
}
```
Mas antes de prosseguir, antes de salvar essa política, preciso editar algumas coisas. A primeira coisa que preciso editar é o número da conta para que eu esteja utilizando a conta correta. E isso será feito aqui onde diz, insert account number, e vou colar o número da minha conta ali. A partir daí, também vou rolar a tela para baixo e mudar essa área onde diz, insert bucket name, e colocarei o nome do meu balde ali. E preciso me certificar de fazer isso nos dois locais e de remover os colchetes ao fazer isso. 
# __
![[Pasted image 20230707161029.png]]
Agora que fiz isso, posso salvar essas alterações e minha política de bucket será criada. 
# __
![[Pasted image 20230707161108.png]]
E agora minha conta com essa função específica terá acesso a esse bucket e aos objetos dentro dele. Portanto, agora que testei o upload de um objeto e criei o bucket, bem como forneci acesso ao bucket por essa função, preciso modificar o aplicativo para utilizar esse bucket. 
# __
![[Pasted image 20230707161142.png]]
Para isso, vou acessar o EC2 
![[Pasted image 20230707161318.png]]
e clicar em Instâncias. 
# __
![[Pasted image 20230707161350.png]]
E, como os senhores podem ver, minha instância parada do exercício anterior está lá, e há um pequeno atalho interessante que pode ser usado para clonar essa instância de modo que eu inicie basicamente a mesma coisa e me certifique de manter essas configurações. 
# __
![[Pasted image 20230707161438.png]]
Então, para fazer isso, o que farei é selecionar essa instância interrompida e, em seguida, ir para Actions (Ações), e para Image and Templates (Imagem e Modelos). E, em seguida, posso clicar em launch more (lançar mais) assim. 
# __
![[Pasted image 20230707161604.png]]
O que isso fará é abrir a página de lançamento da minha instância, mas já ter algumas coisas preenchidas para que minha instância seja um clone da instância interrompida que já lancei. Portanto, o que quero fazer é ter certeza de que sei que essa é a instância atualizada do meu aplicativo. Para isso, vou acrescentar -s3 ao final do nome da instância. Portanto, será employee-directory-app-s3. 
# __
![[Pasted image 20230707161636.png]]
E minha imagem e o tipo de instância permanecerão os mesmos. Portanto, o que posso fazer é ter certeza de que estou usando o mesmo par de chaves que estou usando com minhas outras instâncias. 
# __
![[Pasted image 20230707161707.png]]
Em seguida, quero rolar a tela para baixo e me certificar de que essa instância estará acessível. Portanto, quero alterar a atribuição automática de IP público para habilitada, e isso garantirá que eu tenha um endereço IP público para acessar essa instância. A partir daí, vou continuar a rolar a tela para baixo, pois todas as outras configurações ainda estão corretas, e, em seguida, vou expandir os detalhes avançados. 
# __
![[Pasted image 20230707162047.png]]
Com os detalhes avançados expandidos, posso ver que a função já está associada a essa instância. 
# __
![[Pasted image 20230707162123.png]]
E vou rolar a tela até os dados do usuário,
![[Pasted image 20230707162141.png]]
e o que preciso fazer é colocar o nome do meu bucket aqui para que agora meu aplicativo saiba qual bucket utilizar. 
![[Pasted image 20230707162214.png]]
E assim, com o nome do meu bucket aqui, posso agora iniciar minha instância.
# __
![[Pasted image 20230707162247.png]]
E isso levará um pouco de tempo, portanto, vou até minhas instâncias e esperarei que ela seja iniciada, 
![[Pasted image 20230707162313.png]]
apenas atualizando-a ocasionalmente para garantir que tudo seja iniciado corretamente. E quero esperar até que a verificação de status mostre duas das duas verificações aprovadas. 
# __
![[Pasted image 20230707162347.png]]
Então, agora que já dei um tempo, vou clicar em atualizar novamente. E, como podemos ver, há duas das duas verificações aprovadas. 
# __
![[Pasted image 20230707162428.png]]
Então, só quero ter certeza de que esse aplicativo está em funcionamento. Vou selecionar essa instância e copiar o endereço IP público, e, em seguida, em uma nova guia, vou colar esse endereço IP. 
# __
![[Pasted image 20230707162459.png]]
E, como podemos ver, o aplicativo está em funcionamento. Ainda não podemos interagir com esse aplicativo porque o banco de dados não foi associado. Portanto, isso é apenas para garantir que o aplicativo está em funcionamento e que poderemos interagir com ele daqui a pouco. Agora que isso foi feito, quero apenas realizar algumas tarefas de encerramento para isso. 
# __
![[Pasted image 20230707162606.png]]
E, portanto, certifique-se de que o senhor, se estiver acompanhando ou se já tiver feito isso, que vá em frente e pare essa instância, 
![[Pasted image 20230707162635.png]]
bem como exclua o objeto que foi carregado no bucket S3. 
# __
Isso garantirá que o senhor não acumule acidentalmente nenhuma cobrança fora da execução deste exercício.