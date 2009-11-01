solr.home，可以有三种方式。 
   
   1）基于当前路径的方式 
      这种情况需要在c:\solr-tomcat\目录下去启动tomcat，Solr查找./solr，因此在启动时候需要切换到c:\solr-tomcat\ 
   2）基于环境变量 
      windows在环境变量中建立solr.home,值为c:\solr-tomcat
      linux在当前用户的环境变量中（.bash_profile）或在catalina.sh中添加如下环境变量 
export JAVA_OPTS="$JAVA_OPTS -Dsolr.solr.home=/opt/solr-tomcat/solr" 
    3）基于JNDI 
       在tomcat的conf文件夹建立Catalina文件夹，然后在Catalina文件夹中在建立localhost文件夹，在该文件夹下面建立solr.xml，其中内容： 
Xml代码 

<Context docBase="D:/env_java/source/solr-tomcat/solr.war" debug="0" crossContext="true" >   
      <Environment name="solr/home" type="java.lang.String" value="D:/env_java/source/solr-tomcat/solr" override="true" />   
</Context>


问题描述：个人发现的一个问题，就是如果配置好JNDI的话，然后在tomcat的bin文件夹下面启动tomcat的话，会在tomcat的bin下面建立solr文件夹，这个文件夹中主要存放的索引文件。 本来这些东西应该放入D:/env_java/source/solr-tomcat/solr。如果你不想出现这种情况的话，请使用基于当前路径的方式。


