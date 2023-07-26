# 1. Understand hierarchical Injection.
Component sẽ không tạo instances của service mà nó sẽ ủy thác cho 1 object được gọi là Injector.
Injector chịu trách nhiệm cho việc tạo object.

`
  const userDependency = new UserService();
  return new YourCompoennt(userDependency);
`
