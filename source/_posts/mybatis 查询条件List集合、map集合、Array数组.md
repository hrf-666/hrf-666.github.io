---
title: mybatis 查询条件List集合、map集合、Array数组
date: 2023-09-19 10:58:00
tags: 后端
categories: mybatis
---
# 参数为集合
## 传入map类型
```java
Mapper接口如下，service将调用该接口方法，需要注意的是，
        Map集合在foreach由于没有默认键可用，故需要使用 
@Param 注解手动指定一个标识，后面将在foreach中将其作为键使用。
        该标识任意指定即可，这里使用"stuMap"

@Mapperpublic interface StudentMapper {
    public List<Student> findAddByName2(@Param("stuMap") Map<String, String> stuMap);
}
```
```xml
传入参数为集合时，映射文件的sql标签parameterType属性可省略。
        由于是Map集合，collection无默认键，
        故配置其为对应的接口方法中的形参前的@Param注解中的标识(此处即为"stuMap")。
        由于是Map集合，index、item属性分别表示为该Map集合中的key、value，
        故可以分别用${k}，#{v}来获取该Map集合中的key、value

<select id="findAddByName2" resultMap="studentResultMap">
        SELECT * FROM user
        <where>
            <foreach collection="stuMap" index="k" item="v">
                AND  ${k} = #{v}
            </foreach>
        </where>
    </select>
```

## 传入List<Object>类型
```java
Mapper接口如下，service将调用该接口方法

@Mapper
public interface StudentMapper {
    public List<Student> findAddByName3(List<Student> stuList);
}

```

```xml
传入参数为集合时，映射文件的sql标签parameterType属性可省略。这里由于是List集合，
        故collection使用默认键list，而item属性可以任意指定，
        用来标识每次遍历的元素对象名称，这里记为node,则表示每次遍历的元素的属性时，
        可以使用点操作符,如node.address，node.sex所示

<select id="findAddByName3" resultMap="studentResultMap">
        SELECT * FROM user
<where>
<foreach collection="list" item="node">
<if test="node.address != null">
        OR address = #{node.address}
</if>
<if test="node.username != null">
        OR username = #{node.username}
</if>
<if test="node.sex != null">
        OR sex = #{node.sex}
</if>
</foreach>
</where>
</select>
```



## 传入Array类型
```java
Mapper接口如下，service将调用该接口方法

@Mapper
public interface StudentMapper {
    public List<Student> findAddByName4(Student[] stuArray);
}
```

```xml
传入参数为集合时，映射文件的sql标签parameterType属性可省略。
        这里由于是Array，故collection使用默认键array，
        而item属性可以任意指定，用来标识每次遍历的元素对象名称，这里记为node,
        则表示每次遍历的元素的属性时，可以使用点操作符,如node.address，node.sex所示。
        需要注意的是，foreach将遍历数组的所有元素，
        所以每次取该元素的属性前，需要先对该元素对象进行判空(如下所示)

    <select id="findAddByName4" resultMap="studentResultMap">
        SELECT * FROM user
        <where>
            <foreach collection="array" item="node">
                <if test="node != null">
                    <if test="node.username != null">
                        OR username = #{node.username}
                    </if>
                    <if test="node.address != null">
                        OR address = #{node.address}
                    </if>
                    <if test="node.sex != null">
                        OR sex = #{node.sex}
                    </if>
                </if>
            </foreach>
        </where>
    </select>
```

##  传入参数为包含集合属性的POJO
传入的参数为一个POJO，其属性中有集合类型时，collection直接配置为相应集合中的属性名即可

构造下列一个UserVo对象同时设置一个List集合属性，传入service
```java
    UserVo userVo = new UserVo();
    userVo.setSex("123");
    List<Student> list = new LinkedList<>();
    list.add( new Student("Aaron", "3", "NanJing") );
    list.add( new Student("tony", "0", "Beijing") );
    userVo.setStuList(list);
    studentService.findAddByName6(userVo);
```

```java
Mapper接口如下，service将调用该接口方法

    public interface StudentMapper {
        public List<Student> findAddByName6(UserVo userVo);
    }
```
```xml
传入参数为UserVo类型，故映射文件的sql标签parameterType属性配置为UserVo。
        该POJO的stuList属性为List集合类型，在遍历该属性的List集合时，collection配置为该属性名stuList即可。
        而item属性可以任意指定，用来标识每次遍历的元素对象名称，这里记为node,
        则表示每次遍历的元素的属性时，可以使用点操作符,如node.address，node.sex所示

    <select id="findAddByName6" parameterType="com.aaron.springbootdemo.pojo.UserVo" resultMap="studentResultMap">
        SELECT * FROM  user
        <where>
            <if test="sex != null">
                OR sex = #{sex}
            </if>
            <foreach collection="stuList" item="node">
                <if test="node.username != null">
                    OR username = #{node.username}
                </if>
                <if test="node.sex != null">
                    OR sex = #{node.sex}
                </if>
                <if test="node.address != null">
                    OR address = #{node.address}
                </if>
            </foreach>
        </where>
    </select>
```


## POJO 属性为 Array
构造下列一个UserVo对象同时设置一个Array属性，传入service
```java
    UserVo userVo = new UserVo();
    userVo.setSex("456");
    Student[] stuArray = new Student[4];
    stuArray[0] = new Student("Aaron", "3");
    stuArray[1] = new Student("Tom", "1");
    userVo.setStuArray(stuArray);
    studentService.findAddByName5(userVo);
```
```java
Mapper接口如下，service将调用该接口方法

    public interface StudentMapper {
        public List<Student> findAddByName5(UserVo userVo);    
    }
```

```xml
传入参数为UserVo类型，故映射文件的sql标签parameterType属性配置为UserVo。
        该POJO的stuArray属性为Array类型，在遍历该属性的Array时，
        collection配置为该属性名stuArray即可。而item属性可以任意指定，
        用来标识每次遍历的元素对象名称，这里记为node,则表示每次遍历的元素的属性时，
        可以使用点操作符,如node.address，node.sex所示。
        需要注意的是，foreach将遍历数组的所有元素，所以每次取该元素的属性前，需要先对该元素对象进行判空(如下所示)

    <select id="findAddByName5" parameterType="com.aaron.springbootdemo.pojo.UserVo" resultMap="studentResultMap">
        SELECT * FROM user
        <where>
            <if test="sex != null ">
                OR sex = #{sex}
            </if>
            <foreach collection="stuArray" item="node">
                <if test="node != null">
                    <if test="node.address != null">
                        OR address = #{node.address}
                    </if>
                    <if test="node.username != null">
                        OR username = #{node.username}
                    </if>
                    <if test="node.sex != null">
                        OR sex = #{node.sex}
                    </if>
                </if>
            </foreach>
        </where>
    </select>
```






## POJO 属性为 Map
构造下列一个UserVo对象同时设置一个Map属性，传入service
```java
    UserVo userVo = new UserVo();
    userVo.setSex("987");
    Map<String, String> map = new HashMap<>();
    map.put("address", "Shanghai");
    map.put("id", "2");
    map.put("username", "Bob");
    userVo.setStuMap(map);
    studentService.findAddByName7(userVo);
```
```java
Mapper接口如下，service将调用该接口方法

    public interface StudentMapper {
        public List<Student> findAddByName7(UserVo userVo);
    }
```
```xml
传入参数为UserVo类型，故映射文件的sql标签parameterType属性配置为UserVo。
        该POJO的stuMap属性为Map类型，在遍历该属性的Map时，collection配置为该属性名stuMap即可。
        由于是Map集合，index、item属性分别表示为该Map集合中的key、value，
        故可以分别用${k}，#{v}来获取该Map集合中的key、value

    <select id="findAddByName7" parameterType="com.aaron.springbootdemo.pojo.UserVo" resultMap="studentResultMap">
        SELECT * FROM user
        <where>
            <if test="#{sex} != null">
                OR sex = #{sex}
            </if>
            <foreach collection="stuMap" index="k" item="v">
                OR ${key} = #{value}
            </foreach>
        </where>
    </select>

```




