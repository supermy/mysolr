���⣬��solr Post�����ʱ����ҪתΪutf-8���롣��solr ���صĲ�ѯ���Ҳ��Ҫ����һ��utf-8��ת�롣��������ʱ�Բ�ѯ�Ĺؼ���Ҳ��Ҫת�룬Ȼ���á�+�����ӡ�

String[] array = StringUtils.split(query, null, 0);

        for (String str : array) {

            result = result + URLEncoder.encode(str, "UTF-8") + "+";

        }



��װ
copy mmseg4j-all-1.8.1.jar D:\env_java\apache-tomcat-6.0.14\webapps\solr\WEB-INF\lib
�ύ��������
D:\env_java\source\mysolr\client\exampledocs\post-chinese.bat
java -Durl="http://localhost:8080/solr/update" -jar post.jar  *.xml 

solr.home�����������ַ�ʽ�� 
   
   1�����ڵ�ǰ·���ķ�ʽ 
      ���������Ҫ��c:\solr-tomcat\Ŀ¼��ȥ����tomcat��Solr����./solr�����������ʱ����Ҫ�л���c:\solr-tomcat\ 
   2�����ڻ������� 
      windows�ڻ��������н���solr.home,ֵΪc:\solr-tomcat
      linux�ڵ�ǰ�û��Ļ��������У�.bash_profile������catalina.sh��������»������� 
export JAVA_OPTS="$JAVA_OPTS -Dsolr.solr.home=/opt/solr-tomcat/solr" 
    3������JNDI 
       ��tomcat��conf�ļ��н���Catalina�ļ��У�Ȼ����Catalina�ļ������ڽ���localhost�ļ��У��ڸ��ļ������潨��solr.xml���������ݣ� 
Xml���� 

<Context docBase="D:/env_java/source/solr-tomcat/solr.war" debug="0" crossContext="true" >   
      <Environment name="solr/home" type="java.lang.String" value="D:/env_java/source/solr-tomcat/solr" override="true" />   
</Context>


�������������˷��ֵ�һ�����⣬����������ú�JNDI�Ļ���Ȼ����tomcat��bin�ļ�����������tomcat�Ļ�������tomcat��bin���潨��solr�ļ��У�����ļ�������Ҫ��ŵ������ļ��� ������Щ����Ӧ�÷���D:/env_java/source/solr-tomcat/solr������㲻�������������Ļ�����ʹ�û��ڵ�ǰ·���ķ�ʽ��


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
    
dicPath ָ���ʿ�λ�ã�ÿ��MMSegTokenizerFactory����ָ����ͬ��Ŀ¼���������Ŀ¼ʱ������� solr.home ��Ŀ¼����mode ָ���ִ�ģʽ��simple|complex|max-word��Ĭ����max-word����


������һ�������ֶΣ������е�ȫ���ֶθ��Ƶ�һ���ֶ��У��Ա����ͳһ�ļ���
���弸���ֶΣ�
<field name="simple" type="textSimple" indexed="true" stored="true"/>  
<field name="complex" type="textComplex" indexed="true" stored="true"/>  
<field name="text" type="textMaxWord" indexed="true" stored="true"/>  

����Ӹ� copyField�������Ӱɣ���
<copyField source="text" dest="simple" />  
<copyField source="text" dest="complex" />  