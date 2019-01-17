#### 使用startService启动Service
生命周期：onCreate() -> onStartCommand() -> 服务运行 -> onDestory()

#### 使用绑定启动Service
生命周期：onCreate() -> onBind() -> onUnbind() -> onDestory()

