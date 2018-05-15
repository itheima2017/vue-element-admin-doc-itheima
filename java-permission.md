# 权限控制

在黑马Admin中，我们详细的设计了权限模块，目前权限分为3大类：

- 菜单权限

  主要用于约束页面菜单，路由等，其约束实现主要作用于前端，后端对此仅做信息的记录和查询操作。

- 点权限

  主要用于页面元素，如按钮，控件等等，其作用域同菜单权限

- api权限

  主要用于约束用户访问api，当用户访问未授权api，后端会返回未授权信息。


这里，我们主要介绍一下api权限。作为后端防御措施的一种，api权限可以有效的避免非授权用户对一些敏感接口进行访问和操作，从而达到接口保护的作用。接下来，将分步骤的分解api权限是如何设计以及实现。

##### 第一步 定义api权限

我们在编写接口时，都需要通过RequestMapping注解来完成接口访问地址等信息的编写。由于在项目启动时，我们会通过一个自定义启动类，利用Spring mvc提供的RequestMappingHandlerMapping获取项目中所有的 定义的api，并记录api的相关信息（URL,请求方法，接口名称）。因此，在编写api的RequestMapping时，需要为api定义一个易读的接口名称，这个名称将在为用户分配权限时使用。同时，按照约定，在定义接口名称时，所定义接口为敏感接口时，在名称前面增加check字样，用来标识这个接口在访问时，需要进行校验。

```java
//RequestMapping 编写示例
@RequestMapping(
    name = "check分页获取用户列表", 						//接口名称
    value = "/base/users", 								 //接口url
    method = RequestMethod.GET, 						 //请求方法
    produces = "application/json;charset=utf-8"
)

//初始化
List<PermissionUrlInfo> urlInfoList = PermissionUtil.getAllUrl(webApplicationContext);
        List<Permission> saveList = new ArrayList<>();
        for (PermissionUrlInfo info : urlInfoList) {
            Permission permission = new Permission();
            permission.setName(info.getName());
            permission.setType(PermissionConstants.PERMISSION_TYPE_API);
            PermissionApiExtend apiExtend = new PermissionApiExtend();
            apiExtend.setApiMethod(info.getMethod());
            apiExtend.setApiUrl(info.getUrl());
            permission.setPermissionApiExtend(apiExtend);
            if (permission.getName().startsWith("check")) {
                permission.setName(permission.getName().replace("check", ""));
                apiExtend.setApiLevel(PermissionConstants.API_LEVEL_CHECK);
            } else {
                apiExtend.setApiLevel(PermissionConstants.API_LEVEL_UNCHECK);
            }
            saveList.add(permission);
        }
        permissionsService.saveApiPermissions(saveList);
```

初始化操作，将所有的api接口写入到权限表中，以便在用户授权时使用。api权限的新增和信息更新无需手动添加，在项目启动时，会自动加载所有的变更。

##### 第二步 校验

在用户登录时，通过实现Spring Security提供的UserDetailsService，将已授予用户的权限放入上下文中。当用户访问接口时，Spring Security的验证模块会根据接口上定义的权限校验信息，对上下文中的用户信息的权限进行检查，只有通过时，才可进入接口具体的业务处理。

```java
//加载权限到上下文
@Service
public class UserDetailsServiceImpl implements UserDetailsService {
    @Autowired
    private IUserService userService;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        User user = userService.findByEmail(username);
        List<GrantedAuthority> authorities = new ArrayList<>();
        if (user != null && user.getStatus() != EUserStatus.DISABLE.getCode()) {
            PermissionGroup permissionGroup = user.getPermissionGroup();
            if (permissionGroup != null) {
                Set<Permission> permissionSet = permissionGroup.getPermissions();
                if (permissionSet != null) {
                    for (Permission permission : permissionSet) {
                        if (PermissionConstants.PERMISSION_TYPE_API == permission.getType()) {
                            //此为API权限
                            PermissionApiExtend permissionApiExtend = permission.getPermissionApiExtend();
                            GrantedAuthority grantedAuthority = new GrantedAuthorityImpl(permissionApiExtend.getApiMethod() + "|" + permissionApiExtend.getApiUrl());
                            authorities.add(grantedAuthority);
                        }
                    }
                }
            }
            return new org.springframework.security.core.userdetails.User(user.getEmail(), user.getPassword(), authorities);
        }
        return null;
    }
}

//声明权限检查
@PreAuthorize("hasAuthority('GET|/base/users')")
@RequestMapping(name = "check分页获取用户列表", value = "/base/users", method = RequestMethod.GET, produces = "application/json;charset=utf-8")
public Mono<Map<String, Object>> findAllByPage() throws Exception {}
```

通过PreAuthorize注解，在进入方法前，进行权限校验，当该用户的上下文信息当中存在当前访问接口的权限，则进入方法继续执行。反之，直接返回未授权信息。

在上述权限内容的基础上，未来我们会对权限控制进行进一步的细化，做到用户与权限的细粒度控制。