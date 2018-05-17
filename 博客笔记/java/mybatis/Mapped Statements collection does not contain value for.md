## 错误截图
![](http://ove4nglsb.bkt.clouddn.com/Mapped%20Statements%20collection%20does%20not%20contain%20value%20for%20addNewEmp.png)

## 错误原因
出现这个错误是因为 mapper 文件需要在核心配置文件中进行注册，如果没有注册就会出现这个错误。
如何进行注册只需要在 mappers 节点下加入 mapper 节点，指向我们的 sql xml 文件。
```xml
<mappers>
    <mapper resource="mappers/DeptMapper"></mapper>
    <mapper resource="mappers/EmpMapper"></mapper>
</mappers>
```
