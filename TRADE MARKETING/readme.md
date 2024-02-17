📊ANALISIS DE TRADE MARKETING AL DATASET

https://www.kaggle.com/datasets/rodsaldanha/arketing-campaign 

🚀Rendimiento Financiero y Demográfico (Página 1): 
Los ingresos totales y la cantidad de clientes sugieren una base de clientes sustancial y diversa, con la recencia promedio indicando un compromiso razonablemente reciente. La distribución del gasto en productos revela preferencias de consumo clave que podrían influir en futuras estrategias de inventario.

🚀Estructura Familiar y Segmentación (Página 2): 
La presencia de niños y adolescentes en el hogar junto con los datos educativos y maritales aportan una comprensión detallada de la base de clientes, permitiendo una segmentación más precisa y personalizada en campañas de marketing.

🚀Análisis por País (Página 3): 
La variabilidad en el gasto y los ingresos por país, combinada con la respuesta a campañas y las quejas, subraya la importancia de adaptar las campañas a especificidades regionales y culturales.

🚀Detalles de Campaña (Página 4): 
La tasa de respuesta general y el comportamiento de los clientes multirespuesta reflejan la eficacia de las campañas. La participación varía significativamente con factores demográficos, como la edad y el estado civil, lo que sugiere oportunidades para una orientación más granular.

📊 Recomendación para Mejoras en Campañas Futuras:

A partir de los insights obtenidos, recomiendo una estrategia de campaña multifacética que:

🎯Personalice las Ofertas: Utilice la información demográfica para personalizar las ofertas a segmentos específicos, mejorando la relevancia y potencialmente la tasa de respuesta.

🎯Optimice la Segmentación Geográfica: Ajuste las estrategias de marketing a las peculiaridades culturales y económicas de cada región, basándose en el rendimiento y las respuestas pasadas por país.

🎯Aumente la Fidelización: Desarrolle programas de fidelización dirigidos a clientes que han respondido a múltiples campañas, maximizando su valor a largo plazo.

🎯Aproveche los Datos de Quejas: Analice las quejas para identificar y abordar problemas recurrentes, mejorando así la satisfacción del cliente y reduciendo las tasas de quejas futuras.

🎯Refine el Targeting Generacional: Adapte los mensajes y canales de las campañas para resonar mejor con las preferencias de comunicación de diferentes generaciones.

🎯Fortalezca la Presencia Web: Con base en la correlación entre las visitas web y la participación en campañas, mejore la experiencia en línea para aumentar la eficacia de las campañas digitales.

🎯Enfoque Basado en Datos: Continúe aplicando técnicas de análisis de datos avanzadas para refinar continuamente la comprensión del comportamiento del cliente y optimizar las campañas de marketing.

🎯El uso efectivo de Business Intelligence y análisis de datos no solo mejorará el rendimiento de las campañas individuales, sino que también contribuirá a una estrategia de marketing integral más robusta y basada en datos.

## MODELO DE DATOS
<p align="center">
  <img src="https://github.com/Pear-itaPE/PORTFOLIO-POWER-BI/blob/main/TRADE%20MARKETING/RECURSOS/MODELO%20DE%20DATOS.png" alt="MODELO DE DATOS">
</p>

## FORMULAS DAX

Nombre	Expresión DAX
	
# COUNTRYS	DISTINCTCOUNT(marketing_data[Country])
 	 
% COMPLAINTS	CALCULATE(
	    SUMX(marketing_data, marketing_data[Complain]),
	    marketing_data[Complain] = 1
	) / COUNTROWS(marketing_data) * 1
	
AVG (AGE/INCOMES/RECENCY)	AVERAGE(marketing_data[Name])
	
purchasing channel 	SUM(marketing_data[NumDealsPurchases]) +
	SUM(marketing_data[NumWebPurchases]) +
	SUM(marketing_data[NumCatalogPurchases]) +
	SUM(marketing_data[NumStorePurchases]) 
	
MultipleClientsCampaigns	CALCULATE(
	    COUNTROWS(marketing_data), 
	    marketing_data[AcceptedCmp1] + marketing_data[AcceptedCmp2] + marketing_data[AcceptedCmp3] + marketing_data[AcceptedCmp4] + marketing_data[AcceptedCmp5] > 1
	)
	
CMP RESPONSE	DIVIDE(
	    SUM(marketing_data[Response]), 
	    COUNTROWS(marketing_data), 
	    0
	) * 1
	
CMP[1,2,3,4,5]	DIVIDE(
	    SUM(marketing_data[Name]), 
	    COUNTROWS(marketing_data), 
	    0
	) * 1
	
WithResponseCampaigns	COUNTROWS(
	    FILTER(
	        marketing_data, 
	        (marketing_data[AcceptedCmp1] + marketing_data[AcceptedCmp2] + 
	         marketing_data[AcceptedCmp3] + marketing_data[AcceptedCmp4] + 
	         marketing_data[AcceptedCmp5] + marketing_data[Response]) = 1
	    )
	)
	
DEALS PURCHASES	SUM(marketing_data[NumDealsPurchases])
	
TOTAL (FISH/FRUITS/GOLD/WINES	SUM(marketing_data[Name])
/MEAT/SWEET)
	
INCOMES	SUM(marketing_data[MntWines]) + SUM(marketing_data[MntFruits]) + SUM(marketing_data[MntMeatProducts]) + SUM(marketing_data[MntFishProducts]) + SUM(marketing_data[MntSweetProducts]) + SUM(marketing_data[MntGoldProds])
	
LTV 	DIVIDE(
	    [INCOMES], 
	    COUNTROWS(marketing_data),
	    0
	)
	
MEDIAN INCOMES	MEDIAN(marketing_data[ Income ])
	
No Teenagers / No Children	 CALCULATE
	 (
	    COUNTROWS(marketing_data),
	    marketing_data[Name]=0
	 )
	
One Child / One Teenagers	CALCULATE
	(
	        COUNTROWS(marketing_data), 
	        marketing_data[Name] = 1
	)
 	
AverageExpenseTotal	
	VAR TotalWines = SUM(marketing_data[MntWines])
	VAR TotalFruits = SUM(marketing_data[MntFruits])
	VAR TotalMeat = SUM(marketing_data[MntMeatProducts])
	VAR TotalFish = SUM(marketing_data[MntFishProducts])
	VAR TotalSweets = SUM(marketing_data[MntSweetProducts])
	VAR TotalGold = SUM(marketing_data[MntGoldProds])
	VAR TotalGastos = TotalWines + TotalFruits + TotalMeat + TotalFish + TotalSweets + TotalGold
	VAR NumeroClientes = COUNTROWS(marketing_data)
	RETURN
	TotalGastos / NumeroClientes
	
 	
Total customer	COUNTROWS(marketing_data)
	
Z CHILD = 	SUMX(marketing_data,marketing_data[Kidhome])
 	
Two Children/Two Teenagers	 CALCULATE
	 (
	    COUNTROWS(marketing_data),
	    marketing_data[Name]=2
	 )

![image](https://github.com/Pear-itaPE/PORTFOLIO-POWER-BI/assets/143855758/ebf7f37d-d63f-444e-8eca-c234e0c41262)

