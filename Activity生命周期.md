Activity A启动到Activity B的生命周期变化过程：

Activity A的onPause方法执行， Activity B的onCreate、onStart、onResume依次执行， 然后Activity A的onStop执行。  所以尽量不要在onPause方法执行耗时操作。
