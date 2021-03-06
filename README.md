thrift-generator
================

Creating a thrift file via a Java interface

## example
```java
public interface ICommonUserService {

	public User login(int id, String name);
	
	public User getUserById(long id);
	
	public boolean saveUser(User user);
	
	public List<User> getUserIds(long id); 
	
	public Map<Long, User> getUserByIds(List<User> ids);
	
	public Map<String, List<User>> getUsersByName(List<String> names);

	public Map<Long, List<Long>> getGroupUsers(List<String> names, List<User> userList, List<Long> lns, long ll);
	
	public List<String> testCase1(Map<Integer,String> num1, List<User> num2, List<String> num3, long num4, String num5);
}
```
```java

public class ThriftStructBuilderTest {

	private ThriftFileBuilder fileBuilder = new ThriftFileBuilder();
	
	@Test
	public void toOutputstream() throws Exception {
		this.fileBuilder.buildToOutputStream(ICommonUserService.class, System.out);
	}
	
}
```
### 执行之后会在控制台输入如下:
```thrift

	namespace java com.sohu.thrift.generator.test.thrift

	enum Status {
			NORMAL = 0,
			BLOCKED = 1
	}

	struct Account {
			1:i32 id,
			2:string name
	}
	struct User {
			1:i32 id,
			2:string name,
			3:bool sex,
			4:Status status,
			5:list<i64> ids,
			6:Account account
	}

	service ICommonUserService {
		 	User login(1:i32 arg0,2:string arg1),
		 	map<string, list<User>> getUsersByName(1:list<string> arg0),
		 	bool saveUser(1:User arg0),
		 	map<i64, User> getUserByIds(1:list<User> arg0),
		 	list<User> getUserIds(1:i64 arg0),
		 	map<i64, list<i64>> getGroupUsers(1:list<string> arg0,2:list<User> arg1,3:list<i64> arg2,4:i64 arg3),
		 	User getUserById(1:i64 arg0),
		 	list<string> testCase1(1:map<i32, string> arg0,2:list<User> arg1,3:list<string> arg2,4:i64 arg3,5:string arg4)
	}

```
