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


