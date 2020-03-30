## __getattr__和__getattribute__的区别
### `__getattr__`
当实例化对象调用属性不存在的时候调用
```python
class A:
    def __init__(self):
        pass

a=A()
print(a.age)
>>> AttributeError: 'A' object has no attribute 'age'
```
```python
class A:
    def __init__(self):
        pass
    def __getattr__(self, item):
        print("即使你没有属性也不会报错")

a=A()
print(a.age)
>>> 即使你没有属性也不会报错
>>> None
```
```python
from datetime import date
class User:
    def __init__(self, info={}):
        self.info = info

    def __getattr__(self, item):  # 'item' is key
        return self.info[item]

if __name__ == '__main__':
    user = User(info={"name": "bobby", "birthday": date(year=1987, month=1, day=1)})
    print(user.name)
>>> bobby
```
作用: 我们可以指定在找不到该属性的时候实现的操作, 比如修改查找的名称, 重新指定查找的区域等

### `__getattribute__`
执行查找, 无条件进入该魔法函数, 即使所查找的属性不存在
```python
from datetime import date
class User:
    def __init__(self, info={}):
        self.info = info

    def __getattr__(self, item):
        return self.info[item]

    def __getattribute__(self, item):
        return 'always run'

if __name__ == '__main__':
    user = User(info={"name": "bobby", "birthday": date(year=1987, month=1, day=1)})
    print(user.name)
>>> always run
```






















