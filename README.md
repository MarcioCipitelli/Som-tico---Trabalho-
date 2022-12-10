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


```
from google.colab import drive 
drive.mount('/content/drive')

```
2- Montar um diretório específico para os documentos gerados. Utilizar o ```%%bash``` para indicar ao Colab que este código está em bash e utilizar o ```%cd```para fixar esse diretório como o diretório principal:

```
%%bash
mkdir vepsomatico
%cd somatico

```

3- Confirmar o diretório que será utilizado:
```
%%bash
pwd

```

4- Instalar algumas módulos que serão utilizados mais adiante:

```
import pandas as pd
import csv

```

Ambiente de trabalho está preparado para a utilização do programa VEP.


 <h1 align="center">Utilizando o VEP </h1> 


Criado o ambiente de trabalho, utilizar o comando abaixo para instalar o VEP. Em ordem, cada linha do comando pode ser interpretada da seguinte forma:

1- Instalação dos pacotes necessários para utilizar o VEP;

2- Fazer download do VEP na versão esembl-vep 105.0;

3- Descompactar o documento baixado.

As duas últimas linhas indicam ao colab para entrar no diretório do VEP onde foi descompactado e realizar a instalação:
```
%%bash
sudo apt install unzip curl git libmodule-build-perl libdbi-perl libdbd-mysql-perl build-essential zlib1g-dev
wget -c https://github.com/Ensembl/ensembl-vep/archive/refs/tags/105.0.tar.gz
tar -zxvf 105.0.tar.gz
cd ensembl-vep-105.0
./INSTALL.pl --NO_UPDATE 

```
 Após, utilizar o código abaixo para verificar a instalação:
 ```
 %%bash
cd ensembl-vep-105.0
./vep

```

Com o ambiente de trabalho preparado e o VEP instalado, realizar a anotação das variantes:
```
%%bash
/ensembl-vep-105.0/vep  \
  --fork 4 \
  -i /caminho_documento_vcf/nome_documento_vcf.vcf.gz \
  -o nome_desejado.filtered.vcf.tsv \
  --dir_cache /caminho_dir_cashe/ \
  --fasta /caminho_documento_fasta/nome_documento_fasta.fasta \
  --cache --offline --assembly GRCh37 --refseq  \
	--pick --pick_allele --force_overwrite --tab --symbol --check_existing --variant_class --everything --filter_common \
  --fields "Uploaded_variation,Location,Allele,Existing_variation,HGVSc,HGVSp,SYMBOL,Consequence,IND,ZYG,Amino_acids,CLIN_SIG,PolyPhen,SIFT,VARIANT_CLASS,FREQS" \
  --individual all
  
  ```
  
 Para interpretar os caminhos e nomes necessários para preencher corretamente o comando acima obervar:
 
-Em ```-i```  o ```caminho_documento_vcf``` se refere ao caminho do diretório onde o arquivo vcf a ser analisado está localizado e ```nome_documento_vcf``` se refere ao nome do documento VCF que será analisado.

-Em ```-o``` o ```nome_desejado``` se refere ao nome que deseja utilizar no output do arquivo filtrado gerado pelo VEP.

-Em ```--dir_cache``` o ```'caminho_dir_cashe'``` se refere ao caminho do diretório cashe.

-Em ```--fasta``` o ```caminho_documento_fasta``` é o caminho para o diretório onde está localizado o documento fasta.

-As opções ```--cache```, ```--fields``` e ```--individual```  deve-se preencher de acordo com o que deseja gerar no output e a documentação para fazer a melhor escolha possível para cada caso pode ser encontrada no site:
https://www.ensembl.org/info/docs/tools/vep/script/vep_filter.html

Depois, visualizar o arquivo gerado pelo VEP através de uma tabela gerada pelo pandas:

1- Em ```caminho_para_vcf_tsv``` indica o caminho do diretório para o arquivo ```vcf.tsv```;

2- Em ```nome_arquivo_vcf_tsv``` se refere ao nome do arquivo ```vcf.tsv``` que foi gerado.
```
tabela = pd.read_csv('/caminho_para_vcf_tsv/nome_arquivo_vcf_tsv.filtered.vcf.tsv', sep='\t', skiprows=38)
df = pd.DataFrame(tabela)
df
```

