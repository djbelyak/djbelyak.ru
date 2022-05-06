+++
title = "Программный комплекс оценки запаса реактивности реактора ВВР-ц"
date = "2018-07-31"

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["И.П. Белявцев", "С.О. Старков"]

# Publication type.
# Legend:
# 0 = Uncategorized
# 1 = Conference proceedings
# 2 = Journal
# 3 = Work in progress
# 4 = Technical report
# 5 = Book
# 6 = Book chapter
publication_types = ["2"]

# Publication name and optional abbreviated version.
publication = "Известия высших учебных заведений. Ядерная энергетика"
publication_short = "Известия вузов. Ядерная энергетика"

# Abstract and optional shortened version.
abstract = ""

# Featured image thumbnail (optional)
image_preview = ""

# Is this a selected publication? (true/false)
selected = true

# Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter the filename (excluding '.md') of your project file in `content/project/`.
#projects = ["example-external-project"]

# Links (optional).
url_pdf = "https://static.nuclear-power-engineering.ru/articles/2018/02/06.pdf"
#url_preprint = "http://iopscience.iop.org/article/10.1088/1742-6596/945/1/012031"
#url_code = "#"
#url_dataset = "#"
#url_project = "#"
#url_slides = "#"
#url_video = "#"
#url_poster = "#"
#url_source = "#"

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{name = "Custom Link", url = "http://example.org"}]

# Does the content use math formatting?
math = true

# Does the content use source code highlighting?
highlight = true

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
[header]
#image = "headers/bubbles-wide.jpg"
#caption = "My caption :smile:"

+++

**Авторы**: И.П. Белявцев, С.О. Старков

Запас реактивности реактора ВВР-ц [1] можно рассчитать с помощью прецизионной модели реактора. Прецизионная модель, основанная на методе Монте-Карло [2], мало пригодна для оперативных расчетов. Представлена работа по созданию программного комплекса предварительной оценки запаса реактивности реактора ВВР-ц. Обоснована возможность применения искусственной нейронной сети для построения аппроксимации запаса реактивности реактора по состоянию активной зоны. Проведены вычислительные эксперименты по обучению искусственной нейронной сети на данных прецизионной модели и на измеренных данных реального реактора. По итогам вычислительных экспериментов максимальная относительная ошибка аппроксимации Δk/k от глубины выгорания составила 3,13 и 3,56% соответственно. Среднее время расчета – 100 мс. В ходе вычислительных экспериментов была построена архитектура искусственной нейронной сети. Данная архитектура стала основой для построения программного комплекса оценки запаса реактивности реактора ВВР-ц – REST API веб-приложения, имеющего удобный пользовательский интерфейс для ввода конфигурации активной зоны. Есть возможность дополнить обучающую выборку новыми измерениями и доучить искусственную нейронную сеть. Программный комплекс для оценки запаса реактивности готов для тестирования персоналом реактора ВВР-ц и использования его в виде компонента системы автоматического планирования перезагрузки реактора. С незначительными изменениями комплекс можно применять для реакторных установок других типов.

### DOI

<https://doi.org/10.26583/npe.2018.2.06>

### Ссылки

1. Кочнов О.Ю., Лукин Н.Д, Аверин Л.В. Реактор ВВР-ц: опыт эксплуатации и перспективы развития. // Ядерная и радиационная безопасность. – 2008. – №1. – С. 18-25.
1. Колесов В.В., Кочнов О.Ю., Волков Ю.В., Украинцев В.Ф., Фомин Р.И. Создание прецизионной модели реактора ВВР-ц для последующей оптимизации его конструкции и наработки 99Mo и других радионуклидов. // Известия высших учебных заведений. Ядерная энергетика. – 2011. – №4. – С. 129-133.
1. Кочнов О.Ю., Колесов В.В., Фомин Р.И., Жердев Г.М. Оценка увеличения производства 131I при использовании теллуровых мишеней усовершенствованной конструкции на реакторе ВВР-ц. // Известия высших учебных заведений. Ядерная энергетика. – 2014. – №4. – С. 102-110.
1. Хайкин С. Нейронные сети. Полный курс. – М.: Издательский дом «Вильямс». – 2006. – 1104 с.
1. Филатова Т.В. Применение нейронных сетей для аппроксимации данных // Вестник Томского государственного университета. – 2004. – №284. – C. 121–125.
1. Горбань А. Н. Обобщенная аппроксимационная теорема и вычислительные возможности нейронных сетей. // Сибирский журнал вычислительной математики. – 1998. – Т. 1. – №1. – С. 12-24.
1. Belyavtsev I., Legchikov D., Starkov S., Kolesov V., Nikulin E. Approximation of the criticality margin of WWR-c reactor using artificial neuron networks // Journal of Physics: Conference Series. – 2018. – Т. 945. – PP. 012–031.
1. Abadi M., Barham P., Chen J., Chen Zh., Davis A., Dean J., Devin M., Ghemawat S., Irving G., Isard M., Kudlur M., Levenberg J., Monga R., Moore Sh., Murray D., Steiner B., Tucker P., Vasudevan V., Warden P., Wicke M., Yu Yu., Zheng X. TensorFlow: Large-scale machine learning on heterogeneous systems. – 2015. Электронный ресурс: https://www.tensorflow.org/about/bib (дата обращения 2.05.2018)
1. Zaccone G. Getting Started with TensorFlow. – Packt Publishing – 2016. – 180 p.
1. Lieder I., Resheff Y., Hope T. Learning TensorFlow. A Guide to Building Deep Learning Systems. – O’Reilly Media. – 2017. – 242 p.
1. You E. VueJs. Электронный ресурс: https://vuejs.org/v2/guide/ (дата обращения 2.05.2018).
1. Filipova O. Learning Vue.js 2. Learn how to build amazing and complex reactive web applications easily with Vue.js. – Packt Publishing. – 2016. – 334 p.
1. Street M. Vue.js 2.x by Example. – Packt Publishing. – 2017. – 412 p.
1. Ronacher A. Flask. Электронный ресурс: http://flask.pocoo.org/ (дата обращения 2.05.2018).
1. Grinberg M. Flask Web Development, 2nd Edition. – O’Reilly Media. – 2018. – 316 p.
1. Dwyer G. Flask by Example. – Packt Publishing. – 2016. – 276 p.
1. Masse M. REST API Design Rulebook. – O’Reilly Media. – 2011. – 116 p.
1. Richardson L., Ruby S. RESTful Web Services. – O’Reilly Media. – 2008. – 448 p.
