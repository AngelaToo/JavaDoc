##### 整合Redis

maven 构建

1. 向pom.xml 添加相关依赖
2. properties或yml 添加配置文件
3. 在spring的xml中，配置redis的连接池，定义redisTemplate，方便service的调用。 |springboot   @PropertySource
4. 操作redis对象，@autowired   redisTemplate

