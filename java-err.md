# 错误处理

当服务器发生错误时，SpringBoot都会返回一个状态码以及一个错误页面,但是这种方式，只对浏览器端有效，而不是浏览器发送的请求不会生效。那么我们就需要自定义异常处理来解决这个问题。

首先，我们编写一个继承于Exception的CommonException异常类

```java
package itcast.research.exception;

public class CommonException extends Exception {
    public CommonException() {
    }

    public CommonException(String message) {
        super(message);
    }

    public CommonException(String message, Throwable throwable) {
        super(message, throwable);
    }

    public CommonException(Throwable throwable) {
        super(throwable);
    }
}
```

接着，我们编写一个handler类处理controller层抛出的异常：

```java
package itcast.research.exception;

import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.http.HttpStatus;
import org.springframework.security.access.AccessDeniedException;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

import javax.servlet.http.HttpServletResponse;

@RestControllerAdvice
public class ExceptionHandlers {
    private static final Logger LOGGER = LoggerFactory.getLogger(ExceptionHandlers.class);

    @ExceptionHandler(Exception.class)
    public String serverExceptionHandler(HttpServletResponse httpServletResponse, Exception ex) {
        LOGGER.error(ex.getMessage(), ex);
        ObjectMapper om = new ObjectMapper();
        httpServletResponse.setContentType("application/json;charset=utf-8");
        int errCode = HttpStatus.INTERNAL_SERVER_ERROR.value();
        if (ex.getClass() == AccessDeniedException.class) {
            errCode = HttpStatus.FORBIDDEN.value();
        }
        httpServletResponse.setStatus(errCode);
        try {
            return om.writeValueAsString(new ReturnValue(errCode, ex.getMessage()));
        } catch (JsonProcessingException e) {
            return "{\"err_code\":500,\"message\":\"信息处理错误！\"}";
        }
    }
}

```

这个类加上@RestControllerAdvice注解将会处理controller层抛出的对应的异常，这里我们处理controller抛出的CommonException自定义异常，并且将错误信息以json串的格式返回给用户。

```java
// 使用代码片段
@RequestMapping(name = "check添加用户", value = "/base/users", method = RequestMethod.POST, produces = "application/json;charset=utf-8")
    public Mono<Map<String, Object>> save(@RequestBody String strBody) throws Exception {
        User user = formatInUser(strBody);
        if (VEAStringUtil.isBlank(user.getPassword()) || VEAStringUtil.isBlank(user.getUsername()) || VEAStringUtil.isBlank(user.getEmail())) {
            throw new CommonException("用户名或密码或邮箱不能为空！");
        }
        userService.save(user);
        return Mono.just(formatOutUser(user));
    }
```

SpringBoot默认的错误处理机制以及自定义异常来处理错误请求，这更有利于我们的开发，带给用户更佳的使用效果。