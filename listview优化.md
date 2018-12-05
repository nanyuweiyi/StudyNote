1、复用convertView,减少不必要的View创建、减少findViewById次数；
2、采用ViewHolder缓存item引用；
3、避免在getView方法中做耗时操作；
4、图片异步加载；
5、局部刷新。
