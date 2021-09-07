## @component

作用是实现bean的注入

web开发，提供3个@Component注解衍生注解（功能一样）取代
@Repository(“名称”)
dao层（存储层Bean）

@Service(“名称”)
service层（业务层Bean）

@Controller(“名称”)
web层（展示层Bean）

@Autowired：
自动根据类型注入（对类成员变量、方法及构造函数进行标注，完成自动装配的工作）

@Qualifier(“名称”)
指定自动注入的id名称（在Controller中需要注入service，如果这个service有两个实现类，用来区分使用哪一个实现类。）

@Resource(“名称”)
@Resource和@Autowired注解都是用来实现依赖注入的。只是@AutoWried按by type自动注入，而@Resource默认按byName自动注入。



> 从Java EE5规范开始，Servlet中增加了两个影响Servlet生命周期的注解，@PostConstruct和@PreDestroy，这两个注解被用来修饰一个非静态的void（）方法。

## @PostConstruct 
自定义初始化

用法：

```java
@PostConstruct
public void someMethod(){}
```

被@PostConstruct修饰的方法会在服务器加载Servlet的时候运行，并且只会被服务器调用一次，类似于Servlet的inti()方法。被@PostConstruct修饰的方法会在构造函数之后，init()方法之前运行。

# @PreDestroy 
自定义销毁

被@PreDestroy修饰的方法会在服务器卸载Servlet的时候运行，并且只会被服务器调用一次，类似于Servlet的destroy()方法。被@PreDestroy修饰的方法会在destroy()方法之后运行，在Servlet被彻底卸载之前。



## @ConfigurationProperties

每个要捕获的外部属性提供一个带有字段的类(Spring Boot提供注解@ConfigurationProperties实现从配置文件自动注入对应的配置值到对应的Bean对象。)

- 前缀定义了哪些外部属性将绑定到类的字段上
- 根据 Spring Boot 宽松的绑定规则，类的属性名称必须与外部属性的名称匹配
- 我们可以简单地用一个值初始化一个字段来定义一个默认值
- 类本身可以是包私有的
- 类的字段必须有公共 setter 方法

使用举例：

ElasticsearchProperties.java

```java
@Data
@Builder
@Component
@NoArgsConstructor
@AllArgsConstructor
@ConfigurationProperties(prefix = "demo.data.elasticsearch")
public class ElasticsearchProperties {

    /**
     * 集群名称
     */
    private String clusterName = "elasticsearch";

    /**
     * 集群节点
     */
    @NotNull(message = "集群节点不允许为空")
    private List<String> clusterNodes = new ArrayList<>();

    /**
     * 连接请求超时时间
     */
    private Integer connectionRequestTimeout = 500;

    /**
     * 索引配置信息
     */
    private Index index = new Index();


    /**
     * 索引配置信息
     */
    @Data
    public static class Index {

        /**
         * 分片数量
         */
        private Integer numberOfShards = 3;

        /**
         * 副本数量
         */
        private Integer numberOfReplicas = 2;

    }

}
```

application.yml

```yaml
demo:
  data:
    elasticsearch:
      cluster-name: elasticsearch
      cluster-nodes: 20.20.0.27:9200
      index:
        number-of-replicas: 0
        number-of-shards: 3
```

