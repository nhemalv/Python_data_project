# Analisis

## Buscando cuales son las habilidades con más demanda para los 3 roles más populares de datos
Filtre las 3 posiciones con más puestos publicados y consegui las 5 habilidades más populares para cada uno. Esto demuestra en que habilidades se debería enfocar uno para conseguir su puesto preferido. 

Notebook: [2_Skill_Demand.ipynb](3_Project\2_Skills_Count.ipynb)

## Visualizando los datos:

fig, ax= plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles):
    df_plot=df_skills_count[df_skills_count['job_title_short']==job_title].head(5)
    df_plot.plot(kind='barh', x = 'job_skills', y = 'skill_count', ax = ax[i], title=job_title)
    plt.tight_layout()
    ax[i].invert_yaxis()
    ax[i].set_ylabel('')
    ax[i].legend().set_visible(False)

fig.suptitle('Counts of Top Skills in Job Postings', fontsize=15)
plt.tight_layout()
plt.show()

## Resultado
![Mejores Habilidades para los que Trabajan con Datos](3_Project\images\skill_demand_all_data_roles.png)

## Qué nos dice la visualización?
1. Habilidades compartidas entre roles

SQL y Python son muy demandadas en los tres perfiles (Analista, Ingeniero y Científico de Datos).

SAS y Tableau aparecen tanto en Data Analyst como en Data Scientist, pero no en Data Engineer.

2. Data Analyst

SQL es la habilidad más solicitada, con casi 35,000 menciones.

Excel también tiene gran relevancia (~27,000), lo que refleja la importancia del análisis en hojas de cálculo.

Tableau y Python tienen demanda intermedia, útiles para visualización y análisis más avanzado.

SAS aparece con menor frecuencia.

🔎 Insight: El rol de Analista de Datos se centra en SQL + Excel, apoyándose en herramientas de visualización y algo de programación.

3. Data Engineer

SQL y Python dominan nuevamente.

AWS y Azure resaltan la importancia de las habilidades en la nube.

Spark muestra que se requiere experiencia en procesamiento de grandes volúmenes de datos.

🔎 Insight: Los Ingenieros de Datos necesitan experiencia en infraestructura, cloud y big data, además de programación.

4. Data Scientist

Python es la habilidad más demandada de todo el gráfico, con más de 40,000 menciones.

SQL sigue siendo muy relevante para la manipulación de bases de datos.

R mantiene importancia en estadística, aunque está por debajo de Python.

SAS y Tableau aparecen, pero con menor peso.

🔎 Insight: Los Científicos de Datos deben dominar Python y SQL, mientras que R, SAS y Tableau son complementarios.

5. Tendencia general

Analistas de Datos → más orientados a reportes, visualización y consultas estructuradas.

Ingenieros de Datos → centrados en infraestructura escalable, nube y procesamiento masivo.

Científicos de Datos → enfocados en machine learning, programación avanzada y modelos estadísticos.

El gráfico muestra una base común (SQL y Python), pero cada rol se especializa según su propósito: Analista → Ingeniero → Científico.

## 2. Cómo esta la demanda de ciertas habilidades para Analistas de Datos?

### Visualización

df_plot = df_DA_US_perc.iloc[:, :5]

sns.lineplot(data=df_plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()

plt.title('Mejores Habilidades para un Analista de Datos')
plt.ylabel('Probabilidad de que lo pida un puesto')
plt.xlabel('2023')
plt.legend().remove()

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

from adjustText import adjust_text

texts = []
for i, col in enumerate(df_plot.columns):
    texts.append(plt.text(11.2, df_plot.iloc[-1, i], col))
adjust_text(texts, arrowprops=dict(arrowstyle="-", color='gray'))

plt.show()

## Resultados

![Demanda de Habilidades para Analistas de Datos](3_Project\images\demanda_habilidades_DA.png)

## Insights
SQL domina con claridad

A lo largo del 2023, SQL se mantiene como la habilidad más solicitada, con una probabilidad siempre superior al 45%.

Aunque muestra una leve tendencia a la baja en el segundo semestre, sigue siendo la más demandada.

Excel sigue fuerte, pero en descenso

Excel arranca en segundo lugar alrededor de 42%, pero va cayendo de manera más marcada hacia final de año (~35%).

Esto puede indicar que las empresas lo siguen valorando, pero cada vez priorizan más herramientas modernas.

Competencia entre Tableau y Python

Ambas habilidades tienen una demanda bastante similar (~27–30%), con ligeras fluctuaciones.

No hay una clara superioridad de una sobre la otra, lo que sugiere que en analistas de datos visualización y programación son casi igual de relevantes.

SAS en declive

SAS se mantiene como la habilidad menos pedida (~18–21%), con una tendencia ligeramente descendente.

Esto refleja la transición del mercado hacia herramientas más modernas y de código abierto.

Tendencia general

El gráfico muestra que las empresas siguen valorando las herramientas clásicas (SQL y Excel), pero la brecha con herramientas modernas (Python, Tableau) se está cerrando.

A futuro, es posible que la relevancia de Python y Tableau siga creciendo, mientras que Excel y SAS podrían seguir perdiendo peso.


## 3. Que tan bien pagan ciertos puestos?
### Visualizando

sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)

plt.title('Salary Distribution in the United States')
plt.xlabel('Yearly Salary in USD')
plt.ylabel('')
ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K'))
plt.xlim(0, 600000)
plt.show()

### Resultados

![Distribución de Salarios por puesto de Data](3_Project/images/distribucion%20de%20salario.png)

## Insights
Los salarios crecen con la seniority

Los puestos Senior (Data Scientist, Data Engineer, Data Analyst) tienen medianas de salario claramente más altas que sus contrapartes junior.

Por ejemplo, Senior Data Scientist y Senior Data Engineer tienen medianas por encima de los $150K, mientras que Data Analyst ronda más cerca de los $80K–$90K.

Los Data Scientists tienen un rango amplio

Tanto los Data Scientist como los Senior Data Scientist muestran una distribución bastante extendida, con presencia de outliers que llegan hasta cerca de $600K.

Esto indica que el mercado para estos roles es más variable y posiblemente más influenciado por industria, empresa o ubicación.

Data Analysts son los menos remunerados

El rol de Data Analyst (y también el Senior Data Analyst) tiene las medianas más bajas, con menor dispersión que los demás.

Esto refleja que es una posición de entrada al mercado de datos y menos valorada en términos de salario.

Los Data Engineers también son altamente valorados

Data Engineers y Senior Data Engineers muestran salarios competitivos, incluso a la par o ligeramente superiores a los de Data Scientist.

Esto resalta la importancia de la infraestructura y el manejo de datos en grandes organizaciones.

Outliers significativos

En todos los roles hay individuos que ganan mucho más que la media (outliers extremos de $400K–$600K), lo que podría corresponder a posiciones en grandes tecnológicas, roles especializados o compensaciones que incluyen bonos/stock options.

## 3. Cuanto pagan ciertas habilidades?

### Visualizado
fig, ax = plt.subplots(2, 1)

sns.set_theme(style='ticks')

#df_DA_toppay.plot(kind='barh', y = 'median', ax=ax[0], legend=False)

sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, ax=ax[0], hue='median', palette='dark:b_r')

ax[0].set_ylabel('')
ax[0].set_title('10 Highest Paid Skills for Data Analysts')
ax[0].legend().remove()

#df_DA_skills.plot(kind='barh', y = 'median', ax=ax[1], legend=False)

sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, ax=ax[1], hue='median', palette='light:b')

ax[1].set_xlim(ax[0].get_xlim())
ax[1].set_ylabel('')
ax[1].set_title('10 Most In-Demand Skills for Data Analysts')
ax[1].legend().remove()

plt.tight_layout()
plt.show()

### Resultado
![Habilidades con salario mas alto](3_Project\images\salarioxhabilidad.png)

### Insights
Las herramientas más técnicas y de nicho son las mejor pagadas

dplyr, bitbucket, gitlab, solidity, hugging face superan los $175K de salario mediano.

Esto indica que manejar librerías/frameworks específicos, sobre todo relacionados con programación y machine learning, está muy bien valorado.

Conocimientos en tecnologías emergentes marcan la diferencia

Solidity (blockchain) y Hugging Face (NLP/IA) se encuentran en el top de skills mejor remuneradas.

Esto muestra que especializarse en nuevas áreas puede abrir oportunidades salariales muy altas.

Skills menos comunes también pagan más

Herramientas como couchbase, ansible, mxnet, cassandra, vmware no son tan masivas como SQL o Excel, pero quienes las dominan pueden acceder a salarios muy superiores al promedio.

El core sigue siendo Python, SQL y R

Python lidera como el skill más demandado, seguido por Tableau, SQL Server, SQL y R.

Esto confirma que la base de análisis sigue girando alrededor de lenguajes de programación estadística y bases de datos.

Herramientas de visualización y ofimática tienen alta demanda

Tableau, Power BI, Excel, PowerPoint siguen siendo fundamentales porque muchas empresas valoran la capacidad de comunicar resultados además de hacer análisis.

No siempre lo más demandado es lo mejor pagado

Skills como Excel y Word aparecen en la lista de demanda, pero no en la de salarios altos.

Esto refleja que aunque muchas empresas las piden, no diferencian mucho el salario porque son consideradas habilidades básicas.

## 4. Mejores habilidades para aprender
### Visualizado
from adjustText import adjust_text

df_DA_skills_high_demand.plot(kind='scatter', x='skill_percent', y='median_salary')

texts= []
for i, txt in enumerate(df_DA_skills_high_demand.index):
    texts.append(plt.text(df_DA_skills_high_demand['skill_percent'].iloc[i], df_DA_skills_high_demand['median_salary'].iloc[i], txt))

adjust_text(texts, arrowprops=dict(arrowstyle='->', color='gray'))

plt.xlabel('% of Data Analyst jobs')
plt.ylabel('Median Yearly Salary')
plt.title('Most Optimal Skills for Data Analysts in the US')
plt.tight_layout()

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K'))
ax.xaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.tight_layout()
plt.show()

### Resultado
![Mejores Habilidades para un Analista de Datos basado en Salario y Demanda](3_Project\images\best_skills_for_DA.png)

## Insights
Skills con mayor demanda (más usadas en trabajos de Data Analyst)

SQL aparece en casi 60% de los trabajos, siendo la habilidad más demandada del mercado, con un salario mediano de ~$91K.

Excel también tiene gran presencia (40% de los trabajos), aunque su salario mediano es menor ($84K).

Son habilidades “básicas pero indispensables” para conseguir un trabajo en análisis de datos.

Skills con mejores salarios (arriba en el eje Y)

Python lidera con un salario mediano cercano a $98K, además de estar en ~30% de los trabajos → combina buena demanda y excelente paga.

Oracle también destaca en salario (~$97K), aunque con baja demanda (<10%).

Tableau y R rondan los $92K–$93K, con demanda media (20–30%).

Estas son las habilidades que más impulsan el crecimiento salarial.

Skills con equilibrio ideal (alta demanda + buen salario)

Python, SQL y Tableau forman el triángulo de oro: demandadas por muchas empresas y con salarios competitivos.

Power BI y SAS también tienen un balance razonable (20% de demanda, ~$90K).

Skills menos óptimas (baja paga o poca demanda)

Word y PowerPoint están en el rango más bajo: relativamente presentes en algunos empleos pero con salarios medianos menores (~$81K–$86K).

Son útiles para comunicar resultados, pero no diferencian en compensación.