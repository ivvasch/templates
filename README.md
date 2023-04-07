# Maven Plagin Template

## Настройка проекта

Все основные настройки и зависимости уже добавлены в файл pom.xml. Для использования шаблона необходимо 
внести некоторые изменения в него:
~~~
<artifactId>template-maven-plugin</artifactId>  <!--Здесь необходимо задать имя плагина--> 
<packaging>maven-plugin</packaging>             <!--задаем сборку плагина-->
<version>0.0.1-SNAPSHOT</version>               <!--версия нашего плагина-->

<name>template-maven-plugin Maven Mojo</name>   <!--просто имя плагина, ни на что не влияет-->
~~~
Остальные параметры можно не менять. Плагин создастся и сохранится в локальный репозиторий.

## Настройка класса

Аннотация @Mojo(name="name") расположенная над классом указывает на цель плагина для Maven. Значение, которое
присваивается name и есть цель, мы используем ee для запуска нашего плагина.

Аннотация @Parameter используется для получения значений извне. В случае со статическими значениями, такими как путь к файлам, 
мы их можем задавать в нашем pom.xml:
~~~
<plugin>
<groupId>......</groupId>
<artifactId>.....</artifactId>
<version>.....</version>
<executions>
    <execution>
        <configuration>
            <sourceXmlFilePath>${project.basedir}/src/main/resources/data.xml</sourceXmlFilePath>
            <destinationJsonFilePath>${project.basedir}/src/main/resources/data.json</destinationJsonFilePath>
        </configuration>
        <goals>
            <goal>XmlToJson</goal>
        </goals>
    </execution>
</executions>
</plugin>
~~~

## Сборка инсталяция в репозиторий и запуск плагина

### Сборка и инсталяция
mvn clean install - соберет плагин в папку target и сохранит его в локальный репозиторий.

### Запуск плагина
~~~
mvn groupId:artifactId:version:goal
    groupId -       <groupId>org.unistream</groupId>
    artifactId -    <artifactId>template-maven-plugin</artifactId>
    version -       <version>0.0.1-SNAPSHOT</version>
    goal -          dependency_counter (name указанное в аннотации @Mojo)
~~~
Таким образом в нашем случае запуск плагина будет выглядеть следующим образом:
~~~
mvn org.unistream:template-maven-plugin:0.0.1-SNAPSHOT:dependency_counter
~~~