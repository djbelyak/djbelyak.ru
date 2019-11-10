+++
tags = ["TensorFlow", "High Level API", "Датасет", "Dataset"]
highlight = true
math = false
date = "2018-03-31T20:00:00+03:00"
title = "Как загрузить датасет в TensorFlow"
draft = false

[header]
  caption = ""
  image = ""

+++

Высокоуровневый процесс обучения в фреймворке TensorFlow консолидируется вокруг объекта класса `Estimator` и его наследников.
Для обучения, оценки и вывода результата каждый такой объект содержит методы `train`, `evaluate` и `predict` соответственно.
Эти методы в качестве аргумента принимают некую функцию `input_fn`, которая отвечает за загрузку данных для искусственной нейронной сети.
В этом посте мы подробно рассмотрим как создается такая функция.

<!--more-->

Согласно описанию, `input_fn` вызывается на каждом шаге процесса.
Ожидается, что каждый вызов `input_fn` вернет либо один семпл из набора данных, либо несколько семплов, объединенных в batch.
При этом для методов `train` и `evaluate` ожидается кортеж тензоров: первый тензор --- входные параметры (в терминах TF: features), второй тензор --- ожидаемые выходные значения (в терминах TF: labels).

Получается, что `input_fn` должна возвращать специфический итератор.
Класс этого итератора объявлен в пакeте `tf.data` и называется `Iterator`.
Чтобы получить семпл или batch нужно вызвать метод `get_next`.
Таким образом уже можно описать конец функции:

```python
def input_fn():
    # some operations

    # make Iterator object
    # iterator = ...
    return iterator.get_next()
```

Поднимаясь далее вверх по коду, возникает вопрос каким образом создать объект итератора.
Есть два способа: использовать статические методы класса `Iterator` или воспользоваться методами `make_one_shot_iterator` и `make_initializable_iterator` объектов класса `Dataset` и производных.
Руководство программиста рекомендует использовать метод `make_one_shot_iterator`, так как он не требует дополнительной инициализации.
Обновим функцию `input_fn`:

```python
def input_fn():
    # Make Dataset 
    # dataset = ...

    # some operations

    iterator = dataset.make_one_shot_iterator()
    return iterator.get_next()
```

Теперь надо создать объект класса `Dataset`.
В модуле `tf.data` уже есть несколько классов для работы с конкретными форматами:

* Класс `TextLineDataset` позволяет сформировать датасет, читая строки из текстовых файлов;
* Класс `FixedLengthRecordDataset` позволяет сформировать датасет, читая фиксированный байтовый размер из бинарных файлов;
* Класс `TFRecordDataset` позволяет сформировать датасет, читая файлы в формате TensorFlow.

Если ни один из классов не подошел, то можно воспользоваться статическими методами класса `Dataset`:

* `range` -- создает набор данных из заданной последовательности;
* `zip` -- объединяет два датасета в кортеж датасетов;
* `from_tensor_slice` -- создает датасет из слайсов тензоров;
* `from_tensors` -- создает единый датасет из списка тензоров;
* `list_files` -- создает датасет из списка файлов;
* `from_generator` --- создает датасет по заданному генератору.

Наиболее гибким является метод `from_generator`.
Добавим в функцию `input_fn` генерацию простого датасета:

```python
def input_fn():
    # Dataset generator
    def dataset_generator():
        for i in range(10):
            yield (i*1.0, i*2.0)

    # Make Dataset
    dataset = tf.data.Dataset.from_generator(
        dataset_generator,
        (tf.float32, tf.float32),
        (tf.TensorShape(None), tf.TensorShape(None))
    )

    # some operations

    iterator = dataset.make_one_shot_iterator()
    return iterator.get_next()
```

Такая функция уже вполне жизнеспособна.
Она будет возвращать по одному примеру за раз и на каждой итерации порядок семплов будет неизменным.
Возвращать по одному примеру за раз не эффективно с точки зрения обработки, поэтому объект `Dataset` может объединить несколько семплов в batch.
Чтобы это сделать нужно вызвать метод `batch` и в качестве параметра указать количество семплов.
Метод вернет новый объект `Dataset`, итератор которого уже будет возвращать йелый batch.
Для того, чтобы перемешать семплы объект `Dataset` имеет метод `shuffle`, в котором задается размер буфера для перемешивания.

Таким образом конечная функция будет выглядеть следующим образом:

```python
def input_fn():
    # Dataset generator
    def dataset_generator():
        for i in range(10):
            yield (i*1.0, i*2.0)

    # Make Dataset
    dataset = tf.data.Dataset.from_generator(
        dataset_generator,
        (tf.float32, tf.float32),
        (tf.TensorShape(None), tf.TensorShape(None))
    )

    # Shuffle and batch
    dataset = dataset.shuffle(10)
    dataset = dataset.batch(5)

    iterator = dataset.make_one_shot_iterator()
    return iterator.get_next()
```

Ести нужно провести более сложную обработку, то можно вызвать метод `map` и в качестве параметра передать функцию для обработки, которая на вход получает исходный кортеж семплов и возвращает уже обработанный кортеж.
Важно помнить, что семплы -- это тензоры, и операции должны производиться как с тензорами.
Больше примеров можно найти по ссылкам ниже.

### Ссылки

1. [tf.estimator.Estimator](https://www.tensorflow.org/api_docs/python/tf/estimator/Estimator#evaluate)
1. [Importing Data](https://www.tensorflow.org/programmers_guide/datasets)
1. [tf.data.Iterator](https://www.tensorflow.org/api_docs/python/tf/data/Iterator)
1. [tf.data.Dataset](https://www.tensorflow.org/api_docs/python/tf/data/Dataset)
1. [Итерируемый объект, итератор и генератор](https://habrahabr.ru/post/337314/)
