## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/tangzhangss/commonutils.github.io/edit/main/README.md) to maintain and preview the content for your website in Markdown files.

### 日志
```markdown
      /**
 * 系统日志注解
 */
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface SysLog {
    String value() default "";
}

@Pointcut("@annotation(com.tangzhangss.commonutils.aspect.syslog.SysLog)")
    public void logPointCut() {}

    @Around("logPointCut()")
    public Object around(ProceedingJoinPoint point) throws Throwable {
        long beginTime = System.currentTimeMillis();
        //执行方法
        Object result = point.proceed();
        //执行时长(毫秒)
        long time = System.currentTimeMillis() - beginTime;
        //保存日志
        saveSysLog(point, time, JSONUtil.toJsonPrettyStr(result));
        return result;
    }
```


### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
