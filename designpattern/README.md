# 设计模式


## 六大基本准则


### 单一职责原则 (Single Responsibility Principle)

* There should never be more than one reason for a class to change.

职责是指类变化的原因, 一个类应该只负责一项职责, 否则应该被拆分

### 里氏替换原则 (Liskov Substitution Principle)

* Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.

里氏替换原则是对开闭原则的补充, 是对实现抽象化的具体步骤的规范, 继承必须确保父类所拥有的性质在子类中仍然成立(Inheritance should ensure that any property proved about supertype objects also holds for subtype objects), 父类出现的地方可以用子类来替换

1. 子类必须完全实现父类的方法
2. 子类可以有自己的属性和方法
3. 覆盖或实现父类的方法时输入参数可以被放大
4. 覆写或实现父类的方法时输出结果可以被缩小

### 依赖倒置原则 (Dependence Inversion Principle)

* High level modules should not depend upon low level modules.Both should depend upon abstractions.Abstractions should not depend upon details.Details should depend upon abstractions.

高层模块不应该依赖低层模块, 两者都应该依赖其抽象; 抽象不应该依赖细节, 细节应该依赖抽象, 其核心思想是:要面向接口编程, 不要面向实现编程

依赖倒置原则是实现开闭原则的重要途径之一, 它降低了客户与实现模块之间的耦合由于在软件设计中, 细节具有多变性, 而抽象层则相对稳定, 因此以抽象为基础搭建起来的架构要比以细节为基础搭建起来的架构要稳定得多这里的抽象指的是接口或者抽象类, 而细节是指具体的实现类

### 接口隔离原则 (Interface Segregation Principle)

* Clients should not be forced to depend upon interfaces that they don’t use.
* The dependency of one class to anther one should depend on the smallest possible interface.

客户端不应该依赖它不需要的接口, 类间的依赖关系应该建立在最小的接口上, 尽量将臃肿庞大的接口拆分成更小的和更具体的接口, 让接口中只包含客户端需要的方法

接口隔离原则和单一职责都是为了提高类的内聚性、降低它们之间的耦合性, 体现了封装的思想, 但两者是不同的:

1. 单一职责原则注重的是职责, 而接口隔离原则注重的是对接口依赖的隔离
2. 单一职责原则主要是约束类, 它针对的是程序中的实现和细节; 接口隔离原则主要约束接口, 主要针对抽象和程序整体框架的构建

### 迪米特法则 (Demeter Principle)

* Talk only to your immediate friends and not to strangers.

也叫最少知道原则, 一个类对自己依赖的类知道的越少越好, 如果两个软件实体无需直接通信, 那么就不应当发生直接的相互调用, 可以通过第三方转发该调用其目的是降低类之间的耦合度, 提高模块的相对独立性

迪米特法则中的“朋友”是指:当前对象本身、当前对象的成员对象、当前对象所创建的对象、当前对象的方法参数等, 这些对象同当前对象存在关联、聚合或组合关系, 可以直接访问这些对象的方法

从迪米特法则的定义和特点可知, 它强调以下两点:

1. 从依赖者的角度来说, 只依赖应该依赖的对象
2. 从被依赖者的角度说, 只暴露应该暴露的方法

在运用迪米特法则时要注意以下 6 点:

1. 在类的划分上, 应该创建弱耦合的类类与类之间的耦合越弱, 就越有利于实现可复用的目标
2. 在类的结构设计上, 尽量降低类成员的访问权限
3. 在类的设计上, 优先考虑将一个类设置成不变类
4. 在对其他类的引用上, 将引用其他对象的次数降到最低
5. 不暴露类的属性成员, 而应该提供相应的访问器（set 和 get 方法）
6. 谨慎使用序列化（Serializable）功能

缺点:
过度使用迪米特法则会使系统产生大量的中介类, 从而增加系统的复杂性, 使模块之间的通信效率降低所以, 在釆用迪米特法则时需要反复权衡, 确保高内聚和低耦合的同时, 保证系统的结构清晰

### 开闭原则 (Open Close Principle)

* Software entities like classes, modules and functions should be open for extension but closed for modifications.

软件实体应当对扩展开放, 对修改关闭

这里的软件实体包括以下几个部分:
1. 项目中划分出的模块
2. 类与接口
3. 方法

开闭原则的含义是:当应用的需求改变时, 在不修改软件实体的源代码或者二进制代码的前提下, 可以扩展模块的功能, 使其满足新的需求

开闭原则是面向对象程序设计的终极目标, 它使软件实体拥有一定的适应性和灵活性的同时具备稳定性和延续性具体来说, 其作用如下

1. 对软件测试的影响, 软件遵守开闭原则的话, 软件测试时只需要对扩展的代码进行测试就可以了, 因为原有的测试代码仍然能够正常运行
2. 可以提高代码的可复用性, 粒度越小, 被复用的可能性就越大; 在面向对象的程序设计中, 根据原子和抽象编程可以提高代码的可复用性
3. 可以提高软件的可维护性, 遵守开闭原则的软件, 其稳定性高和延续性强, 从而易于扩展和维护


可以通过“抽象约束、封装变化”来实现开闭原则, 即通过接口或者抽象类为软件实体定义一个相对稳定的抽象层, 而将相同的可变因素封装在相同的具体实现类中。

因为抽象灵活性好, 适应性广, 只要抽象的合理, 可以基本保持软件架构的稳定。而软件中易变的细节可以从抽象派生来的实现类来进行扩展, 当软件需要发生变化时, 只需要根据需求重新派生一个实现类来扩展就可以了。

<hr/>

## 创建型模式


### 单例模式 (Singleton)

### 原型模式 (Prototype)

### 工厂方法模式 (Factory Method)

### 抽象工厂模式 (Abstract Factory)

### 建造者模式 (Builder)


## 结构型模式


### 代理模式 (Proxy)

### 适配器模式 (Adapter)

### 桥接模式 (Bridge)

### 装饰器模式 (Decorator)

### 外观模式 (Facade)

### 享元模式 (Flyweight)

### 组合模式 (Composite)


## 行为型模式


### 模板方法模式 (TemplateMethod)

### 策略模式 (Strategy)

### 命令模式 (Command)

### 责任链模式 (Chain of Responsibility)

### 状态模式 (State)

### 观察者模式 (Observer)

### 中介者模式 (Mediator)

### 迭代器模式 (Iterator)

### 访问者模式 (Visitor)

### 备忘录模式 (Memento)

### 解释器模式 (Interpreter)
