## @RequiredArgsConstructor(onConstructor_ = @Autowired)

替代构造器的构造方法部分，@RequiredArgsConstructor本身就是生成带参或者不带参的构造方法

对比：

```java
//@Autowired
@Service
public class BaseInfoCompanyFareServiceImpl implements BaseInfoCompanyFareService {

    @Autowired
    private BaseInfoCompanyFareDao baseInfoCompanyFareDao;
    @Autowired
    private BaseInfoCompanyDao baseInfoCompanyDao;
}
//构造器注入
@Service
public class BaseInfoCompanyPayServiceImpl implements BaseInfoCompanyPayService {

    private final BaseInfoCompanyPayDao baseInfoCompanyPayDao;

    public BaseInfoCompanyPayServiceImpl(BaseInfoCompanyPayDao baseInfoCompanyPayDao) {
        this.baseInfoCompanyPayDao = baseInfoCompanyPayDao;
    }
}
//@RequiredArgsConstructor
@Service
@RequiredArgsConstructor
public class BaseInfoCompanyServiceImpl implements BaseInfoCompanyService {

    final BaseInfoCompanyDao baseInfoCompanyDao;
    final BaseInfoCompanyServiceDao baseInfoCompanyServiceDao;
}
```

