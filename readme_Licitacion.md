# Explicación de Etapas y códigos de la Evaluación de los resultados de la licitación del nuevo CM alimentos.

El proceso se divide en 4 etapas (cada una en un folder) y dos versiones. Además los datos generales están en el folder "Data".

# Versión 1

## Etapa 1: Catalogación CM Alimentos. Consiste en la identificación de atributos en los catálogos de productos del CM2014 y CM2017.

Esta identificación de atributos permite hacer match entre los productos de ambos CMs.

 - El código esta explicado paso a paso en "/Etapa1/Version0/catalogar_alimentos2018/codes/CatalogacionCmAlimentos.ipynb"
 - el folder "CmAlimentos/Etapa1/Version0/catalogar_alimentos2018" contiene todo lo necesario (códigos y datos) para hacer la identificación de atributos de los catálogos de productos del CM alimentos 2014 y 2017.
 - El proceso de identificar los atributos se divide en dos tipos de atributos: (1) atributos nominales (2) atributos ratio. 
 - Este procedimiento de identificación de atributos es un proceso supervisado que necesita de conocimiento sobre los productos a catalogar que permita revisar los resultados y enriquecer los diccionarios usados en la identificación.
 - El código usa como input el listado de productos de cada CM a catalogar y los diccionarios necesarios para hacer la identificación.
 - El código genera como output un csv con la identificación de atributos para cada producto.

## Etapa 2 Versión 0: Selección de Productos y construcción de DataFrame para análisis de precios
 - El código esta en "/Etapa2/version0/Etapa2_SeleccionProductosCreacionDataFrame_v0.Rmd" 
 - Este código usa como input la identificación de atributos sobre los productos de ambos CMs.
 - Este código hace match entre las identificación de atributos de ambos CMs y además se hace merge con las ofertas del CM2014 y 2017 y por último 
   se corrigen los precios de CM2014 agregando la IPC (inflación) e IVA (impuesto) para hacer comparables los precios ofertados entre ambos CMs.
 - Para hacer el match se usan los atributos: TipoProducto, Marca y Formato (gr o ml). A la concatenación de estos atributos se les llama idHomo y 
   es un identificador del match.
 - El output de este código es un data.frame en (format long) de los precios ofertados por lo productos que se logro hacer match entre los CMs. 
   Este output permite hacer una comparación entre las ofertas del CM2014 y CM2017.

## Etapa 3 Versión 0: Identificación y Eliminación de Outliers.
 - El código esta en "/Etapa3/version0/Etapa3_EliminacionOutliers_v0.Rmd" 
 - Sobre el DataFrame que genera la etapa 2 se buscan ofertas por un valor muy distinto a la mayoría de las ofertas. La metodología consiste en 
   hallar grandes saltos de precios entre las ofertas que llegan por un producto y ver si estas ofertas atípicas son un % pequeño de todas las ofertas, 
   en caso de ser un % pequeño se eliminan estas ofertas atípicas limpiando así de outliers el producto.

## Etapa 4 Versión 0: Regresión precios de licitación.
 - El código esta en "/Etapa4/version0/Etapa4_Regresion_Licitacion_v0.Rmd"
 - Usando el DataFrame con outliers ya identificados se estiman las regresiones que permiten hacer la comparación de los precios ofertados entre 
   ambas licitaciones.

# Versión 1

Además existen las Versiones 1 de las Etapas 2, 3 y 4. Esta versión 1 permite aumentar la cantidad de productos que participan en el match entre productos
de CM 2014 y CM 2017. Es decir, en la práctica, la única modificación en las Etapas ocurre en la Etapa 2, las etapas 3 y 4 funcionan igual que en las versiones 0. 
Dentro de las principales modificaciones desde Etapa 2 versión 0 a Etapa 2 versión 1 podemos destacar:

 - Simplificación de la metodología para hacer el match.
 - Para hacer el match se usan los atributos: TipoProducto, Marca, Formato (gr, ml o formato.especial). Donde se agrega como identificador de formato lo que he 
   llamado formato.especial, este aplica para dos categorías (TipoProducto) especificas: (1) "té" donde formato especial corresponde al numero de 'bolsitas' de una 
   caja de te, (2) "endulzante comprimido" donde el formato especial corresponde a el numero de "tabletas" por caja de endulzante.
 - Se corrigieron algunos atributos faltantes en algunos pocos productos
 - para hacer el match se aplican funciones que eliminan cualquier discrepancia entre la valores de los atributos


Notas (Date:   Thu Mar 24 16:28:51 2022): Se creo Crea_DF_Oferta2014.Rmd que intenta replicar el data set que usamos como insumo de la rregresion de precios ofertados en licitacion. Sin embargo no resulta el mismo data set. Hay elemntos que no estan en uno u otro data set (generado ahora y el usado en la regresiones). Al paracer no se esta usando el data set crudo de adujudocacion correcto (/Users/edu/Downloads/EV.\ ALIMENTOS\ PERECIBLES\ Y\ NO\ PERECIBLES\ FINAL..xlsx ). Probaremos con uno recien descargado. Reescribiremos Crea_DF_Oferta2014.Rmd. El resto de codigos no han sido modificados.




