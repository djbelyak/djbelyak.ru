+++
title = "Criticality margin evaluation software for WWR-c reactor"
date = "2018-07-31"

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["I.P. Belyavtsev", "S.O. Starkov"]

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
publication = "Izvestiya vuzov. Yadernaya Energetika"
publication_short = "Izvestiya vuzov. Yadernaya Energetika"

# Abstract and optional shortened version.
abstract = """The criticality margin of a WWR-c reactor can be calculated using a precision reactor model. However, due to the high computing time consumption (approximately eight hours of calculations per one state of the reactor core), it would be rather difficult to use this model for making operational criticality margin evaluations. This problem has determined the purpose of this work, namely, to create a software package for preliminary evaluations of the WWR-c reactor criticality margin.

The research has confirmed the possibility of using an artificial neural network to approximate the criticality margin based on the reactor core state. A number of computational experiments were conducted on training the artificial neural network, using the precision model data and real reactor measured data. According to the results of these computational experiments, the maximum relative approximation error was found to be 3.13 and 3.56%, respectively. The mean computation time was 100 ms.

Based on these experiments, it became possible to develop a software package for evaluating the WWR-c reactor criticality margin – REST API based web application – which has a convenient user interface for inputting the core configurations and obtaining evaluations. Besides that, it is also possible to supplement the training sample with new measurements and to finish training the artificial neural network.

The criticality margin evaluation software is ready to be tested by the WWR-c reactor personnel as well as to be used as a component of the automated reactor refueling system. In future, with some modifications, this software package can be used for reactor plants of other types."""

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

### DOI

https://doi.org/10.26583/npe.2018.2.06

### References

1. Kochnov O.Yu., Lukin N.D, Averin L.V. WWR-c reactor: exploitation experience and development prospects. Yadernaya i radiatsionnaya bezopasnost’, 2008, no.1, pp. 18-25 (in Russian).
2. Kolesov V.V., Kochnov О.Yu., Volkov Yu.V., Ukraintsev V.F., Fomin R.V. Creation of the WWR-c Reactor Precision Model for Its Construction Optimisation and Following Optimisation of the 99Мо and Other Radioisotope Productivity. Izvestia vysshikh uchebnykh zavedenij. Yadernaya energetika. 2011, no. 4, pp. 129-133 (in Russian).
3. Kochnov O.Yu. Kolesov V.V. Fomin R.V. Jerdev G.M. Assessment of the increasing in 131I production due to improved tellurium target in the WWR-C reactor core. Izvestia vysshikh uchebnykh zavedenij. Yadernaya energetika. 2014, no.4, pp. 102-110 (in Russian).
4. Simon Haykin. Neural networks. A Comprehensive Foundation. Second Edition. Prentice Hall, Inc., 1999. 1104 p.
5. Filatova T.V. Application of neural networks for data approximation. Vestnik Tomskogo gosudarstvennogo universiteta. 2004, no.284, pp. 121-125 (in Russian).
6. Gorban’ A.N. Generalized approximation theorem and computational capabilities of neural networks. Sibirskij zhurnal vychislitel’noy matematiki. 1998, v. 1, no. 1, pp. 12-24 (in Russian).
7. Belyavtsev I., Legchikov D., Starkov S., Kolesov V., Nikulin E. Approximation of the criticality margin of WWR-c reactor using artificial neuron networks. Journal of Physics: Conference Series. 2018, v. 945, pp. 012-031.
8. Abadi M., Barham P., Chen J., Chen Zh., Davis A., Dean J., Devin M., Ghemawat S., Irving G., Isard M., Kudlur M., Levenberg J., Monga R., Moore Sh., Murray D., Steiner B., Tucker P., Vasudevan V., Warden P., Wicke M., Yu Yu., Zheng X. TensorFlow: Large-scale machine learning on heterogeneous systems. – 2015. Available at: https://www.tensorflow.org/about/bib (accessed May 2, 2018).
9. Zaccone G. Getting Started with TensorFlow. Packt Publishing, 2016. 180 p.
10. Lieder I., Resheff Y., Hope T. Learning TensorFlow. A Guide to Building Deep Learning Systems. O’Reilly Media, 2017, 242 p.
11. You E.VueJs. Available at: https://vuejs.org/v2/guide/ (accessed May 2, 2018).
12. Filipova O. Learning Vue.js 2. Learn how to build amazing and complex reactive web applications easily with Vue.js. Packt Publishing, 2016. 334 p.
13. Street M. Vue.js 2.x by Example. Packt Publishing, 2017. 412 p.
14. Ronacher A. Flask. Available at: http://flask.pocoo.org/ (accessed May 2, 2018).
15. Grinberg M. Flask Web Development, 2nd Edition. O’Reilly Media, 2018. 316 p.
16. Dwyer G. Flask by Example. Packt Publishing, 2016. 276 p.
17. Masse M. REST API Design Rulebook. O’Reilly Media, 2011. 116 p.
18. Richardson L., Ruby S. RESTful Web Services. O’Reilly Media, 2008. 448 p.
