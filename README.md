# CLP
Proposta de **C**ódigo **L**ocalizador de **P**ortão para o meio rural

Com apoio das Secretarias do Estado (da Agricultura e do Meio Ambiente) do Estado de São Paulo, e você, cidadão,
estamos construimdo um novo protocolo de localização geográfica e de endereçamento, a ser utilizado inicialmente por viaturas oficiais da prefeitura, do Estado, para ocorrências policiais, ambulâncias e bombeiros. Consiste em usar métodos simples e já bem conhecidos, tudo é uma questão de se adotar o padrão:

* Usar métodos conhecidos de localização;
* Conhecer a malha viária (com o Openstreetmap) e identificá-la (com IDs eternos a Wikidata);
* Comunicar os maiores interessados &mdash; os produtores rurais;
* Divulgar e revisar os mapas básicos;
* Fazer ajustes finos nas informações oficiais e bancos de dados públicos.

![](assets/CLP-resumo1b.png)<br/>Ver detalhes em [neste PDF](assets/CLP-gov2018-05-02.pdf).

## Motivações
Mesmo no rico Estado de São Paulo, em pleno 2018, chegar até uma propriedade rural nunca foi simples: as vias não tem nome ou não se sabe, sinalização inexiste; distâncias são imprecisas, referências são perdidas, temporárias. Mesmo com celular, o sinal nem sempre pega.

Esse abandono, essa dor é forte para o poder público e pior para o cidadão.  

É preciso "dar nome aos bois", identificar com precisão digital, e encontrar a agulha no palheiro.

## Implementação

Implementar um "conversor de CLP em ponto no mapa" é relativamente simples com as tecnologias disponiveis em domínio público. Um sistema completo,  todavia, que garanta a utilização em todas as cidades, por longo prazo, e operando com todos os tipos de localidade rural, requer diversos cuidados. Preservação digital, abertura de dados, consistência das normas, consistência e viabilidade de tradução das normas para algoritmos (software) eficientes, e outros. 

### Elementos metodológicos e jurídicos

O nome ou número oficial identificador do município, normatizados pelo IBGE, se apresentam como padrão oficial estável e amplamente utilizado.  Já a  codificação de abreviaçao de nome de cidade por código de 3 letras, ainda pouco conhecida mesmo entre as autoridades governamentais, será tão estável quanto o grau de obrigatoriedade do seu uso: uma vez publicada como tabela de-para oficial em lei ou decreto estadual &mdash; tabela anexa "de abreviação para identificador IBGE" &mdash;, não correrá mais risco de instabilidade.

Analogamente o  número oficial identificador da via, o seu marco zero e a referência oficial de mapeamento e metragem da via: sem estabilidade nestas referências oficiais não haverá incentivo ou motivação racional para o uso do CLP. Por exemplo o proprietário não vai investir em uma placa na sua porteira, a prefeitura não vai investir na divulgação de endereços, o corpo de bombeiros e hospitais não vão investir nos aplicativos de georeferenciamento dos endereços, etc.

Mas não é tão simples quanto a tabela de abreviações:

* O processo de "batismo oficial" das vias com respectivos identificadores precisa ser norteado por regras, ser transparente e descentralizado. Hoje apenas autoridades federais e estaduais possuem essa clarareza de regras e acesso a meios técnicos. A descentralização inclui liberdade de usar ferramentas como o OpenStreetMap para que os municípios tenham autonomia. O mesmo vale para  

* Vias dentro de grandes propriedades (e no meio rural isso pode incluir condomínios e loteamentos) possuem como "autoridade de batismo" o proprietário ou associações de proprietários. Esse tipo de identificador deve também ser contemplado pelo processo de normatização, para garantir ampla aderência à malha viária real, na onde nasce a demanda por endereçamento. Mesmo  sendo normatizados num momento posterior, as normas de rotulação devem prever desde o inicio a existência dessas vias, garantindo "reserva de numeração" para elas.

* O processo de "mapeamento digital oficial" precisa prever a existência de [metodologias](https://wiki.openstreetmap.org/wiki/WikiProject_Brazil/Modelos_de_Contrato) baseadas no uso de ferramentas abertas ([licenças OpenDefinitoin](https://opendefinition.org/od/2.0/pt-br/)), tais como as ferramentas de mapeamento digital do OpenStreetMap e cadastramento de dados estruturados na Wikidata.

* As licenças de dados, tanto dados cadastrais como mapas digitais, precisa ser idealmente [CC0](http://creativecommons.org/publicdomain/zero/1.0/legalcode), ou seja, o dado precisa estar dedicado ao domínio público, sem qualquer tipo de retrição &mdash; tal como um mapa anexado à Lei Orgânica do  município. Quando isso não for possível o máximo de restrição que se pode admitir é a Licença de Banco de Dados Aberto Open Data Commons, [ODbL](http://opendatacommons.org/licenses/odbl/1.0). <br/>Eventualmente estratégias de [liceamento dual](https://en.wikipedia.org/wiki/Multi-licensing) para dados esopecíficos podem também ajudar o município a contornar problemas jurídicos.

* Batismo informal compativel com o batismo oficial: quando da indisponibilidade de código oficial de uma via, as "regras de batismo" devem ser suficientemente claras e independentes da autoridade central para que possa ser fixada pela prefeitura ou comunidade de interesse no Openstreetmap sem maiores riscos de mudança no momento futuro da oficialização. As "normas de batismo de via" devem prever esse tipo de situação.  

* Referência em mapas oficiais quando possível (por exemplo mapas de municípios fornecidos pelo IBGE), convencinando como segunda opção, quando da indisponibilidade de mapas oficiais adequados, uma versão estável homologada do Openstreetmap. Regras objetivas e transparentes permitiram que a referência métrica não seja colocada em risco quando da ausência de um  mapa oficial.

 	 	
### Subsídios técnicos

Dados abertos, estáveis e confiáveis são o lastro do CLP. Esses dados são obtidos de projetos mais especializados:

* [Identificadores persistentes](https://wiki.openstreetmap.org/wiki/Permanent_ID) no Openstreetmap, baseados na [tag Wikidata](https://wiki.openstreetmap.org/wiki/Key:wikidata), atribuida a estados, cidades e vias. <br/> O projeto de preservação digital,  [semantic-bridge](https://github.com/OSMBrasil/semantic-bridge) ajuda a garantir a "eternidade" dos identificadores e da sua resolução no Openstreetmap. Nada será perdido, e poderemos dar garantia de décadas!

* Abreviações de nome de estado (2 letras) e **nome de cidade (3 letras)**, com respectivos **mapas digitais estáveis**, também garantidos por projetos de preservação:  [semantic-bridge](https://github.com/OSMBrasil/semantic-bridge), [datasets-br/state-codes](https://Datasets.OK.org.BR/state-codes) e [datasets-br/city-codes](https://Datasets.OK.org.BR/city-codes).

Em seguida a implementação deve contar com dois recursos fundamentais de referência de dados e padronização nos protocolos e algoritmos:

1. Preservação digital unificada de identificadores e metadados de apoio à identificação: **Wikidata**. Todas as entidades geográficas envolvidas na representação CLP são passíveis de identificação persistente e georeferenciamento a partir da [`key:wikidata`](https://wiki.openstreetmap.org/wiki/Key:wikidata) no Openstreetmap e sua identificação recíproca através da [propriedade `P402`](https://www.wikidata.org/wiki/Property:P402) Wikidata.

2. Algoritmos [PostGIS](https://postgis.net/docs/manual-2.0/) para a inferência métrica.



