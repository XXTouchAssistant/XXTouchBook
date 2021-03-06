### 脚本守护模式是什么？


- 脚本守护模式会保证脚本在被外力因素 (如服务程序崩溃、设备断电) 终止后，设备再次恢复正常状态的时候能够再次启动脚本。例外情形如下：
  - 设备断电后再无充电
  - 设备开不了机
  - 设备重启后丢失越狱状态
  - 设备处于安全模式
  - 设备有锁屏密码并重启
  - 用户终止
  - 脚本因运行期错误终止
- 守护模式会先于开机启动脚本启动，所以在设备发生故障重启后可以在脚本头部加上如下代码以确保当次脚本启动的时候，屏幕已经处于解锁状态
```lua
while (device.is_screen_locked()) do
	device.unlock_screen()
	sys.msleep(1000)
end
sys.toast("屏幕已解锁，脚本开始")
-- 这下面就可以开始脚本
-- ...
```

