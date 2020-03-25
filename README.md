

# 应用说明

本应用模拟查询航班报价，由以下模块组成

````
Airports                          机场查询服务
Eureka                            微服务注册
Flights                           航班查询服务
Presentation                      应用前端
Sales                             票价查询服务
Zuul                              微服务网关
Zipkin                            微服务调用追踪
````

遵照微服务应用的通用模式设计，前端通过微服务网关Zuul对后端微服务Airports、Flights、Sales进行调用，将航班信息呈现给用户。所有微服务均注册到Eureka，后端微服务之间的调用，则是直接调用的方式，比如Flights对Airports的调用。服务调用的链路追踪信息发送到Zipkin，可通过查询界面进行观看。

# 本地编译及运行

````
git clone https://github.com/idcf-devops-on-kubernetes/CoolAir.git
cd CoolAir
````


````
cd CoolAir-master
````

使用Maven进行编译打包

````
mvn package
````

在以下目录生成了可运行的.jar文件

````
Airports\target\airports-1.0-SNAPSHOT.jar
Eureka\target\eureka-1.0.0-RELEASE.jar
Flights\target\flights-1.0-SNAPSHOT.jar
Presentation\target\presentation-1.0-SNAPSHOT.jar
Sales\target\sales-1.0-SNAPSHOT.jar
Zuul\target\zuul-1.0.0-RELEASE.jar
````

从Spring Boot 2.0.0开始，Zipkin不再作为Spring Boot可编译项目存在，官方推荐从 [官网](https://zipkin.io) 下载打包好的.jar文件直接运行。在Zipkin目录中，已经准备好zipkin.jar文件。

需要打开七个命令行窗口运行所有的微服务：

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

各微服务监听的端口分别如下：

````
Airports                          6010
Eureka                            8761
Flights                           6020
Presentation                      6080
Sales                             6030
Zuul                              6000
Zipkin                            9411
````

# 访问应用

通过 [http://localhost:6080](http://localhost:6080) 访问应用前端，在起始地址和目的地址尝试分别输入SEA和DFW，片刻后将会展现航班时间和报价，也可尝试输入其他起始地址或目的地址，比如LAS或SAN等。

访问 [http://localhost:8761](http://localhost:8761) 查看当前已经注册到Eureka的微服务列表。

访问 [http://localhost:9411](http://localhost:9411) 查看微服务链路跟踪和调用依赖关系。

# 微服务说明

## Airports

Airports会从一个.csv文件中加载机场信息以提供查询服务，它的主执行类AirportApplication.java内容如下：

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

在model包中包含了Airport.java文件，主要为数据模型类，重要的实现类在service包中。

ApplicationInitialization.java主要实现查询数据的加载；Controller.java对外通过REST接口暴露服务，为了提供链路调用分析，在服务调用入口打上了Tag；而AirportsService.java则是主要的处理逻辑所在。

## Flights/Sales

和Airports类似，不同的是，Flights会调用Airports的查询服务。

## Presentation

是基于jQuery的一个简单应用前端，页面呈现的同时即会通过Zuul向后端发送请求进行机场信息的初始化，当在查询框中输入起始机场及旅行时间，它会异步的向后台发送查询请求，请求也是首先到Zuul，然后通过Zuul分发给相应的服务提供者。

## Zuul

Zuul的构造和Eureka类似，作为微服务网关，是前端和后端的桥梁，在实际应用中，它的功能还包括流控、鉴权等。

## 微服务之间的调用方式

在本例中，所有对微服务的调用，在调用前都通过查询Eureka获得地址信息，比如Presentation对Zuul的调用，以及后端微服务间的互相调用。通过restTemplate的实例进行具体的调用发送动作，而负载均衡依赖的是Ribbon，由于本例中每个微服务仅仅启用单实例，因此Ribbon的作用无法直接体现。Zuul对后台微服务的调用也采用了从Eureka获得地址信息，并通过Ribbon进行负载均衡的方式，这是典型的微服务应用架构。