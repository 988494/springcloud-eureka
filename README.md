# springcloud-eureka注册中心
配置：
	windows中配置host文件中的域名解析，在C:\Windows\System32\drivers\etc\HOSTS中添加如下配置
	127.0.0.1 eureka7001.com
	127.0.0.1 eureka7002.com
	127.0.0.1 eureka7003.com



数据库脚本：
clouddb01:
DROP TABLE IF EXISTS `dept`;
CREATE TABLE `dept` (
  `deptno` bigint(20) NOT NULL AUTO_INCREMENT,
  `dname` varchar(60) DEFAULT NULL,
  `db_source` varchar(60) DEFAULT NULL,
  PRIMARY KEY (`deptno`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of dept
-- ----------------------------
INSERT INTO `dept` VALUES ('1', '开发部', 'clouddb01');
INSERT INTO `dept` VALUES ('2', '人事部', 'clouddb01');
INSERT INTO `dept` VALUES ('3', '财务部', 'clouddb01');
INSERT INTO `dept` VALUES ('4', '市场部', 'clouddb01');
INSERT INTO `dept` VALUES ('5', '运维部', 'clouddb01');


启动顺序：
	1.首先启动eureka集群：microservicecloud-eureka-7001、microservicecloud-eureka-7002、microservicecloud-eureka-7003
	2.然后启动服务提供者提供的微服务：microservicecloud-provider-dept-8001
	3.最后启动服务消费者：microservicecloud-consumer-dept-80
	其中microservicecloud为所有服模块的父工程，microservicecloud-api是公共模块
	
结果呈现：访问http://localhost/comsumer/dept/list
eureka服务注册中心：http://eureka7001.com:7001、http://eureka7002.com:7002、http://eureka7003.com:7003
