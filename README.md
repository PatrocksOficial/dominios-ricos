# dominios-ricos
Um documento onde irei descrever as principais funcionalidades, comparações, ganhos, dificuldade sobre os dominios ricos

Domínios Ricos vs Domínios Anêmicos
Os Domínios Anêmicos só tem propriedades que referem diretamente no seu banco, ou seja, você não consegue testar procedures, functions e afins pois ele já afeta diretamente seu banco de dados.

Alguns exemplos dos malefícios:
- Não consegue testar
- Tem uma limitação pois geralmente não se deixa regras no banco e sim por exemplo no C#, Java e afins, pois nesse caso você tem a Orientação a Objetos, tem ainda regras de negócios em procedures porém atualmente já traz as regras de negócio na própria aplicação.
- Store Procedure você pode utilizar porém não é recomendado condicionais, ou seja, condições como if é uma condição e não um teste, é uma complexidade ciclomática, aumentando a complexidade do código a medida que coloca mais e mais condições.

Já com os Domínios Ricos, você pode testar, a aplicação que irá ter a regra de negócio, podendo ser testada ainda por cima e o banco só irá buscar as informações já condicionadas em sua aplicação,
você obtem uma melhor segurança, para manuseio de suas regras, pois as mesmas você consegue testar antes de mandar de fato esse "update" para o seu banco afetando diretamente e dificultando sua viabilidade e manutenção.


Sub Domínios:
São as segmentações dos domínios, como pode-se citar os micro serviços, que pode ser compreendido por uma comparação simples, diversos commits que são conhecidos como back size, ou seja,
ao invés de commitar todas alterações de uma vez, você vai fragmentando seus commits, tornando assim o versionamento do código, suas demais alterações não causam tantos merges e demoram para serem resolvidos,
então você segmenta seus commits a fim de facilitar o manejamento do código.

Separação em Contextos Delimitados:
Podemos dizer que seria o dimensionamento do patch size, entender qual o grau de dificuldade que será imposto mediante as mudanças, por exemplo, versionamento, dar upgrade em uma determinada versão de sua aplicação, quanto tempo levaria até de fato conseguir executar? Uma aplicação legado sendo atualizada para novas linguagens, qual o tamanho da mudança?
- OBS: Patch Size (Tamanho da mudança).
Quanto menor for a mudança, melhor, por isso os microsserviços vem ganhando visibilidade e uma alta demanda, sendo assim, quebrar em vários contextos a fim de facilitar a manutenção / criação, obtendo ótimos resultados.


Criar as entidades conforme o que foi estruturado e conversado com o cliente, onde o mesmo irá falar o que deseja em sua aplicação e você irá modelar e fazer a criação das entidades conforme pedir, exemplo:
o cliente quer uma plataforma onde os estudantes tenham que pagar assinaturas para poderem assistir aos cursos.

Nesse sentido, a princípio deverá ser criado três classes:
- Student
- Payment
- Subscription
  
O Student deverá ter os seguintes campos:
- Nome, Sobrenome, Documentos, Email, List<Subscription>, string Adress(endereço de entrega).
  
O Subscription deverá ter os seguintes campos:
-DateTime CreateDate, LastUpdateDate, DateTime? ExpireDate, bool Active, List<Payment>.

O Payment deverá ser dividido em 3 classes diferentes, onde um será o paypal, boleto e cartão de crédito, note que é importante separar pois cada forma de pagamento possuem campos necessários que precisam ser passados.

Para o Payment, deverá ser uma classe abstrata pois ela tem que ser ou paypal, boleto ou cartão de crédito, seus campos devem ser:
- string Number (será gerado um hash a fim de identificar o pagamento), DateTime PaidDate, DateTime ExpireDate, Decimal Total, Decimal TotalPaid, string Address (endereço de cobrança).

Para as demais, elas irão fazer a herança de Payment que é nossa classe abstrata, e no BoletoPayment deverá conter os seguintes campos:
- 

