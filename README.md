# ˵��
����Ŀ��ʾ���ڱ������л���Spring Boot/Spring Cloud�ܹ�������΢����Ӧ�ã���������ע�ᡢ�����֡��������ء���·���١���·���Ȼ������ܡ�Spring Bootʹ��Red Hat Runtimes Spring Boot 2.1.6��Spring Cloudʹ��Greenwich.SR5����ƽ���ڱ��ػ�Red Hat OpenShift�Ͻ��в���δ����Ҳ��ʹ��OpenShift Service Mesh�Ա���Ŀʹ�õ�Spring Cloud������Ӧ�������

# Ӧ��˵��

��Ӧ����һ��ģ���ѯ���౨�۵�Ӧ�ã�������ģ�����

````
Airports                          ������ѯ����
Eureka                            ΢����ע��
Flights                           �����ѯ����
Presentation                      Ӧ��ǰ��
Sales                             Ʊ�۲�ѯ����
Zuul                              ΢��������
Zipkin                            ΢�������׷��
````

����΢����Ӧ�õ�ͨ��ģʽ��ƣ�ǰ��ͨ��΢��������Zuul�Ժ��΢����Airports��Flights��Sales���е��ã���������Ϣ���ָ��û�������΢�����ע�ᵽEureka�����΢����֮��ĵ��ã�����ֱ�ӵ��õķ�ʽ������Flights��Airports�ĵ��á�������õ���·׷����Ϣ���͵�Zipkin����ͨ����ѯ������йۿ���

# ���ر��뼰����

````
git clone https://github.com/mransonwang/LambdaAir.git
cd LambdaAir
````

������Ŀ�ļ��ϴ�Ҳ����ͨ�� [LambdaAir on Spring Boot](https://github.com/mransonwang/LambdaAir/archive/master.zip) ֱ�����ش���ļ�(Լ70M)����ѹ��ָ��Ŀ¼��

````
cd LambdaAir-master
````

ʹ��Maven���б�����

````
mvn package
````

������Ŀ¼���ɿ����е�.jar�ļ�

````
Airports\target\airports-1.0-SNAPSHOT.jar
Eureka\target\eureka-1.0.0-RELEASE.jar
Flights\target\flights-1.0-SNAPSHOT.jar
Presentation\target\presentation-1.0-SNAPSHOT.jar
Sales\target\sales-1.0-SNAPSHOT.jar
Zuul\target\zuul-1.0.0-RELEASE.jar
````

��Spring Boot 2.0.0��ʼ��Zipkin������ΪSpring Boot�ɱ�����Ŀ���ڣ��ٷ��Ƽ��� [����](https://zipkin.io) ���ش���õ�.jar�ļ�ֱ�����С���ZipkinĿ¼�У��Ѿ�׼����zipkin.jar�ļ���

��Ҫ���߸������д����������е�΢����

````
java -jar Eureka\target\eureka-1.0.0-RELEASE.jar
````
````
jar -jar Zipkin\zipkin.jar
````
````
jar -jar Airports\target\airports-1.0-SNAPSHOT.jar
````
````
jar -jar Flights\target\flights-1.0-SNAPSHOT.jar
````
````
jar -jar Presentation\target\presentation-1.0-SNAPSHOT.jar
````
````
jar -jar Sales\target\sales-1.0-SNAPSHOT.jar
````
````
jar -jar Zuul\target\zuul-1.0.0-RELEASE.jar
````

��΢��������Ķ˿ڷֱ����£�

````
Airports                          6010
Eureka                            8761
Flights                           6020
Presentation                      6080
Sales                             6030
Zuul                              6000
Zipkin                            9411
````

# ����Ӧ��

ͨ�� [http://localhost:6080](http://localhost:6080) ����Ӧ��ǰ�ˣ�����ʼ��ַ��Ŀ�ĵ�ַ���Էֱ�����SEA��DFW��Ƭ�̺󽫻�չ�ֺ���ʱ��ͱ��ۣ�Ҳ�ɳ�������������ʼ��ַ��Ŀ�ĵ�ַ������LAS��SAN�ȡ�

���� [http://localhost:8761](http://localhost:8761) �鿴��ǰ�Ѿ�ע�ᵽEureka��΢�����б�

���� [http://localhost:9411](http://localhost:9411) �鿴΢������·���ٺ͵���������ϵ��

# ����Ŀ���뵽Eclipse

��Ŀ��������Eclipse�н��п������ԣ�ʹ��IDEҲ�������׷�����ѧϰ��Ŀ��

����Eclipse������Ŀ¼ѡ��LambdaAir��LambdaAir-master��Eclipse�����ʼ������Ŀ¼������ʼ����Ϻ󣬽����µ�������Ŀ¼��һ���룺

````
File > Import... > Maven > Existing Maven Projects 
````
Eclipse�����Զ�������������Ŀ��Ȼ���ھ���״̬��

����Ҽ��������һ����Ŀ������Eureka��ѡ����ִ���ࣺ

````
Run As > Java Application > EurekaApplication - com.example
````

ʹ�����Ϸ�ʽ��������������΢����

# ��Ŀ�ļ�Ҫ���

## Eureka

��Ҫע��ĵط���pom.xml��application.yaml����ִ����

pom.xml�����÷ǳ���Ҫ������������Ŀ��Ҫ�ĸ���������⣬����ʹ�õ���Spring Cloud Greenwich.SR5�汾�Լ�Red Hat Spring Boot 2.1.6�汾��JDK����1.8�汾��

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
		<spring-cloud.version>Greenwich.SR5</spring-cloud.version>
		
		<spring-boot.version>2.1.6.RELEASE</spring-boot.version>
    	<spring-boot-maven-plugin.version>2.1.6.RELEASE</spring-boot-maven-plugin.version>
	</properties>

�������������������

````
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-actuator</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
		</dependency>
	</dependencies>

	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>me.snowdrop</groupId>
				<artifactId>spring-boot-bom</artifactId>
				<version>2.1.6.SP3-redhat-00001</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
			<dependency>
				<groupId>org.springframework.cloud</groupId>
				<artifactId>spring-cloud-dependencies</artifactId>
				<version>${spring-cloud.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>
````
	
��pom.xml��ĩβ�������Red Hat��Maven�ֿ⣬������Ϊ��Ŀ���õ���Red Hat Spring Boot����ٷ�֧�ֵ���⣬�ʹ���Դ����ȣ���ñ�汾��Spring Boot����Ҳ��ȫ��Դ�����Ҹ��ܻ�ùٷ��ṩ�ļ���֧�֣�Ŀǰ������Red Hat Runtimes�е�һԱ��

    <repositories>
        <repository>
            <id>redhat-ga-repository</id>
            <name>Redhat GA Repository</name>
            <url>https://maven.repository.redhat.com/ga/all/</url>
        </repository>
    </repositories>
    <pluginRepositories>
        <pluginRepository>
            <id>redhat-ga-repository</id>
            <name>Redhat GA Repository</name>
            <url>https://maven.repository.redhat.com/ga/all/</url>
        </pluginRepository>
    </pluginRepositories>

������Ҫ�ص��ἰһ�£�����Spring Boot/Spring Cloud΢�����ڿ�������ʱ��Ҫ���������Maven�����ֿ⣬ǿ�ҽ����ڱ��شһ��˽�еĹ����ֿ⣬�Խ�ʡÿ�ι�����ʱ�䣬���˽���JFrog Artifactory��

application.yaml�ļ�λ��src/main/resourcesĿ¼��������Ҫ���ݣ�

````
spring:
  application:
    name: eureka

server: 
  port: 8761

eureka: 
  instance: 
    hostname: localhost    
  server:
    response-cache-update-interval-ms: 500
  client: 
    register-with-eureka: false
    fetch-registry: false
    service-url:
      default-zone: http://${eureka.instance.hostname}:${server.port}/eureka/
````

����ִ����com.example.EurekaApplication.java�У�ͨ��ע�⽫��Ӧ����������ΪEureka Server��

````
@SpringBootApplication
@EnableEurekaServer
public class EurekaApplication {

	public static void main(String[] args) {
		SpringApplication.run(EurekaApplication.class, args);
	}
}
````

������һ��Eureka΢����Ϳ�������ˡ�

## Airports

Airports���һ��.csv�ļ��м��ػ�����Ϣ���ṩ��ѯ����������ִ����AirportApplication.java�������£�

````
@SpringBootApplication
@EnableDiscoveryClient
public class AirportsApplication
{
	public static void main(String[] args)
	{
		SpringApplication.run( AirportsApplication.class, args );
	}
}
````

��model���а�����Airport.java�ļ�����ҪΪ����ģ���࣬��Ҫ��ʵ������service���С�

ApplicationInitializatioin.java��Ҫʵ�ֲ�ѯ���ݵļ��أ�Controller.java����ͨ��REST�ӿڱ�¶����Ϊ���ṩ��·���÷������ڷ��������ڽ������׳Ƶ���㣻��AirportService.java������Ҫ�Ĵ����߼����ڡ�

## Flights/Sales

��Airports���ƣ���ͬ���ǣ�Flights�����Airports�Ĳ�ѯ����

## Presentation

�ǻ���JQuery��һ����Ӧ��ǰ�ˣ����ڲ�ѯ����������ʼ����������ʱ�䣬�����첽�����̨���Ͳ�ѯ�����������ȵ�Zuul��Ȼ��ͨ��Zuul�ַ�����Ӧ�ķ����ṩ�ߡ�

## Zuul

Zuul�Ĺ����Eureka���ƣ���Ϊ΢�������أ���ǰ�˺ͺ�˵���������ʵ��Ӧ���У����Ĺ��ܻ��������ء���Ȩ�ȡ�

## ΢����֮��ĵ��÷�ʽ

�ڱ����У����ж�΢����ĵ��ã��ڵ���ǰ��ͨ����ѯEureka��õ�ַ��Ϣ������Presentation��Zuul�ĵ��ã��Լ����΢�����Ļ�����á�ͨ��restTemplate��ʵ�����о���ĵ��÷��Ͷ����������ؾ�����������Ribbon�����ڱ�����ÿ��΢����������õ�ʵ�������Ribbon�������޷�ֱ�����֡���Zuul�Ժ�̨΢����ĵ���Ҳ�����˼򵥵�ת����ʽ��Ŀ����Ϊ��������һ��΢����Ӧ���У�����֮��ĵ��÷�ʽ�����Ǻ����ġ�