另外，向solr Post请求的时候需要转为utf-8编码。对solr 返回的查询结果也需要进行一次utf-8的转码。检索数据时对查询的关键字也需要转码，然后用“+”连接。

String[] array = StringUtils.split(query, null, 0);

        for (String str : array) {

            result = result + URLEncoder.encode(str, "UTF-8") + "+";

        }



安装
copy mmseg4j-all-1.8.1.jar D:\env_java\apache-tomcat-6.0.14\webapps\solr\WEB-INF\lib
提交索引数据
D:\env_java\source\mysolr\client\exampledocs\post-chinese.bat
java -Durl="http://localhost:8080/solr/update" -jar post.jar  *.xml 

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


	<fieldType name="textComplex" class="solr.TextField" >
      <analyzer>
        <tokenizer class="com.chenlb.mmseg4j.solr.MMSegTokenizerFactory" mode="complex" dicPath="dic"/>
      </analyzer>
    </fieldType>
	<fieldType name="textMaxWord" class="solr.TextField" >
      <analyzer>
        <tokenizer class="com.chenlb.mmseg4j.solr.MMSegTokenizerFactory" mode="max-word" dicPath="dic"/>
      </analyzer>
    </fieldType>
	<fieldType name="textSimple" class="solr.TextField" >
      <analyzer>
        <tokenizer class="com.chenlb.mmseg4j.solr.MMSegTokenizerFactory" mode="simple" dicPath="n:/OpenSource/apache-solr-1.3.0/example/solr/my_dic"/>
      </analyzer>
    </fieldType>
    
dicPath 指定词库位置（每个MMSegTokenizerFactory可以指定不同的目录，当是相对目录时，是相对 solr.home 的目录），mode 指定分词模式（simple|complex|max-word，默认是max-word）。


建立了一个拷贝字段，将所有的全文字段复制到一个字段中，以便进行统一的检索
定义几个字段：
<field name="simple" type="textSimple" indexed="true" stored="true"/>  
<field name="complex" type="textComplex" indexed="true" stored="true"/>  
<field name="text" type="textMaxWord" indexed="true" stored="true"/>  

再添加个 copyField（最后面加吧）：
<copyField source="text" dest="simple" />  
<copyField source="text" dest="complex" />  