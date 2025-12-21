# Экологический мониторинг водных ресурсов

## Описание проекта

Проект направлен на эконометрический анализ зависимости между инвестициями в охрану окружающей среды и объёмом сброса загрязнённых сточных вод в региональном разрезе Российской Федерации. Исследование основано на панельных данных 83 регионов России с 2000 по 2023 год и включает множественное регрессионное моделирование с контрольными переменными, проверку через методы машинного обучения и анализ эффектов инвестиций в условиях различных уровней загрязнения.

## Актуальность

Проект опирается на **Постановление Правительства РФ**, согласно которому:
- Государственный экологический мониторинг, включая наблюдение за состоянием водных объектов, осуществляется через единую федеральную систему состояния окружающей среды
- Собственники водных объектов и водопользователи обязаны предоставлять сведения о результатах учета и наблюдений

Государство и регионы активно инвестируют в экологические мероприятия, но нуждаются в количественной оценке эффективности этих вложений на единицу снижения загрязнения.

## Цели проекта

- **Выявить зависимость** между инвестициями в охрану окружающей среды и объёмом сброса неочищенных сточных вод по регионам России
- **Идентифицировать скрытые факторы**, влияющие на загрязнение водных ресурсов (численность населения, урбанизация, использование свежей воды, промышленное производство)
- **Построить интерпретируемые регрессионные модели** с панельной структурой данных для оценки причинного эффекта инвестиций
- **Валидировать результаты** с помощью методов машинного обучения (Gradient Boosting, Random Forest)
- **Разработать рекомендации** по оптимальному распределению инвестиций в региональную водоохрану

## Бизнес-ценность

### Для региональных властей
- Обоснование объёма и направления инвестиций для максимизации экологического эффекта на единицу вложений (руб./м³ снижения сбросов)
- Возможность бенчмаркинга и сравнения эффективности между регионами
- Учет структурных факторов при планировании водоохранных программ

### Для крупных предприятий, банков и Сбера
- Использование результатов в ESG-оценке регионов и инвестиционных проектов
- Обоснование финансирования «зелёных» инициатив на основе данных
- Демонстрация эффективности экоинвестиций в нефинансовой отчётности

## Данные

### Источники
- **Росстат**: сборник «Регионы России. Социально-экономические показатели 2024»
- **ЕМИСС** (Единая межведомственная информационно-статистическая система)

### Состав датасета

**Экологические показатели:**

| Переменная | Описание | Примечание |
|-----------|---------|-----------|
| **Объём сточных вод (норм. по ВРП)** | Объём загрязнённых сточных вод | Нормализовано по ВРП, зависимая переменная |
| **Инвестиции в ООС (норм. по ВРП)** | Инвестиции в охрану окружающей среды | Нормализовано по ВРП, основной предиктор |

**Социально‑экономические показатели:**

| Переменная | Описание | Роль в анализе |
|-----------|---------|-----------|
| **Численность населения** | Абсолютное число жителей региона | Значимый фактор (сильный предиктор) |
| **Доля городского населения** | Процент населения в городах | Показатель урбанизации (значимый фактор) |
| **Использование свежей воды** | Объём водопотребления в регионе | Показатель водоинтенсивности (значимый фактор) |
| **Индекс промышленного производства** | Темп изменения объёмов промышленности | Контрольная переменная |
| **Индексы производства продукции сельского хозяйства** | Темп изменения АПК | Контрольная переменная |
| **ВРП на душу населения** | Валовой региональный продукт на одного жителя | Для кластеризации и масштабирования |

**Идентификационные переменные:**

| Переменная | Описание |
|-----------|---------|
| **Регион** | Название субъекта РФ (83 региона) |
| **Год** | Временной период (2000–2023 гг.) |

### Обработка данных

- **Исключённые регионы**: ДНР, ЛНР, Запорожская область, Херсонская область, Севастополь, Крым (недостаточно данных)
- **Обработка пропусков**: Чеченская Республика (строки 2000–2004 удалены из-за Второй Чеченской войны); Ингушетия (данные по инвестициям заполнены из Постановления Правительства Республики Ингушетии)
- **Нормализация**: все финансовые показатели приведены в расчёте на единицу ВРП для сравнимости

## Методология и инструменты

### Использованные методы

**Предварительная обработка данных**
- Нормализация по ВРП и другим масштабным показателям
- Обработка пропусков и выбросов
- Формирование панельной структуры (регионы × временные периоды)

**Регрессионный анализ**
- Линейная и множественная регрессия с оценкой статистической значимости коэффициентов
- Панельные модели с фиксированными региональными и временными эффектами (PanelOLS)
- Анализ коэффициентов регрессии, t-статистики и p-value

**Машинное обучение**
- Random Forest и Gradient Boosting для анализа нелинейных зависимостей
- Feature importance для определения вклада каждого признака
- Проверка устойчивости выводов классического анализа

**Визуализация и интерпретация**
- Распределения ключевых переменных
- Регрессионные графики по квартилям загрязнения (Q1–Q4)
- Графики важности признаков из ML моделей
- Сравнительные диаграммы эффектов инвестиций в разных группах регионов

### Технологический стек

- **Язык программирования**: Python 3.8+
- **Статистическое моделирование**: statsmodels, scikit-learn
- **Машинное обучение**: XGBoost, RandomForest
- **Панельные данные**: linearmodels (PanelOLS с fixed effects)
- **Обработка данных**: pandas, numpy
- **Визуализация**: matplotlib, seaborn, plotly

## Основные результаты

### Главные факторы загрязнения водных ресурсов
1. **Численность населения** (самый сильный фактор)
2. **Доля городского населения** (урбанизация)
3. **Использование свежей воды** (водопотребление)

### Эффект инвестиций
- Инвестиции в водоохрану — **необходимый и работающий инструмент**, но их эффект скрыт более мощными структурными факторами
- Объём сточных вод в первую очередь зависит от масштаба и структуры экономики, а не от доли инвестиций
- **Наибольший эффект** достигается в регионах с высокими начальными объёмами загрязнения

## Рекомендации по распределению инвестиций

1. **Прекратить "распыление"** инвестиций в регионах с малыми объёмами сточных вод — переделать программы, не увеличивать бюджет

2. **Инвестировать в комплексе** с управлением структурными факторами: контроль численности, урбанизации, водопотребления

3. **Увеличивать финансирование** при ускоренном росте населения и урбанизации: при росте городского населения на 10% выше среднего пересчитывать инвестиционную норму вверх

4. **Приоритизировать** высокозагрязненные регионы (Q4), где подтверждён статистический эффект инвестиций

## Перспективы развития

- Автоматизация обучения моделей при появлении новых официальных данных
- Расширение анализа на другие экологические показатели (качество воздуха, загрязнение почв)
- Детализация структуры инвестиций: анализ влияния отдельных видов расходов на водоохрану
- **Финальный результат**: создание рекомендательной системы и цифрового сервиса, показывающего целесообразность инвестиций и эффект на единицу вложений

## Структура репозитория

- **data/** — исходные и подготовленные датасеты
  - **raw/** - черновики
  - `main_dataset.csv` — основной датасет (83 региона, 2000-2023)
- **notebooks/** — примеры анализа и визуализации
  - **raw/** - черновики
- **analysis/** — результаты анализа и отчёты
  - **results/** — графики и диаграмм
  - **analysis_2_2/** — сохранённые модели и результаты
- **README.md** — описание проекта

---

## Авторы

Студенты УрФУ, 2025

# Environmental Monitoring of Water Resources

## Project Description

This project conducts an econometric analysis of the relationship between investments in environmental protection and the volume of polluted wastewater discharge across Russian regions. The research uses panel data from 83 Russian regions covering 2000–2023 and includes multiple regression modeling with control variables, machine learning validation (Gradient Boosting, Random Forest), and analysis of investment effects under varying pollution levels.

## Relevance

The project is grounded in **Russian Government Decree**, which establishes that:
- State environmental monitoring, including water body condition assessment, operates through a unified federal environmental information system
- Water resource owners and users must report monitoring results and observations

Governments and regional authorities invest heavily in environmental initiatives but require quantitative measurement of effectiveness per unit of pollution reduction.

## Project Goals

- **Identify the relationship** between environmental protection investments and polluted wastewater discharge across Russian regions
- **Detect hidden factors** affecting water pollution (population size, urbanization, freshwater use, industrial output)
- **Build interpretable regression models** with panel structure to estimate causal investment effects
- **Validate results** using machine learning methods (Gradient Boosting, Random Forest)
- **Develop recommendations** for optimal allocation of water protection investments

## Business Value

### For Regional Authorities
- Justification for investment volume and direction to maximize environmental impact per ruble spent (RUB/m³ discharge reduction)
- Benchmarking and efficiency comparison across regions
- Structural factors accounting in water protection program planning

### For Large Enterprises, Banks, and Sberbank
- ESG rating and assessment of regions and investment projects
- Evidence-based justification for green initiative financing
- Demonstrated investment effectiveness for non-financial reporting

## Data

### Sources
- **Rosstat**: "Regions of Russia. Socio-Economic Indicators 2024"
- **EMISS** (Unified Interdepartmental Information-Statistical System)

### Dataset Composition

**Environmental Indicators:**

| Variable | Description | Note |
|-----------|---------|-----------|
| **Wastewater volume (norm. by GRP)** | Volume of polluted wastewater discharge | Normalized by GRP, dependent variable |
| **Environmental investments (norm. by GRP)** | Investments in environmental protection | Normalized by GRP, main predictor |

**Socio-Economic Indicators:**

| Variable | Description | Role in Analysis |
|-----------|---------|-----------|
| **Population size** | Absolute number of regional residents | Significant factor (strong predictor) |
| **Urban population share** | Percentage of population in cities | Urbanization indicator (significant factor) |
| **Freshwater use** | Water consumption volume in region | Water intensity indicator (significant factor) |
| **Industrial production index** | Rate of change in industrial output | Control variable |
| **Agricultural production indices** | Rate of change in agriculture | Control variable |
| **GRP per capita** | Gross regional product per resident | For clustering and scaling |

**Identification Variables:**

| Variable | Description |
|-----------|---------|
| **Region** | Name of RF subject (83 regions) |
| **Year** | Time period (2000–2023) |

### Data Processing
- **Excluded regions**: DNR, LNR, Zaporizhzhia, Kherson, Sevastopol, Crimea (insufficient data)
- **Missing data handling**: Chechen Republic (2000–2004 removed); Ingushetia (investments filled from official decree)
- **Normalization**: Financial indicators scaled by GRP for comparability

## Methodology and Tools

### Methods Used

**Data Preprocessing**
- Normalization by GRP and other scale indicators
- Handling missing values and outliers
- Formation of panel structure (regions × time periods)

**Regression Analysis**
- Linear and multiple regression with statistical significance testing
- Panel models with fixed regional and temporal effects (PanelOLS)
- Coefficient analysis, t-statistics, and p-value interpretation

**Machine Learning**
- Random Forest and Gradient Boosting for nonlinear relationship analysis
- Feature importance to determine contribution of each variable
- Robustness validation of classical analysis conclusions

**Visualization & Interpretation**
- Distribution plots of key variables
- Regression plots by pollution quartiles (Q1–Q4)
- Feature importance graphs from ML models
- Comparative diagrams of investment effects across region groups

### Technology Stack

- **Language**: Python 3.8+
- **Statistical Modeling**: statsmodels, scikit-learn
- **Machine Learning**: XGBoost, RandomForest
- **Panel Data**: linearmodels (PanelOLS with fixed effects)
- **Data Processing**: pandas, numpy
- **Visualization**: matplotlib, seaborn, plotly

## Key Findings

### Primary Pollution Drivers
1. Population size (strongest)
2. Urbanization rate
3. Freshwater use and industrial production

### Investment Effect
- Environmental investments **work** but are **overshadowed by structural factors**
- Wastewater volume depends primarily on regional economic scale, not investment variation
- **Most effective** in highly polluted regions with sustained problems

## Investment Allocation Recommendations

1. **Stop dispersed spending** in low-pollution regions; restructure programs rather than increase budgets

2. **Combine investments** with structural factor management; economic structure explains discharge variation more than investments alone

3. **Scale up funding** with accelerating population growth and urbanization (adjust investment norms +X% per 10% urban growth)

4. **Prioritize high-pollution regions** where investment effect is statistically confirmed

## Future Development

- Automate model training when new official data becomes available
- Expand analysis to other environmental indicators (air quality, soil pollution)
- Detailed investment analysis: examine impact of specific spending categories
- **Final outcome**: Create a recommendation system and digital service demonstrating investment effectiveness per unit spending

## Repository Structure

- **data/** — raw and processed datasets
  - **raw/** — drafts
  - `main_dataset.csv` — main dataset (83 regions, 2000-2023)
- **notebooks/** — analysis and visualization examples
  - **raw/** — drafts
- **analysis/** — analysis results and reports
  - **results/** — plots and diagrams
  - **analysis_2_2/** — saved models and results
- **README.md** — project description

---

## Authors

UrFU Students, 2025
