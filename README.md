# GreenDAO
GreenDAO是一个将对象映射到SQLite数据库中的轻量且快速的ORM解决方案

技术要点：
/**
 * 1.引入greenDAO,project的gradle文件和module的gradle文件一共修改四个地方
 * 2.在module的gradle文件中配置数据库版本号、生成代码的位置等参数
 * 3.创建实体类
 * 4.增删改查
 */


project的build.gradle文件添加

buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath 'org.greenrobot:greendao-gradle-plugin:3.2.1'
    }
}

app的buil.gradle文件添加

apply plugin: 'org.greenrobot.greendao'

dependencies {
    compile 'org.greenrobot:greendao:3.2.0'
}

同时添加：
greendao{
   /* 属性介绍：
    schemaVersion--> 指定数据库schema版本号，迁移等操作会用到;
    daoPackage --> dao的包名，包名默认是entity所在的包；
    targetGenDir --> 生成数据库文件的目录;*/
    //配置数据库版本号
    schemaVersion 1
    //位置
    targetGenDir 'src/main/java'
    daoPackage 'com.example.shisjin.greendao.db'
}

greendao中的注解
(一) @Entity 定义实体
@nameInDb 在数据库中的名字，如不写则为实体中类名
@indexes 索引
@createInDb 是否创建表，默认为true,false时不创建
@schema 指定架构名称为实体
@active 无论是更新生成都刷新
(二) @Id
(三) @NotNull 不为null
(四) @Unique 唯一约束
(五) @ToMany 一对多
(六) @OrderBy 排序
(七) @ToOne 一对一
(八) @Transient 不存储在数据库中
(九) @generated 由greendao产生的构造函数或方法

具体步骤
创建列表（实体类）:

@Entity
public class UserEntity {
    @Id
    private  Long id;
    @Property
    private String username;
    @Property(nameInDb = "passwd")
    private String password;

然后点击build
![image](https://github.com/shisjin/GreenDAO/blob/master/imgs/clipboard.png)
就根据greendao写的内容在对应位置生成相关类，就这么任性！
![image](https://github.com/shisjin/GreenDAO/blob/master/imgs/clipboard2.png)

