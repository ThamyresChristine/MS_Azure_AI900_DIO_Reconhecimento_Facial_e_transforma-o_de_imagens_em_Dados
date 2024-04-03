# Detecção de textos em imagens através do Azure Machine Learning
_Projeto realizado para a Certificação IA900 oferecida pela Microsoft em parceria com a DIO - Digital Innovation One_

---

## O Azure AI Vision Studio

O _Vision Studio_ é um dos serviços de Inteligência Artificial do Azure, voltado para especialmente para processamento de imagens - seja  como reconhecimento facial, de objetos, reconhecimento de textos em imagens ou análise espacial de vídeos, reconhecendo o que aparece em tela. 
---
## Criando um Recurso
---
Primeiro, acesse sua conta Azure (pelo portal Azure) e clique em _Create a resource_.

![img1]()

No menu lateral esqurdo clique em _AI + Machine Learning_. A busca te retornará todos os serviços dessa seção. Escolha o _Azure AI services_ e clique em _create_.

![img2]()

O Azure solicita que você preencha alguns dados, como o _Resource group_, onde você pode criar um ou selecionar um já existente.

![img3]()

Além disso, você precisa criar um nome e definir o _Pricing tier_. E não esqueça de marcar a _checkbox_, onde você concorda com os termos do Azure AI Services.

![img4]()

***
## Acessando e configurando o AI Vision Studio

Após a configuração do _Resource group_, acesse o Visio Studio (_portal.vision.cognitive.azure.com_). Na página inicial, clique em _View all resources_.  

![img5]()

Selecione o _resource_ criado anteriormente no portal do Azure e clique em _Select as default resource_.

![img6]()

***
## Acessando a ferramenta

Retorne para a página inicial do Vision Studio. Escolha a ferramenta que deseja utilizar - no meu caso, eu quero o _OCR - Optical Character Recognition_, que faz o reconhecimento de textos em imagens.

![img7]()

E seleciono a API _Extract text from images_.

![img8]()

No _Read API_, eu posso enviar um arquivo do computador local e tirar uma foto na hora, mas antes é necessário marcar a _checkbox_ que informa que a demonstração vai utilizar o recurso criado no portal da Azure e pronto! Agora é enviar as imagens e ver como a ferramenta analisa as imagens e reconhece os textos.

![img9]()


---
## Análise e extração dos textos nas imagens enviadas para o _Read_ 
---

- **Imagem 01**: Como primeiro exemplo, adicionei uma imagem sem texto de propósito para ver como resultado _"null"_. Mas para minha surpresa, o _Read_ reconheceu uma linha como valor numérico 211, numa imagem que está de boa qualidade. E no json, a confiança (ou acurácia) até apresenta um valor pouco alto - 63%.

![Output_01]()

- **Imagem 02**: Uma imagem simples, de boa qualidade, onde o texto claramente se destaca, o _Read_ reconheceu perfeitamente as duas palavras presentes. No json, a confiança até apresenta um valor excelente para as duas palavras - 99% e 98%, respectivamente.

![Output_02]()

- **Imagem 03**: Nessa imagem, apesar de o texto não estar em uma superfície plana, como uma folha de papel, ele está nítido e com fundo branco. O _Read_ reconheceu perfeitamente o texto. No json, a confiança até apresenta o valor de 99% para quase todas as palavras, com exceção de _o_(62%) e _Colossenses_(77%), mas mesmo assim, é um valor aceitável.

![Output_03]()

- **Imagem 04**: Como é uma foto de uma tela de computador, a imagem está claramente com a nitidez ruim. Mesmo assim, o _Read_ conseguiu extrair algumas palavras. Detalhe que ele reconheceu o _X_ para fechar a janela como se fosse a letra X. No json, temos a maioria das palavras com confiança de 98% e outras com 33%.

![Output_04]()

- **Imagem 05**: Outra foto de tela, aqui com a nitidez perfeita. Percebe-se que o _Read_ faz a leitura assim como fazemos com uma folha de papel - iniciando no canto superior direito e seguindo para a esquerda, uma linha atrás da outra - mas que isso não se aplica em todos os casos, pois aqui a primeira linha é _jogos_, a seguinte é _fazer_, a terceira contém o título do vídeo e só na quarta linha está _login_. O correto seria _fazer login_ em uma mesma linha, mas o _Read_ não reconheceu assim. No json, temos a maioria das palavras com confiança de 98%, mas algumas com o valor bem baixo (_/01_ com 3%).

![Output_05]()

- **Imagem 06**: Testando para valer o _Read_ com texto à mão. Ele reconheceu bem a maior parte do texto, e até algumas palavras do outro lado da folhar por causa da sombra, mas alguns detalhes, como em _Ctrl + N_, em que a letra N está dentro de um quadrado, ele reconheceu como _\N/_ e não reconheceu as setas. No json, a maioria das palavras tinha confiança com valor alto - destaque para _the_ e _screen_, ambas com valor 1 - e algumas expressões como _Ctrl+B_ tiveram valor quase zero.

![Output_06]()

- **Imagem 07**: Uma foto que não está muito nítida, mas podemos entender e o _Read_ também reconheceu o texto. Aqui fica claro que ele faz a leitura da esquerda para a direita como deve ser, mas que nesse caso isso não se aplica, já é um cronograma de aulas e o ideal seria a leitura no sentido de cima para baixo. No json, o valor da confiança não foi muito alto, ficou entre 60% e 80% e por mais que as palavras se repetissem aqui, elas apresentaram valores de confiança totalmente diferentes.

![Output_07]()

- **Imagem 08**: Aqui, além do reconhecimento de palavras, o _Read_ também reconheceu alguns pontinhos da linha do sumário. No json, as palavras apresentaram valor de confiança bem alto (98%), já os pontinhos ficam com um valor um pouco baixo (60%).

![Output_08]()

- **Imagem 09**: O _Read_ reconhece muito bem os dois textos da página. Mas como citado anteriormente, o _Read_ sempre faz a leitura da esquerda para a direita e os dois textos se misturam no resultado. No json, a grande maioria das palavras ficou com o valor de confiança em 99%.

![Output_09]()

- **Imagem 10**: O _Read_ reconheceu, muito bem o texto e até o o link do vídeo do Youtubem mesmo que estando bem pequeno. O resultado ficou um pouco confuso, já que o _Read_ não reconhece que há textos separados e novamente, faz a leitura da esquerda para a direita. No json, a maioria das palavras tem o valor de confiança em torno de 98%, com exceção de alguns símbolos confusos.

![Output_10]()

- **Imagem 11**: Os elementos textuais estão bem claros e organizados aqui, então o _Read_ fez a transcrição da página perfeitamente. No json, a maioria das palavras tem o valor de confiança em torno de 99%.

![Output_11]()

- **Imagem 12**: O _Read_ reconheceu perfeitamente todos os elementos textuais presentes na imagem, mas o resultado ficou um pouco confuso, já que o _Read_ não reconhece a organização das perguntas e da tabela, sempre fazendo a leitura da esquerda para a direita. No json, a maioria das palavras tem o valor de confiança em torno de 99%.

![Output_12]()

- **Imagem 13**: A imagem não tem muitos elementos textuais e eles estão, de certa forma, esparçardos, mas o _Read_ reconheceu melhor o texto que está organizado na parte inferior e o que está com letras grandes. A confiança variou bastante nessa análise, entre 20% e 90%.

![Output_13]()

- **Imagem 14**: Aqui temos a praticamente a mesma imagem da anterior, com uma pequena diferença. Mas diferente da primeira análise, aqui o _Read_ reconheceu bem o texto na parte inferior. Ainda assim, a confiança variou bastante nessa análise, entre 30% e 90%.

![Output_14]()

- **Imagem 15**: Na última imagem para análise do _Read_, ele reconheceu todo texto na página, até as letras que indicam o dia na parte superior esquerda, reconheceu também até o símbolo de divisão, mas não entendeu que era uma operação porque faz  leitura da esquerda para a direita. No json, a confiança variou bastante nessa análise, entre 20% e 90%.

![Output_15]()

---
## Conclusões
---
O _Read_ identifica de forma bem precisa os elementos textuais presentes. Percebe-se que ele foi projetado para realizar a leitura da forma que ela é - da esquerda para a direita, iniciando na parte superior - e em alguns casos, onde o texto não se encaixa nesse padrão - uma tabela, por exemplo, o _Read_ entrega o texto, mas de forma desorganizada. Independente disso, ele continua sendo uma excelente ferramenta para reconhecimento de texto em imagens.

---
## Fontes/Links Úteis
---
- **Portal do Azure.** Disponível em: https://azure.microsoft.com/pt-br/ Acesso em: 30 de Março de 2024.
- **Read text in Vision Studio.** Disponível em: https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/05-ocr.html Acesso em: 30 de Março de 2024.
- **OCR - Optical Character Recognition.** Disponível em: https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/overview-ocr Acesso em: 30 de Março de 2024.
- **What is Azure AI Vision?** Disponível em: https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/overview Acesso em: 30 de Março de 2024.
- **Demonstração do OCR.** Disponível em: https://portal.vision.cognitive.azure.com/demo/extract-text-from-images Acesso em: 30 de Março de 2024.
