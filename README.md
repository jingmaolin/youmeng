友盟集成使用需知：

①友盟AppKey与各大平台的AppKey等的申请相对麻烦，有的还需要app官方下载的网址

②根据集成后的感觉而言，过程还是主要参考集成官方文档即可。自动集成需注意，
官方给出的依赖中并没有指定版本，而是读取最新版本的包（如此，友盟方可能在最新的库中
少传某些文件，进而导致上线的app崩溃），故最好指定使用的依赖版本

③多余依赖包的注释。一些debug包和运行时的log一般状态都删除或者关闭日志，减小包体积

④QQ与QQ空间回调问题的解决：
	在调用分享的模块中，提供调用onActivityResult接口。
	实际问题发现：
		主模块 application  子模块 module
		之前调用友盟qq的代码在子module中，展示页面在主application中，起初将回调onActivityResult写在主application，结果成功时
		回调的cancel方法。后在子module中提供调用onActivityResult的接口，主application在onActivityResult中调用子module的方法(传入上下文)，该问题解决。
		感觉问题出现的原因在于，主applition 与子module依赖的库问题导致调用的方法不是同一库中的。