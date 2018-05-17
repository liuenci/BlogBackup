## 错误截图
![](http://ove4nglsb.bkt.clouddn.com/Error%20instantiating%20class.png)

## xml 配置
```xml
<resultMap id="BaseResultMap" type="com.liuenci.pojo.Emp" >
  <constructor >
      <idArg column="empno" jdbcType="INTEGER" javaType="java.lang.Integer" />
      <arg column="ename" jdbcType="VARCHAR" javaType="java.lang.String" />
      <arg column="job" jdbcType="VARCHAR" javaType="java.lang.String" />
      <arg column="mgr" jdbcType="INTEGER" javaType="java.lang.Integer" />
      <arg column="hiredate" jdbcType="DATE" javaType="java.lang.String" />
      <arg column="sal" jdbcType="DOUBLE" javaType="java.lang.Double" />
      <arg column="comm" jdbcType="DOUBLE" javaType="java.lang.Double" />
      <arg column="deptno" jdbcType="INTEGER" javaType="java.lang.Integer" />
  </constructor>
</resultMap>
```
## java pojo
```java
package com.liuenci.pojo;

public class Emp {
    private Integer empno;
    private String ename;
    private String job;
    private Integer mgr;
    private String hiredate;
    private double sal;
    private double comm;
    private Integer deptno;

    public Emp(Integer empno, String ename, String job, Integer mgr, String hiredate, double sal, double comm, Integer deptno) {
        this.empno = empno;
        this.ename = ename;
        this.job = job;
        this.mgr = mgr;
        this.hiredate = hiredate;
        this.sal = sal;
        this.comm = comm;
        this.deptno = deptno;
    }

    public Emp() {
    }

    public Integer getEmpno() {
        return empno;
    }

    public void setEmpno(Integer empno) {
        this.empno = empno;
    }

    public String getEname() {
        return ename;
    }

    public void setEname(String ename) {
        this.ename = ename;
    }

    public String getJob() {
        return job;
    }

    public void setJob(String job) {
        this.job = job;
    }

    public Integer getMgr() {
        return mgr;
    }

    public void setMgr(Integer mgr) {
        this.mgr = mgr;
    }

    public String getHiredate() {
        return hiredate;
    }

    public void setHiredate(String hiredate) {
        this.hiredate = hiredate;
    }

    public double getSal() {
        return sal;
    }

    public void setSal(double sal) {
        this.sal = sal;
    }

    public double getComm() {
        return comm;
    }

    public void setComm(double comm) {
        this.comm = comm;
    }

    public Integer getDeptno() {
        return deptno;
    }

    public void setDeptno(Integer deptno) {
        this.deptno = deptno;
    }
}
```
这个问题找了好久才发现的，仔细看 xml 配置文件可以发现 sal 和 comm 的类型都是
```xml
javaType="java.lang.Double"
```
但是在我的 pojo 中用的是 double 类型，而不是包装类型，使用包装类型就能完美解决。
