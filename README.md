# hm-dianping
## 手机号+验证码注册登录
### 工具类
校验手机号
```java
RegexUtils.isPhoneInvalid(phone)
```
生成定长随机数列
```java
String code = RandomUtil.randomNumbers(6);
```
返回类型约定
```java
public class Result {
    private Boolean success;
    private String errorMsg;
    private Object data;
    private Long total;

    public static Result ok(){
        return new Result(true, null, null, null);
    }
    public static Result ok(Object data){
        return new Result(true, null, data, null);
    }
    public static Result ok(List<?> data, Long total){
        return new Result(true, null, data, total);
    }
    public static Result fail(String errorMsg){
        return new Result(false, errorMsg, null, null);
    }
}
```
正则类
```java
public class RegexUtils {
    /**
     * 是否是无效手机格式
     * @param phone 要校验的手机号
     * @return true:符合，false：不符合
     */
    public static boolean isPhoneInvalid(String phone){
        return mismatch(phone, RegexPatterns.PHONE_REGEX);
    }
    /**
     * 是否是无效邮箱格式
     * @param email 要校验的邮箱
     * @return true:符合，false：不符合
     */
    public static boolean isEmailInvalid(String email){
        return mismatch(email, RegexPatterns.EMAIL_REGEX);
    }

    /**
     * 是否是无效验证码格式
     * @param code 要校验的验证码
     * @return true:符合，false：不符合
     */
    public static boolean isCodeInvalid(String code){
        return mismatch(code, RegexPatterns.VERIFY_CODE_REGEX);
    }

    // 校验是否不符合正则格式
    private static boolean mismatch(String str, String regex){
        if (StrUtil.isBlank(str)) {
            return true;
        }
        return !str.matches(regex);
    }
}
```
