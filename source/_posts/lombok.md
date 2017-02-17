---
title: lombok
date: 2016-11-30 12:57:46
tags: [tool,dev]

---

## 目标
使用[lombok][1]重构系统中的模型对象，移除`getter`，`setter` 方法。

## 问题
有些`getter`，`setter`方法系统中有重写。不能无差别处理，需要只移除默认生成的那部分。lombok的idea插件可以快捷的给类添加注解，并删除相应的代码。它是通过反射方法名删除的，不管方法实现。这里就有问题了，重要的是假如删错了代码也不会报错，检查代码也麻烦。处理办法如下。

## 实现
### 工具
* lombok jar包。增加maven依赖，因为各个模块都有用到所以引用到父级。系统已经引入，此问题不必关心。
* lombok 插件。从Idea插件库中安装，默认版本即可。
* Idea编译环境需要如下设置：
> Setting》Build，Extention，Deployment》Compile》Annotation Processors》Enable annotation processing。

### 处理已重写方法
扫描package所有class，检查所有`getter/setter` 方法，给重写了的方法加上标记。插件是通过反射查找方法的，加了标记的代码不会被清理，这部分毕竟是少数，手动处理一下。


## 过程问题

### 用@Data 产生警告
> 
Warning:(12, 1) java: Generating equals/hashCode implementation but without a call to superclass, even though this class does not extend java.lang.Object. If this is intentional, add '@EqualsAndHashCode(callSuper=false)' to your type.

**解决：** 使用`@Getter`和`@Setter`代替`@Data`可以解决。确实我们只需要`getter/setter`。推荐加`@NoArgsConstructor`。

### Boolean类型
java中boolean类型属性的getter/setter方法比较特殊。
``` java
boolean flag;
public boolean isFlag() {
    return flag;
}
public void setFlag(boolean flag) {
    this.flag = flag;
}

private boolean isValid;
public boolean isValid() {
    return isValid;
}
public void setValid(boolean valid) {
    isValid = valid;
}
```
检查工具代码需要特殊处理，又因为使用的过程中也有需要`getIsValid/setIsValid `的场景（如与Json互转），所以检查工具不处理，系统中模型清理后按需增加这类方法。

### 方法重载
使用lombok，遇到方法重载，必须保留原有方法和重载过的方法。如果移除原有方法，插件检查方法名时发现已经有了，就不会生成默认方法了。所以都要保留。

### 方法注解
系统中，部分模型的`Getter/Setter`方法上有注解(如`@JSONField`)，这类注解需要移到字段上。

## 完成
至此，重构完成。


  [1]: https://projectlombok.org/