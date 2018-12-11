总结：

1、如果两个对象相同（即用equals比较返回true），那么它们的hashCode值一定要相同；
2、如果两个对象的hashCode相同，它们并不一定相同(即用equals比较返回false)  



重写equals方法必须重写hashCode方法： 参与equals函数的字段，必须都参与hashCode的计算。





8种基本类型：byte、short、int、long、double、float、char、boolean
