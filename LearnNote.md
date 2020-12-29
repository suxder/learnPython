---

---

# learnPython
## 一、关于Python

### 1.面向对象的设计思想

面向对象的设计思想是从自然界中来的，因为在自然界中，类（Class）和实例（Instance）的概念是很自然的。Class是一种抽象概念，比如我们定义的Class——Student，是指学生这个概念，而实例（Instance）则是一个个具体的Student，比如，Bart Simpson和Lisa Simpson是两个具体的Student。

### 2.Python与静态语言的某些区别

和静态语言不同，Python允许对实例变量绑定任何数据，也就是说，对于两个实例变量，虽然它们都是同一个类的不同实例，但拥有的变量名称都可能不同：

```python 
>>> bart = Student('Bart Simpson', 59)
>>> lisa = Student('Lisa Simpson', 87)
>>> bart.age = 8 #给bart这个实例绑定一个属性age，值为8，而这个属性在类中是不存在的，所以其他实例直接引用该属性会报错
>>> bart.age
8
>>> lisa.age #age这个属性在lisa这个实例中是不存在的，所以会报错。
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Student' object has no attribute 'age'#报错“Student”对象没有“age”属性
```

### 3.Python语言的基本代码规范

1. Python语言一般一行写完一条语句，但是当一条语句过长时，可以使用斜杠(\)将一行的语句分为多行显示。
2. 另外，若语句中包含[ ]、{ }或()括号，就不需要使用多行连接符。

## 二、关于对象与实例

### 1.获取对象信息     

- 判断类型，使用tpye()函数

- 使用isinstance()

- **Tip: 总是优先使用isinstance()判断类型，可以将指定类型及其子类“一网打尽”。**

- 使用dir()获得一个对象的所有类型和方法。    


总结：通过内置的一系列函数

```
getattr()、setattr()、hasattr()
```

我们可以对任意一个Python对象进行剖析，拿到其内部的数据。要注意的是，只有在不知道对象信息的时候，我们才会去获取对象信息。

### 2.Animal.run和Animal().run 有什么区别？

- 永远记住，类只是一个模板，模板是不会亲自下海干活的。
- python中如果不加括号，除了个别的，那就是个标识符（你可以理解为变量）。加了括号代表运行前面的东西，比如f就是个标识符，f（）代表运行f。
- Animal(). run，如果Animal是个类，就代表先运行Animal这个类，记得前面章节说的，类运行变为实例，实例才能亲自下海干活。
- Animal(). run就是这个实例里的run函数（run没加括号表示没运行run，仅仅是个函数而已），Animal(). run（）就是先运行Animal生成一个实例，然后运行这个实例里的run函数。
- 你可以试一下Animal. run（）也就是运行Animal这个类里的run函数，会报错，告诉你缺少self，这个self是什么呢？就是你创建的实例。再回想一遍前面所说的，类只是个模板，打个比方，网站上的PPT模板怎么能干活呢，你得把它下载下来变成你的实例才能干活。而继承是什么呢，差不多就是，有人把PPT模板复制到另一个PPT模板中，变成了一个新模板（注意是模板）。而拿你的实例做一些东西，比如Animal().run（），或者a=animal();a. run（），就像是在给别人展示你的ppt（不是模板，网上ppt模板怎么能给别人展示呢？），你也可以稍加修改你的ppt（不是修改ppt模板），比如a. eye=blue。

### 3.    关于对实例属性的操作

```python 
class MyObject(object):
    def __init__(self):
        self.x = 9     #默认为9
    def power(self):
        return self.x * self.x
    def set_x(self, x):
        self.x = x

#类对象属性值无法修改
MyObjectMyObject().x    #结果不变，为9
MyObject().x = 2
MyObject().x    #结果不变，为9
setattr(MyObject(), 'x', 2)
MyObject().x    #结果不变，为9
MyObject().set_x(2)
MyObject().x    #结果不变，为9

#实例对象属性值可以修改
objobj = MyObject() #实例化
obj.x   #默认为9
obj.x = 2
obj.x   #结果变化为2
setattr(obj, 'x', 9)
obj.x   #结果变化为9
obj.set_x(2)
obj.x   #结果变化为2
```

```python
#类对象的内存地址每次变化
MyObject()  #第一次运行，输出<__main__.MyObject at 0x10efefc3a48>
MyObject()  #第二次运行，输出<__main__.MyObject at 0x10efed0d108>
MyObject()  #第三次运行，输出<__main__.MyObject at 0x10efefc3908>

#实例对象的内存地址引用固定
obj  #第一次运行，输出<__main__.MyObject at 0x10efed09248>
obj  #第二次运行，输出<__main__.MyObject at 0x10efed09248>
obj  #第三次运行，输出<__main__.MyObject at 0x10efed09248>
```

> 廖老师说：MyObject()就是实例，只是没有变量引用它，你就无法对他进行后续操作
>
> x=MyObject()就把实例引用给到变量x，用变量x可以操作实例，变量x的值就是实例地址
>
> 你别重新让x指向另一个实例，它的地址就永远不变
>
> y=x相当于x和y都指向同一个实例，两个变量的值相同
>
> MyObject是class，加个括号MyObject()表示创建并返回实例

**总结：在没有变量引用MyObject()的情况下，MyObject()只是存在临时地址上，所以后续的操作（赋值等）其实都没有用，不是对MyObject()的操作。相反，引用到变量后，变量x才可以影响实例。**

## 三、属性

### 1.实例属性和类属性

> 我们既可以给实例绑定属性，也可以给类绑定一个属性，当给类绑定属性后，有该类生成的所有实例都可以访问该类的属性。

**但要特别注意，禁止将类的属性名与实例的属性名设置为相同的。因为实例的优先级更高，实例的属性会屏蔽掉类的属性，在删除掉实例的属性后，访问实例的属性其实返回的是类的属性。**

### 2.关于 if \__name\__ == '\__main\__ ':

先编写一个测试模块*atestmodule.py*

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

' a test module '

def addFunc(a,b):  
    return a+b  

print('atestmodule计算结果:',addFunc(1,1))
```

再编写一个模块*anothertestmodule.py*来调用上面的模块：

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

' a test module '

import atestmodule

print('调用anothermodule模块执行的结果是：',atestmodule.addFunc(12,23))
```

在刚才两个模块的路径（我的路径为：*“C:\work”*）中打开cmd，用命令行运行*atestmodule.py*：

```
C:\work>python atestmodule.py
atestmodule计算结果: 2
```

在刚才两个模块的路径中打开，用命令行运行*anothertestmodule.py*：

```
C:\work>python anothertestmodule.py
atestmodule计算结果: 2
调用test模块执行的结果是： 35

#显然，当我运行anothertestmodule.py后第一句并不是调用者所需要的，为了解决这一问题，Python提供了一个系统变量：__name__

#注：name两边各有2个下划线__name__有2个取值：当模块是被调用执行的，取值为模块的名字；当模块是直接执行的，则该变量取值为：__main__
```

于是乎，被调用模块的测试代码就可以写在if语句里了，如下：

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

' a test module '

def addFunc(a,b):  
    return a+b  

if __name__ == '__main__':  
    print('atestmodule计算结果:',addFunc(1,1))
```

当再次运行*atestmodule.py*：

```
C:\work>python atestmodule.py
atestmodule计算结果: 2

#结果并没有改变，因为调用atestmodule.py时，__name__取值为__main__，if判断为真，所以就输出上面的结果
```

当再次运行*atestmodule.py*：

```
C:\work>python anothertestmodule.py
调用test模块执行的结果是： 35

#此时我们就得到了预期结果，不输出多余的结果。能实现这一点的主要原因在于当调用一个module时，此时的__name__取值为模块的名字，所以if判断为假，不执行后续代码。
```

所以代码*if **name** == '**main**':* 实现的功能就是**Make a script both importable and executable**，也就是说可以让模块既可以导入到别的模块中用，另外该模块自己也可执行。

### 3.HTTP请求流程

### 4.关于Python中抽象类的一点思考

#### 1.抽象类的作用

> 在不同的模块中通过抽象基类来调用，可以用最精简的方式展示出代码之间的逻辑关系，让模块之间的依赖清晰简单。
>
> 抽象类的编程，让每个人可以关注当前抽象类的方法和描述，而不需要考虑过多的实现细节，这对协同开发有很大意义，也让代码可读性更高。

如果我们定义一个抽象基类File

```python
import abc  # 利用abc模块实现抽象类

class File(metaclass=abc.ABCMeta):  # abc.ABCMeta是实现抽象类的一个基础类
    @abc.abstractmethod  # 定义抽象方法，无需实现功能
    def read(self):
        pass
```

- 该抽象基类有一个抽象方法`read`。

- 再定义其他子类的时候就必须重写`read`方法，但是不同的子类的read的方法的功能是不一样的，但我们无须关心这具体的实现方法。

- ```python
  class Txt(File):  # 子类继承抽象类，但是必须定义read方法将抽象类中的read方法覆盖
      def read(self):
          print('文本数据的读取方法')
  ```

- 如果我们不写这个抽象类，那么每个编程人员写出子类的实现**上述read方法**功能的**方法名字**都不一样，使得代码之间的逻辑关系混乱，代码的可读性降低。

- 从抽象基类继承出的子类，必须重写read，每个编程人员都得遵守。

- **从而提高了代码间的逻辑关系提高了代码的可读性。**

### 5.关于Python中类的self的一点思考

#### 1.属性（变量）

1.如果变量定义在类下面而不是类的方法下面，那这个变量既是类的属性也是类实例的属性  

无论是类还是实例 都可以 调用它

```python
class Test(object):
	a = 1
	b = 2
test1 = Test()
Test.a 
//1
test.a
//1
```

2.如果变量定义在类的方法下面，如果加了self，那这个变量就是类实例的属性，不是类的属性；如果没有加self，这个变量只是这个方法的局部变量，既不是类的属性也不是类实例的属性。

```python
class Test(object):
	def __init__(self):
        self.a = 1
        b = 2
test1 = Test()
test1.a 
//1
Test.a
//报错
test1.b
//报错
Test.b
//报错
```

#### 2.方法（函数）

## *随时补充

### 1.字符串与列表间的相互转换

#### 1.列表转字符串

> ‘分割符’.join(列表)

```python
#eg:  
lst = ['love','you']
b = ' '.join(lst) #分割符为' '(空格)
print(b)
#结果为:love you
```

Tip: 列表转字符串是无法强制类型转换的，即：

```python
# -*- coding: utf-8 -*-
list1 = ['I','love','you']
str1 = str(list1)
print(str1)
#结果为：['I', 'love', 'you']
```

#### 2.字符串转换为列表

> 字符串名.split()

```python
# eg:
b = 'love you'
lst = b.split(' ')
print(lst)
# 结果为:['love','you']
```

Tip：字符串是可以强制转换为列表的：

```python
# eg:
b = 'love you'
list1 = list(b)
print(list1)
# 结果为:['l', 'o', 'v', 'e', ' ', 'y', 'o', 'u']
```

