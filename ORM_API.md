# ORM API
---
[toc]
### 对象关系映射模块
- 分层结构
- 约束一致性和验证
- 对象元数据取决于它的状态
- 通过复杂查询优化运算（一次多个动作）
- 字段默认值
- 权限优化
- 持久对象：postgresql
- 数据转换
- 多层缓存系统
- 两种不同的继承结构
- 丰富的字段类型
    - 常规（varchar, integer, boolean, ...）
    - 关系（one2many, many2one, many2many）
    - 函数
---
### Models
模型字段作为模型本身的属性：
```python
from odoo import field, models
class AModel(models.Model):
    _name = 'a.model.name'

    field1 = field.Char()
```
> <font size=2>*警告*</font>
> <font size=2>这意味着你不能定义相同名称的字段和方法，最后定义的将覆盖前一个</font>

默认的，字段的标签（用户可见的名称）是该字段名称的大写版本，它能被`string`参数覆盖。
```python
field2 = field.Integer(string="Field Label")
```
字段类型和参数请看[字段参考](#Fields)。
默认值定义为字段上的参数，也可定义为值：
```python
name = fields.Char(default="a value")
```
或者可以调用函数计算默认值：
```python
def _default_name(self):
    return self.get_value()

name = fields.Char(default=lambda self: self._default_name())
```
---
### <span id="Fields">Fields</span>