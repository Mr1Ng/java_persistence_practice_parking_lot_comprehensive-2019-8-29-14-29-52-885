# MockMvc测试注解：
### @WebAppConfiguration
表明该类会使用web应用程序的默认根目录来载入ApplicationContext, 默认的更目录是"src/main/webapp", 如果需要更改这个更目录可以修改该注释的value值。

### @RunWith
使用 Spring-Test 框架;在使用所有注释前必须使用@RunWith(SpringJUnit4ClassRunner.class),让测试运行于Spring测试环境。

### @ContextConfiguration(location = ):
指定需要加载的spring配置文件的地址

### @Mock: 
需要被Mock的对象

### @Transactional：
不是必须的，是和@TestExecutionListeners中的TransactionalTestExecutionListener.class配合使用，用于保证插入的数据库中的测试数据，在测试完后，将插入的数据给删除掉，保证数据库的干净。如果没有显示的指定@Transactional，那么插入到数据库中的数据就是真实数据。

### @InjectMocks: 
需要将Mock对象注入的对象, 此处就是Controller

### @Before: 
在每次Test方法之前运行的方法,目前把登陆信息放到session中处理，以及初始化mockMvc。
mockMvc = MockMvcBuilders.webAppContextSetup(webApplicationContext).build();

### @Test：
执行测试

# Mybatis SQL 常用语句

### SELECT
查询语句是 MyBatis 中最常用的元素之一，光能把数据存到数据库中价值并不大，如果还能重新取出来才有用，多数应用也都是查询比修改要频繁。对每个插入、更新或删除操作，通常对应多个查询操作。这是 MyBatis 的基本原则之一，也是将焦点和努力放到查询和结果映射的原因。简单查询的 select 元素是非常简单的。比如：
```
<select
  id="selectPerson"
  parameterType="int"
  parameterMap="deprecated"
  resultType="hashmap"
  resultMap="personResultMap"
  flushCache="false"
  useCache="true"
  timeout="10000"
  fetchSize="256"
  statementType="PREPARED"
  resultSetType="FORWARD_ONLY">
  ```
  
  ### insert, update 和 delete
  插入
  ```
  <insert id="insertAuthor">
  insert into Author (id,username,password,email,bio)
  values (#{id},#{username},#{password},#{email},#{bio})
</insert>
```
更新
```
<update id="updateAuthor">
  update Author set
    username = #{username},
    password = #{password},
    email = #{email},
    bio = #{bio}
  where id = #{id}
</update>
```
删除
```
<delete id="deleteAuthor">
  delete from Author where id = #{id}
</delete>
```



## Requirement

- Please forked this repo for practice
- Read Stories and finish follow requirements
- Design your API list and put it to root folder - `API.text`, including the JSON data format, HTTP METHOD, URI as well as status code. You can try https://editor.swagger.io for API design
- Design your E-R diagram and put it to root folder `E-R.jpg`
- Complement the stories by following 3 layers architecture (controller-service-repository) 
- Write API testing via MockMVC
- Write `Repository` via mybatis testing starter (There is an example for repository, feel free to replace them with your testing)
- Write other unit testing if needed
- Your commit message MUST follow the semantic message rule

### Stores

#### Story 1

As a manager, I want to create and list all parking boys. So that I can find someone to park cars for the customer.

AC1. I should be able to create parking boy to the system. The parking boy contains the following information:
employeeID: The employee id is a non-empty String representing the unique ID for a parking boy.

AC2. I should be able to list ALL the parking boys in the system. Each parking boy should include his employeeID.

#### Story 2

As a manager, I want to create and list all parking lots so that that parking boys can park cars into them.

AC1. I should be able to create a parking lot in the system. The parking lot contains the following information:
parkingLotID: The parking lot id is a non-empty String representing the unique ID for a parking lot.
capacity: The capacity of the parking lot. It is an integer from 1 - 100.

AC2. I should be able to list ALL parking lots in the system. Each parking lot should contain its parkingLotID, availablePositionCount and capacity of each parking lot.

#### Story 3

As a manager, I would like to associate parking lots to parking boys so that the parking boy can park cars in parking lots.

AC1. I should be able to associate one or more parking lots to a parking boy. Note that each parking lot can only be associated with one parking boy.

AC2. I should be able to display the parking boy and his/her managed parking lots. The parking boy should contain his/her employeeID and the associated parking lots should include their parkingLotID.
 
##  Practice Output & Submit

- submit your git repo url to field `answer`

## Hint

- create `Entity` to present your data structure
- create `Repository` for MyBatis integration 
- create `Mapper` under resources package 
- write sql statements 
- use `Repository` for your business to access to database

## How to write semantic commit message 

```text
feat: add hat wobble
^--^  ^------------^
|     |
|     +-> Summary in present tense.
|
+-------> Type: chore, docs, feat, fix, refactor, style, or test.
```

## How to use H2

- `schema.sql` will be loaded and init database when application is starting
- navigate to web console`http://localhost:8080/h2-console`
- put `jdbc:h2:mem:tws_persistence_db` in `JDBC URL` field
