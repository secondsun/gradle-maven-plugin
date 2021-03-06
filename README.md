# gradle-maven-plugin

[![Build Status](https://secure.travis-ci.org/if6was9/gradle-maven-plugin.png?branch=master)](http://travis-ci.org/if6was9/gradle-maven-plugin)


This is a maven plugin that makes it easy to invoke gradle from maven.  

It is similar to the maven-antrun-plugin that allows ant to be invoked from maven. 

# Usage

Add the following plugin repository declaration to your maven pom:

```
<pluginRepositories>
	<pluginRepository>
		<snapshots>
			<enabled>false</enabled>
		</snapshots>
		<id>gradle-maven-plugin-release</id>
		<name>gradle-maven-plugin-release</name>
		<url>http://dl.bintray.com/content/robschoening/gradle-maven-plugin</url>
	</pluginRepository>
</pluginRepositories>
```

Now declare the plugin and bind it to the lifecycle phase:

```
<plugin>
      <groupId>org.fortasoft</groupId>
      <artifactId>gradle-maven-plugin</artifactId>
      <version>1.0.1</version>
        <configuration>
        	<tasks>
			<!-- this would effectively call "gradle doSomething" -->
			<task>doSomething</task>
		</tasks>
       </configuration>
        <executions>
          <execution>
	<!-- You can bind this to any phase you like -->
            <phase>compile</phase>
            <goals>
		<!-- goal must be "invoke" -->
               <goal>invoke</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
```

Now when you run maven, gradle will be invoked and execute the "doSomething" task!  Obviously you can change the task(s)
to suit your needs.
In this example, this will happen during the maven "compile" phase, but this can be easily changed.

## Options
These options can be given in the &lt;configuration&gt; element:

<table>
<tr><th>option</th><th>required</th><th>description</th><th>example</th></tr>

<tr><td>task</td><td>yes (or tasks) </td><td>gradle task to be invoked</td><td><pre>&lt;task&gt;myTask&lt;/task&gt;</pre> </td></tr>
<tr><td>tasks</td><td>yes (or task) </td><td>gradle tasks to be invoked</td><td><pre>&lt;tasks&gt;<br> &lt;task&gt;task1&lt;/task&gt;<br/> &lt;task&gt;task2&lt;/task&gt; <br/>&lt;/tasks&gt;</pre></td></tr>
<tr><td>gradleProjectDirectory</td><td>no</td><td>path to the location of your build.gradle</td><td><pre>&lt;gradleProjectDirectory&gt;<br /> ${project.basedir}/another/path<br/> &lt;/gradleProjectDirectory&gt;</pre></td></tr>
<tr><td>javaHome</td><td>no</td><td>give and explicit path to a JAVA_HOME</td><td><pre>&lt;javaHome&gt; /my/path/to/jdk &lt;/javaHome&gt;</td></pre></tr>
<tr><td>args</td><td>no</td><td>pass argument to gradle</td><td><pre>&lt;args&gt;<br> &lt;arg&gt;-q&lt;/arg&gt; <br/>&lt;/args&gt;</td></pre></tr>
<tr><td>jvmArgs</td><td>no</td><td>pass JVM arg to gradle</td><td><pre>&lt;jvmArgs&gt;<br/> &lt;jvmArg&gt;-XX:MaxPermSize=128m&lt;/jvmArg&gt;<br/> 
&lt;jvmArg&gt;-Xmx256m&lt;/jvmArg&gt; <br/>&lt;/jvmArgs&gt;</pre></td></tr>
</table>

# Plugin Testing

Here is some information on maven plugin testing.  This project is currently using the maven-invoker-plugin for testing.

* http://maven.apache.org/plugin-developers/plugin-testing.html
* http://maven.apache.org/plugins/maven-invoker-plugin/usage.html
