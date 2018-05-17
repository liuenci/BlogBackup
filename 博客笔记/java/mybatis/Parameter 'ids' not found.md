## 错误截图
![](http://ove4nglsb.bkt.clouddn.com/Parameter%20%27ids%27%20not%20found.png)

错误的起因是因为自己需要判断传入的参数是否为空的集合，先看错误之前的源码。

Mapper 接口的代码
```java
public interface DeptMapper {
    List<DeptEmp> testForeachArray( Integer[] ids);
}
```
Mapper.xml 中的代码
```xml
<select id="testForeachArray" resultMap="deptEmp">
    select * from dept
    left join emp on dept.deptno = emp.deptno
    <if test="#{ids}.length > 0">
        where dept.deptno in
        <foreach collection="array" item="item" index="index" open="(" separator="," close=")">
            #{item}
        </foreach>
    </if>
</select>
```
出现这个错误只需要在 Mapper 接口中加入一句注解即可。
```java
List<DeptEmp> testForeachArray(@Param("ids") Integer[] ids);
```
加入之后测试成功。
