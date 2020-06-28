####  什么是MVVM？[MVVM](https://en.wikipedia.org/wiki/Model–view–viewmodel)是Model-View-ViewModel的缩写。 

 用JavaScript在浏览器中操作HTML，经历了若干发展阶段： 

-  第一阶段，直接用JavaScript操作DOM节点，使用浏览器提供的原生API

-  第二阶段，由于原生API不好用，还要考虑浏览器兼容性，jQuery横空出世，以简洁的API迅速俘获了前端开发者的芳心 

-  第三阶段，MVC模式，需要服务器端配合，JavaScript可以在前端修改服务器渲染后的数据 

-  MVVM最早由微软提出来，它借鉴了桌面应用程序的MVC思想，在前端页面中，把Model用纯JavaScript对象表示，View负责显示，两者做到了最大限度的分离。  把Model和View关联起来的就是ViewModel。ViewModel负责把Model的数据同步到View显示出来，还负责把View的修改同步回Model。 

  ####  MVVM的设计思想：关注Model的变化，让MVVM框架去自动更新DOM的状态，从而把开发者从操作DOM的繁琐步骤中解脱出来！ 