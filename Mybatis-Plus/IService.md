
自定义 Service 接口继承 IService 接口
```java
public interface IUserService extends IService<User> {
}
```

自定义 Service 实现类，实现自定义接口并继承 ServiceImpl 类
```java
@Service
public class UserServiceImpl 
	extends ServiceImpl<UserMapper, User>
	implements IUserService {
}
```