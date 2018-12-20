1、onAttach()          使用Activity的引用或者使用Activity作为其他操作的上下文

2、onCreate()          避免耗时操作，此时可以获取Activity传来的参数

3、onCreateView()      

4、onActivityCreated()  在Activity完成其onCreate()回调之后调用

5、onStart()

6、onResume()

7、onPause()

8、onStop()

9、onDestroyView()

10、onDestroy()

11、onDetch()      Fragme生命周期最后回调函数，调用后，Fragment不再与Activity绑定，释放资源。
