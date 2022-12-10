 <h1 align="center"> :man: Somatico--Trabalho Bioinformatica- :computer: </h1> 



Introdução para utilização do VEP Somático:
Ensembl Variant Effect Predictor (VEP) auxilia na determinação dos efeitos das variantes encontradas nos dados analisados. que podem ser genes, transcritos ou sequências proteicas. Para a análise utilizando o VEP é necessário apenas as coordenadas das variantes e a mudança nucleica observada.

O processo inicial para utilização do VEP :

1- Montar o drive no Colab;

2- Instalar o VEP;

3- Fazer a anotação das variantes.


 <h1 align="center">Preparação do ambiente de trabalho </h1> 


Começar criando um novo notebook no seu Google Colab, uma vez no colab:

1- Montar o drive no ambiente de trabalho, que permite criar e gerenciar os dados

"from google.colab import drive 
drive.mount('/content/drive')"
