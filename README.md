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

