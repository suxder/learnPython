---

---

# learnPython
## Day 1

### 1.面向对象的设计思想是从自然界中来的，因为在自然界中，类（Class）和实例（Instance）的概念是很自然的。Class是一种抽象概念，比如我们定义的Class——Student，是指学生这个概念，而实例（Instance）则是一个个具体的Student，比如，Bart Simpson和Lisa Simpson是两个具体的Student。

### 2.和静态语言不同，Python允许对实例变量绑定任何数据，也就是说，对于两个实例变量，虽然它们都是同一个类的不同实例，但拥有的变量名称都可能不同：

```
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

## Day2（原稿已丢失）参考以下链接

[https://www.liaoxuefeng.com/wiki/1016959663602400/1017497232674368]: 

## Day3

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

```
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

```
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