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

![Distribución de Salarios por puesto de Data](3_Project\images\distribucion de salario.png)