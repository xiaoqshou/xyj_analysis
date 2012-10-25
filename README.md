##ModuleExecutionDetector发出的signal

###1.onModuleTransition
* 所属类别：执行跟踪/os相关
* 含义：提供模块切换的信息（提供PreviousModule；currentModule指针）
* 产生此信号的函数：
	* `ModuleExecutionDetector::onExecution()`
	* `ModuleExecutionDetector::exceptionListener()`
* 产生时间点：
 	* `ModuleExecutionDetector::onTranslateBlockStart()`和`ModuleExecutionDetector::onTranslateBlockEnd()`会调用`ModuleExecutionDetector::onExecution()`发出此信号
 	* CorePlugin发出onException信号时触发`ModuleExecutionDetector::exceptionListener()`函数也会发出该信号
* 对这些plugin有帮助：
	* MemoryTracer；MemoryChecker
* 与其他signal的关系：
	* 依赖CorePlugin发出的onException信号

###2.onModuleTranslateBlockStart
* 所属类别：执行跟踪/os相关
* 含义：模块内，代码块翻译前
* 产生此信号的函数：
 	* `ModuleExecutionDetector::onTranslateBlockStart()`
* 产生时间点：
 	* 当接收到Coreplugin发出的onTranslateBlockStart信号
* 对这些plugin有帮助：
	* 执行跟踪：InstructionCounter；
	* 选择插件：StateManager；DataSelector；
	* 分析插件：CacheSim
* 与其他signal的关系：
 	* 依赖Coreplugin发出的onTranslateBlockStart信号

###3.onModuleTranslateBlockEnd
* 所属类别：执行跟踪/os相关
* 含义：模块内，翻译块结束
* 产生此信号的函数：
	* `ModuleExecutionDetector::onTranslateBlockEnd()`
* 产生时间点：
	* 当接收到Coreplugin发出的onTranslateBlockEnd信号
* 对这些plugin有帮助：
	* 路径搜索插件：MaxTbSearcher
* 与其他signal的关系：
	* 依赖Coreplugin发出的onTranslateBlockEnd信号

###4.onModuleLoad
* 所属类别：执行跟踪/os相关
* 含义：检测到模块加载发出的信号
* 产生此信号的函数：
	* `ModuleExecutionDetector::moduleLoadListener()`
* 产生时间点：
	* 当接收到Interceptor（OSMonitor）发出的onModuleLoad信号
* 对这些plugin有帮助：
	* 堆栈检测：AssertExpert；VulMining；
	* 其他插件：LibraryCallMonitor
* 与其他signal的关系：
	* 依赖于Interceptor（OSMonitor）发出的onModuleLoad信号
