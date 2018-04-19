首先我们需要一个 Student 类
```java
package cn.liuenci.study;

public class Student {
	private Integer userId;
	public Integer getUserId() {
		return userId;
	}

	public void setUserId(Integer userId) {
		this.userId = userId;
	}

	private String userName;

	private Integer age;

	public Student() {
	}

	public Student(String userName, Integer age) {
		super();
		this.userName = userName;
		this.age = age;
	}

	public void setUserName(String userName) {
		System.out.println(userName);
		this.userName = userName;
	}

	public String getUserName() {
		return userName;
	}

	public void setAge(Integer age) {
		System.out.println("setAge:" + age);
		this.age = age;
	}

	public Integer getAge() {
		return age;
	}

	@Override
	public String toString() {
		return "Student [userId=" + userId + ", userName=" + userName + ", age=" + age + "]";
	}
}
```
下面来构建我们的（insert）增加语句，假设我们的语句是这样的。
```sql
insert into student (userId,userName,age) values (?,?,?);
```
那么我们需要做以下几步操作：
1. 获取学生类的简单类名，不能获取全限定名。
2. 获取所有学生类的属性。
3. 拼装(?,?,?)。
4. 拼装整条语句。

代码如下：
```java
public static String insertSql(Object obj) {
		Class<?> clazz = obj.getClass();
		String tableName = clazz.getSimpleName();
		Field[] field = clazz.getDeclaredFields();
		StringBuffer sb1 = new StringBuffer();
		StringBuffer sb2 = new StringBuffer();
		for(Field f : field) {
			sb1.append(f.getName()).append(",");
			sb2.append("?").append(",");
		}
		sb1.deleteCharAt(sb1.length()-1);
		sb2.deleteCharAt(sb2.length()-1);
		return String.format("insert into %s (%s) values (%s)", tableName,sb1,sb2);
}
```
这样 insert 语句就用反射给组装好了。
然后 delete,update,select 就大同小异了。全部代码如下：
```java
import java.lang.reflect.Field;

public final class SqlBuilder {
	/**
	 * 构建插入语句 insert into student (userId,userName,age) values (?,?,?);
	 *
	 * @param obj
	 * @return
	 */
	public static String insertSql(Object obj) {
		Class<?> clazz = obj.getClass();
		String tableName = clazz.getSimpleName();
		Field[] field = clazz.getDeclaredFields();
		StringBuffer sb1 = new StringBuffer();
		StringBuffer sb2 = new StringBuffer();
		for(Field f : field) {
			sb1.append(f.getName()).append(",");
			sb2.append("?").append(",");
		}
		sb1.deleteCharAt(sb1.length()-1);
		sb2.deleteCharAt(sb2.length()-1);
		return String.format("insert into %s (%s) values (%s)", tableName,sb1,sb2);
	}

	/**
	 * 构建删除语句 delete from student where userId = ?;
	 *
	 * @param obj
	 * @return
	 */
	public static String deleteSql(Object obj) {
		// 获取类型
		Class<?> c = obj.getClass();
		// 获取表名
		String tableName = c.getSimpleName();

		// 获取属性
		Field[] field = c.getDeclaredFields();
		String f = field[0].getName();
		return String.format("delete from %s where %s = ?", tableName, f);
	}

	/**
	 * 构建修改语句 update Student set userName = ? and age = ? where userId = ?;
	 *
	 * @param obj
	 * @return
	 */
	public static String updateSql(Object obj) {
		Class<?> c = obj.getClass();
		String tableName = c.getSimpleName();
		Field[] field = c.getDeclaredFields();
		StringBuffer sb = new StringBuffer();
		for (Field f : field) {
			sb.append(f.getName()).append(" = ? and ");
		}
		sb.delete(sb.length() - 4, sb.length());
		String userId = field[0].getName();
		return String.format("update %s set %s where %s = ?", tableName, sb, userId);
	}

	/**
	 * 构建选择语句 select * from student where userId = ?
	 *
	 * @param obj
	 * @return
	 */
	public static String selectSql(Object obj) {
		Class<?> c = obj.getClass();
		String tableName = c.getSimpleName();
		Field[] field = c.getDeclaredFields();
		String userId = field[0].getName();
		StringBuffer sb = new StringBuffer();
		for(Field f : field) {
			sb.append(f.getName()).append(",");
		}
		sb.deleteCharAt(sb.length()-1);
		return String.format("select %s from %s where %s = ?",sb, tableName, userId);
	}
}
```
测试代码就不贴出来了，比较简单，这个构建 CRUD 语句只是为了练习一下 Java 的反射机制，代码有点 low ,构建的语句也比较简单，基本上都是写死的，如果你有好的写法，欢迎评论。
