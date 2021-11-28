1、创建maven项目
2、pom文件中的packaging配置为maven-plugin

```xml
<groupId>cloud.bigdragonz</groupId>
<artifactId>maven_plugin</artifactId>
<version>1.0-SNAPSHOT</version>
<!--    maven插件的打包方式-->
<packaging>maven-plugin</packaging>
```

3、编写自定义插件类

```java
package cloud.bigdragon.maven;

import org.apache.maven.plugin.AbstractMojo;
import org.apache.maven.plugin.MojoExecutionException;
import org.apache.maven.plugin.MojoFailureException;
import org.apache.maven.plugins.annotations.LifecyclePhase;
import org.apache.maven.plugins.annotations.Mojo;

/**
 * 自定义插件：
 * 1、继承AbstractMojo
 * 2、使用注解制定 插件名称  作用阶段
 */
@Mojo(name = "custom",defaultPhase = LifecyclePhase.PACKAGE)
public class CustomMojo extends AbstractMojo {
    
    
    @Override
    public void execute() throws MojoExecutionException, MojoFailureException {
        System.out.println("maven 自定义插件实现");
    }
}
```

4、完成后install到本地`mvn clean install`

5、在本地项目中即可使用
使用方式：

```xml
<plugin>
<!--                这里只是引用-->
                <groupId>cloud.bigdragonz</groupId>
                <artifactId>maven_plugin</artifactId>
                <version>1.0-SNAPSHOT</version>
<!--                需要在这里 挂载到maven的生命周期phase里-->
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>custom</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
```

archetype使用

创建模板`mvn archetype:create-from-project`





