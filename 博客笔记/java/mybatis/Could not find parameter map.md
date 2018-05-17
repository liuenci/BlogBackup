## 错误截图
![](http://ove4nglsb.bkt.clouddn.com/Could%20not%20find%20parameter%20map.png)

## 源码
我的 xml 配置
```xml
<update id="updateDeptInformation" parameterMap="com.liuenci.pojo.Dept">
    UPDATE
    dept
    set dname = #{dname}, loc = #{loc}
    where deptno = #{deptno}
</update>
```
原因出在 parameterMap 和 paramterType 我没有分清，这个地方我传入的是一个 pojo ,应该选择的是 parameterType,而不是 paramterMap。

网上查了一下，关于这两者的区分面试问的挺多的，那我单独开一个文章说下区别吧。
