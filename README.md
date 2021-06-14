# Facial-Recognition
Projeto de Robótica com opencv
## Iniciando o programa
* Para que o notebook funcione corretamente, é necessário configurar a aceleração de hardware para GPU. Para isso, clique na aba "Ambiente de Execução" e na opção "Alterar o tipo de ambiente de execução" e então escolhe "GPU".
* Em seguida é necessário executar as três primeiras clásulas do notebook e criar oito pastas dentro de "known_faces" com os nomes das celebridades. Então, baixar as imagens da pasta "Imagens" e adicionar os arquivos das pastas "known_faces" e "unknown_faces" nos lugares correspondentes na aba "Arquivos" no notebook.
## O programa
### Importações e constantes
* Utilizamos o “os” para trabalhar com diretórios e “cv2” para rotular/desenhar em nossas imagens. As primeiras duas constantes são apenas os nomes de nossos diretórios conhecidos e desconhecidos.
* Em seguida, temos TOLERANCE. Este é um valor de 0 a 1 que permitirá que você ajuste a sensibilidade da comparação. O valor usado é 0.5. O valor *zero* indica a tolerância mais rígida e o valor *um* indica a tolerância mais suave. Por meio dos testes, o valor 0.5 ou 0.6 foram os que deram os melhores resultados.
* O FRAME_THICKNESS representa quantos pixels de largura deseja-se que os retângulos que envolvem uma face tenham
* FONT_THICKNESS é a espessura desejada que a fonte com o rótulo tenha.
* Usamos cnn (rede neural convolucional) como modelo de reconhecimento de objetos.
### Definindo marcação
* "def name_to_color(name):"
* Para desenhar um retângulo ao redor das faces reconhecidas, precisamos das coordenadas superior esquerda ("top_left") e inferior direita ("bottom_right"), e usamos "cv2.rectangle" para desenhá-lo.
* Queremos uma cor exclusiva para estas caixas para representar identidades diferentes ("color").
### Faces e Marcações
* Ao iterar (processo conhecido pela repetição de uma ou mais ações) nosso diretório de faces conhecidas, carregamos essa imagem como *face_recognition*. Nesse mesmo loop, codificaremos cada uma dessas faces e armazenaremos as codificações e a identidade associada em nossas listas. E então, o programa estará pronto para verificar se há rostos em imagens desconhecidas e tentar identificar esses rostos em: **encoding = face_recognition.face_encodings (image)**
* Em *known_images* assumimos e precisamos de apenas um rosto por foto, mas em *unknown_faces* presumimos que imagens desconhecidas podem conter várias pessoas e outros objetos. Portanto, queremos primeiro localizar esses rostos. Fazemos isso com: **locations = face_recognition.face_locations(image, model=MODEL)** e codificarmos estas imagens: **encodings = face_recognition.face_encodings(image, locations)**
* Agora iteramos os rostos encontrados nas imagens desconhecidas, para encontrar uma correspondência com algum de nossos rostos conhecidos. Ao encontrar, queremos desenhar um retângulo ao redor deles. Por esse motivo, usamos o OpenCV e foi necessário primeiro converteremos a imagem RGB para BGR, já que o OpenCV usa BGR. Assim: **image = cv2.cvtColor(image, cv2.COLOR_RGB2BGR)**
* A variável “results” contém uma lista de booleanos, considerando se alguma correspondência foi encontrada. **results = face_recognition.compare_faces(known_faces, face_encoding, TOLERANCE)**
* Pegamos o valor do índice para qualquer um dos “True” e procuramos o nome de nossa variável known_names.
 **if True in results: 
        match = known_names[results.index(True)]
        print(f' - {match} from {results}')**

## Reconhecimentos
* O código foi baseado no tutorial de [sentdex](https://pythonprogramming.net/facial-recognition-python/)
