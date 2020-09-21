# JMX (Java Management Extensions)

> Reference: [okminseok.blogspot.com](http://okminseok.blogspot.com/2019/07/jmx.html), [github.com/eugenp](https://github.com/eugenp/)

<br>

<br>

### JMX 란?

- Java Application을 monitoring하고 관리하기 위한 완전한 아키텍처와 일련의 design pattern을 정의하는 technology

- 실행중인 애플리케이션의 상태를 모니터링하고, 설정을 변경할 수 있게 해주는 API 라고 생각하면 된다
  - runtime 상태의 애플리케이션을 관리할 수 있다
  - JDK 1.5부터 기본으로 탑재되어 제공되고 있다
    - Application 관리를 위한 다양한 기능을 제공할 목적으로 시작되었다

<br>

### JMX 용어

- **ManagedResource**
  - 관리의 대상이되는 resource
- **MBean** (Managed Bean)
  - JVM에서 resuource를 표현하는 **의존성 주입** 에 instance화 되는 class
  - Java application의 모니터링과 관리 기능 제공
  - ManagedResource에 대한 **접근** 및 **조작** 에 대한 `interface` 를 제공한다
- **MBean Server**
  - MBean을 관리하는 Java Class
  - MBean들은 MBean server에 등록되며, MBean server는 resource에 접근하는 모든 원격 매니저를 관리한다
  - MBeans, 동일한 JVM의 application 그리고 외부 사이에서 **중재자** 역할을 하는 element
  - MBeans와의 상호작용은 MBean Server를 통해 이루어진다 
- **Management Application**
  - JMX를 활요앟여 만들어진 application을 관리하는 application
- **Notification**
  - MBean에 의해 발생한 event, alert, information을 wrapping한 Java object
- **Instrumentation**
  - MBean에 의해 관리되는 resource들

<br>

### JMX 시작하기

- JMX를 통해 resource를 관리하려면 **MBeans** 라는 **Managed Beans** 를 생성해야 하고, 
  - 생성한 MBean을 `MBen Server`에 등록해야 한다
    - MBean Server는 등록된 MBeans를 관리하는 agent 역할을 수행하게 된다
    - MBean server는 구현한 애플리케이션 **내부** 에서 띄운다
- MBean을 구현하는데에는 rule이 있는데,
  1. **interface**와 **구현체**를 쌍으로 만들어야 하고,
  2. MBean interface의 이름은 *"MBean"* 으로 끝나야 한다
- 노출하는 변수를 monitoring만 할 것이라면 setter는 생략해도 된다

<br>

ex)

```java
import java.lang.management.ManagementFactory;

public interface MonitoringBean {
    long getStorageSize();
}

public class Monitoring implements MonitoringBean {
    @Override
    public long getStorageCount() {
        return ...;
    }
}

// boot up MBean server
Monitoring monitoring = new Monitoring();

// ManagementFactory class로 부터 MBeanServer 인스턴스를 생성
MBeanServer server = ManagementFactory.getPlatformMBeanServer();

ObjectName jmxObjectName = new ObjectName("com.chloe.example:type=basic,name=monitor");
server.registerMBean(monitoring, jmxObjectName);
```

- `ObjectName`은 **domain**,** key**의 구성을 갖는다
  - domain은 이름 충돌이 발생하지 않도록 Java package 이름을 쓰는 것이 관례이다
  -  key는 key=value 쌍을 콤마로 구분해 여러 개를 지정할 수 있다.

<br>

<br>

### Jolokia와 JMX

- 일반적으로 Java code 만이 JMX API에 직접 접근 할 수 있지만, JMX API를 표준 protocol로 변환하는 adaptor들이 있다
  - 그 중 하나가 **Jolokia** 이고, Jolokia는 JMX API를  HTTP로 변환해준다
- **Jolokia** 는 JVM에서 배포될 수 있는  **agen**t로서, 
  - REST 같은 `HTTP endpoint`를 통해` MBeans`를 노출시켜, 
  - 모든 정보가 동일한 host에서 작동하는 비 Java application에 쉽게 제공되도록 한다
    - `일반 JVM` 에서는 agent로,
    - `Java EE` 에서는 WAR or OSGI or Module agent로 배포될 수 있다