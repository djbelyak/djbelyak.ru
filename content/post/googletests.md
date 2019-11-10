+++
title = "Googletest - unit testing framework"
date = 2019-03-19T08:09:24+03:00
draft = false

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["cpp", "unit-testing", "googletest"]
categories = []

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
[image]
  # Caption (optional)
  caption = ""

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""
+++

Googletest (Gtest) -- фреймворк для юнит-тестов для C++ кода.
Этот фреймворк сделан под влиянием xUnit фреймворков.

Visual Studio 2017 имеет встроенный компонент для поддержки Gtest.
Чтобы начать работу необходимо в текущем Solution надо создать проект GTest.
При создании проекта нужно удостоверится, что C++ runtime прилинкован как динамическая библиотека, а GTest - как статическая библиотека.
Также необходимо добавить ссылки на проекты, где содержится тестируемый код (References->Add).

Проект по умолчанию содержит один демонстрационный тест.
Для запуска Gtest надо вызвать команду Test->Run->All tests.
Либо воспользоваться клавиатурной комбинацией `Ctrl+R, A`.
Также можно запустить тесты в режиме отладчика: Test->Debug->All tests или `Ctrl+R, Ctrl+A`.

Один тест -- это одна функция вида:

```cpp
TEST(<TestSuiteName, TestName>)
{
  ASSERT_TRUE(False);
}
```

Существует 2 вида проверок: `ASSERT_*` - падение проверки прерывает выполнение теста, `EXPECT_*` - падение проверки не приводит к прерыванию теста.
В документации рекомендуется использовать `EXPECT_*` как можно чаще, чтобы за один прогон тестов было собрано как можно больше информации об ошибках.

Наиболее часто используются следующие проверки:

- `ASSERT_TRUE(value)` - проверяет, что `value==True`;
- `ASSERT_FALSE(value)` - проверяет, что `value==False`;
- `ASSERT_EQ(a, b)` - проверяет, что `a==b`;
- `ASSERT_NE(a, b)` - проверяет, что `a!=b`;
- `ASSERT_LT(a, b)` - проверяет, что `a<b`;
- `ASSERT_LE(a, b)` - проверяет, что `a<=b`;
- `ASSERT_GT(a, b)` - проверяет, что `a>b`;
- `ASSERT_GE(a, b)` - проверяет, что `a>=b`;
- `ASSERT_STREQ(a, b)` - проверяет, что C-style строки равны (не работает для std::string).

Для того, чтобы тесты не падали с ошибкой компановщика в `include` секции теста надо подключать и `.h`, и `.cpp` файлы с тестируемым кодом.

## Ссылки

1. [Googletest](https://github.com/google/googletest)
1. [How to use Google Test for C++ in Visual Studio](https://docs.microsoft.com/ru-ru/visualstudio/test/how-to-use-google-test-for-cpp?view=vs-2017)