# ˵��
����Ŀ��ʾ���ڱ������л���Spring Boot/Spring Cloud�ܹ�������΢����Ӧ�ã���������ע�ᡢ�����֡��������ء���·���١���·���Ȼ������ܡ�Spring Bootʹ��Red Hat Runtimes Spring Boot 2.1.6��Spring Cloudʹ��Greenwich.SR5����ƽ���ڱ��ػ�Red Hat OpenShift�Ͻ��в���δ����Ҳ��ʹ��OpenShift Service Mesh�Ա���Ŀʹ�õ�Spring Cloud������Ӧ�������

# Ӧ��˵��

��Ӧ����һ��ģ���ѯ���౨�۵�Ӧ�ã�������ģ�����

````
Airports                          �ṩ������ѯ����
Eureka                            ΢����ע��
Flights                           �����ѯ����
Presentation                      Ӧ��ǰ��
Sales                             ����۸��ѯ����
Zuul                              ΢��������
Zipkin                            ΢�������׷��
````

Ӧ������΢����Ӧ�õ�ͨ��ģʽ��ƣ�ǰ��ͨ��΢��������Zuul�Ժ��΢����Airports��Flights��Sales���е��ã���������Ϣ���ָ�ʹ���ߡ�����΢�����ע�ᵽEureka�����΢����֮��ĵ��ã���ͨ��Zuul���ã�Ҳ������ֱ���໥����á�������õ���·׷����Ϣ���͵�Zipkin����ͨ����ѯ������й۲졣

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
mvn package -Popenshift
````
��������Ŀ¼���ɿ����е�.jar�ļ�

````
Airports\target\airports-1.0-SNAPSHOT.jar
Eureka\target\eureka-1.0.0-RELEASE.jar
Flights\target\flights-1.0-SNAPSHOT.jar
Presentation\target\presentation-1.0-SNAPSHOT.jar
Sales\target\sales-1.0-SNAPSHOT.jar
Zuul\target\zuul-1.0.0-RELEASE.jar

````

��Spring Boot 2.0.0��ʼ��Zipkin������ΪSpring Boot�ɱ�����Ŀ���ڣ��ٷ��Ƽ��� [����](https://zipkin.io) ֱ�����ؿ����е�.jar�ļ�ֱ�����У���ZipkinĿ¼�У��Ѿ�׼����zipkin.jar�ļ���

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

ͨ�� [http://localhost:6080](http://localhost:6080) ����Ӧ��ǰ�ˣ�����ʼ��ַ��Ŀ�ĵ�ַ���Էֱ�����SEA��KFW��Ƭ�̺󽫻�չ�ֺ���ʱ��ͱ��ۣ�Ҳ�ɳ�������������ʼ��ַ��Ŀ�ĵ�ַ������LAS��SAN�ȡ�

���� [http://localhost:8761](http://localhost:8761) �鿴��ǰ�Ѿ�ע�ᵽEureka��΢�����б�

���� [http://localhost:9411](http://localhost:9411) �鿴΢������·���ٺ͸��Ե���������ϵ��