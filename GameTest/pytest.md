## python中功能最强大的单元测试框架
- ## 默认运行时，要求文件名必须以test_打头或者_test.py结尾，否则默认会提示找不到用例
- ## 编写代码，可以和unittest相同定义测试类、测试方法，也可以直接定义测试函数、不定义测试类
- ## 定义类语法: class Test打头的类名，不需要继承任何父类
- ## 定义测试函数和测试方法语法:def test打头的函数或方法名
- ## 测试中的断言，pytest默认只有assert 一种方式 只判断bool值
- ## 官方推荐的执行测试的方法，终端中执行命令pytest `[选项]` `[参数]`

# 参数：
# 空，表示运行当前目录中所有满足文件名要求的脚本中的pytest测试方法和测试函数。文件名要求是test_打头或_test.py结尾
# 目录，表示运行指定目录中所有满足文件名要求的脚本中的pytest测试方法和测试函数。
# 文件名，表示运行指定脚本中的pytest测试方法和测试函数。不要求脚本文件名必须满足test_打头或_test.py结尾
# 文件名::测试类名，表示运行指定脚本中的指定测试类中的所有测试方法。
# 文件名::测试类名::测试方法名，表示运行指定脚本中的指定测试类中的指定测试方法。
# 文件名::测试函数名，表示运行指定脚本中的指定测试函数。

## 选项:
- -k:文件名、类名等模糊匹配 :pytest -k 'aa' and not 'bb'
- -m:匹配代码中的标签:@pytest.mark
- -vs:不拦截代码中print语句以及出现详细信息
- -lf:只上次失败的测试，若没有失败则全部执行
- `--`html生成html测试报告 --html 路径/report.html 路径/test_01.py

## 前后置

```python
def setup_function():#函数级前置方法
def setup_method():

def setup_class():#与unittest setUpClass一样
def setup_module():#模块级前置方法所有类，函数，方法的前置

#后置
def teardown_***()

```
pytest的夹具:fixture 是一种生成器
```python
@pytest.fixture
def myFixture():
	print('测试开始')
	yield#表示暂停返回，作用类似于return,回来后执行下半代码
	print('测试结束')
```
夹具的使用方式为参数
多种夹具一起使用，参数在左边靠前的为先执行（包在外面）
```python
@pytest.fixture
def myFixture1():   
# 定义一个函数，使用@pytest.fixture装饰器来装饰，则该函数就是一个自定义夹具，具有前后置的作用
    print('夹具1开始')   # yield之前的代码就是前置
    yield   
    # 使用关键字yield实现前置内容执行结束后暂停，转去执行具体测试，具体测试完成后，再返回到此继续执行后续代码，实现后置内容。
    print('夹具1结束')   # yield之后的代码就是后置

@pytest.fixture
def myFixture2():
    print('夹具2开始')
    yield
    print('夹具2结束')

class Test1:
    def test_1(self,myFixture1):
        print('test1')
        assert 1 == 1
    def test_2(self, myFixture2):
        print('test2')
        assert 1 == 1
def test_3(myFixture1, myFixture2):
    print('test3')
    assert 1 == 1

def test_4(myFixture2, myFixture1):
    print('test3')
    assert 1 == 1
```

夹具的级别，通过函数定义时使用的装饰器带scope参数来定义该夹具的等级
```python
#函数级也用于方法(默认)
@pytest.fixture(scope='function')
#类级，用于测试类
```