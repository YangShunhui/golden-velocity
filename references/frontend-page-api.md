# Frontend Page API Reference

Source: API Center > 页面控件 > gUtil 公共工具类对象.

This reference is used by `golden语法` when generating frontend JavaScript for page controls, service-component calls, dialogs, loading, window/page operations, and frontend utilities.

Do not mix these browser-side page-control methods with backend Velocity `$vs.*` APIs. Backend service-script methods remain documented in `vs-service-api.md`.

Total methods: 106.

## 消息与加载

### 17. info(msg:string,isCover:boolean):void

- 方法名：`info`
- 签名：`info(msg:string,isCover:boolean):void`
- 说明：向用户提示一个成功消息
- 参数：
  - `msg`：提示内容
  - `isCover`：消息是否覆盖模式，true 覆盖模式，只显示最后一条消息；false（默认）同时显示所有消息
- 返回：无
- 代码片段：`info(${1:msg})`

### 18. error(msg:string,isCover:boolean):void

- 方法名：`error`
- 签名：`error(msg:string,isCover:boolean):void`
- 说明：向用户提示一个错误消息
- 参数：
  - `msg`：提示内容
  - `isCover`：消息是否覆盖模式，true 覆盖模式，只显示最后一条消息；false（默认）同时显示所有消息
- 返回：无
- 代码片段：`error(${1:msg})`

### 19. alert(msg:string,fun:Function=null,title:string,iconType:int):void

- 方法名：`alert`
- 签名：`alert(msg:string,fun:Function=null,title:string,iconType:int):void`
- 说明：向用户提示一个对话框
- 参数：
  - `msg`：提示内容
  - `fun`：用户点击“确定”按钮后，回调函数（可缺省）
  - `title`：对话框标题，默认`提示`（可缺省）
  - `iconType`：图标类型：1 - 成功（默认） 2 - 警告 3 - 错误（可缺省）
- 返回：无
- 代码片段：`alert(${1:msg}[,${2:fun},"提示",1])`

### 20. alertWarn(msg:string,fun:Function=null,title:string):void

- 方法名：`alertWarn`
- 签名：`alertWarn(msg:string,fun:Function=null,title:string):void`
- 说明：向用户提示一个警告对话框
- 参数：
  - `msg`：提示内容
  - `fun`：用户点击“确定”按钮后，回调函数（可缺省）
  - `title`：对话框标题，默认`警告`（可缺省）
- 返回：无
- 代码片段：`alertWarn(${1:msg}[,${2:fun},"警告"])`

### 21. alertError(msg:string,fun:Function=null,title:string):void

- 方法名：`alertError`
- 签名：`alertError(msg:string,fun:Function=null,title:string):void`
- 说明：向用户提示一个错误对话框
- 参数：
  - `msg`：提示内容
  - `fun`：用户点击“确定”按钮后，回调函数（可缺省）
  - `title`：对话框标题，默认`错误`（可缺省）
- 返回：无
- 代码片段：`alertError(${1:msg}[,${2:fun},"错误"])`

### 22. confirm(msg:string,okfun:Function=null,cancelfun:Function=null,title:string,morebnts:Arrays<string>):void

- 方法名：`confirm`
- 签名：`confirm(msg:string,okfun:Function=null,cancelfun:Function=null,title:string,morebnts:Arrays<string>):void`
- 说明：产生并显示一个选择（确定、取消）对话框
- 参数：
  - `msg`：提示内容
  - `okfun`：用户点击除“取消”按钮外所有按钮被点击的回调，函数参数：`function(index){}`，index为按钮循序，从`1`开始。
  - `cancelfun`：用户点击“取消”按钮后回调（可缺省）
  - `title`：对话框标题，默认`警告`（可缺省）
  - `morebnts`：自定义按钮，字符串数组类型，如`["保存并提交","保存到草稿"]`（可缺省）
- 返回：无
- 代码片段：`confirm(${1:msg},${2:okfun}[,${3:cancelfun},"警告"])`

### 51. showLoading(msg:string):void

- 方法名：`showLoading`
- 签名：`showLoading(msg:string):void`
- 说明：显示加载动画（需要调用关闭方法关闭加载动画）
- 参数：
  - `msg`：加载窗口显示的文字，可缺省
- 返回：无
- 代码片段：`showLoading([${1:msg}])`

### 52. closeLoading():void

- 方法名：`closeLoading`
- 签名：`closeLoading():void`
- 说明：关闭加载动画
- 参数：无
- 返回：无
- 代码片段：`closeLoading()`

## 服务组件调用

### 44. request(compId:string,args:object,succfun:Function=null,errfun:Function=null,isDisShowLoadPage:Boolean=false):void

- 方法名：`request`
- 签名：`request(compId:string,args:object,succfun:Function=null,errfun:Function=null,isDisShowLoadPage:Boolean=false):void`
- 说明：请求服务组件（异步调用）
- 参数：
  - `compId`：需要调用的服务组件编码或别名
  - `args`：需要传递服务组件的参数
  - `succfun`：调用成功后服务器返回结果，参数：function(result:object){}
  - `errfun`：调用失败后服务器返回结果（可缺省），参数：function(errmsg:string){}
  - `isDisShowLoadPage`：是否不显示加载进度条，true - 静默 other 否
- 返回：无
- 代码片段：`request(${1:compId},${2:args},${3:succfun}[,${4:errfun}])`

### 45. getServerData(compId:string,args:object):object

- 方法名：`getServerData`
- 签名：`getServerData(compId:string,args:object):object`
- 说明：请求服务组件（同步调用）
- 参数：
  - `compId`：需要调用的服务组件编码或别名
  - `args`：需要传递服务组件的参数
- 返回：服务器返回的对象
- 代码片段：`getServerData(${1:compId},${2:args})`
- 用法示例：

```text
请求服务组件（同步调用）

**用        法**：
```

    var params={code:"0000"};
    var data=null;

    try {
        data=gUtil.getServerData("com.golden.jsCompId",params);
    } catch(errmsg) {// 服务器异常或者网络异常
        gUtil.error(errmsg);
        return;
    }

    console.log(data);

```
```

## 页面与窗口操作

### 33. openMainWin(pageId:string,params:object,mkId:string,title:string,callback:function):void

- 方法名：`openMainWin`
- 签名：`openMainWin(pageId:string,params:object,mkId:string,title:string,callback:function):void`
- 说明：动态打开主窗口
- 参数：
  - `pageId`：需要打开的主窗口编码或别名
  - `params`：需要传递给主窗口的参数，在onOpen方法中接收
  - `mkId`：菜单编码，默认为空，一般只有链接菜单需要传值以固定权限
  - `title`：窗口标题
  - `callback`：回调函数，在窗口初始化完成，并显示，且 onOpen 方法调用之后回调； (page,params) => {}
- 返回：无
- 代码片段：`openMainWin(${1:pageId},${2:params}[,${3:mkId}])`

### 34. openMainWin(pageId:string,params:object,mkId:string,title:string):void

- 方法名：`openMainWin`
- 签名：`openMainWin(pageId:string,params:object,mkId:string,title:string):void`
- 说明：动态打开主窗口
- 参数：
  - `pageId`：需要打开的主窗口编码或别名
  - `params`：需要传递给主窗口的参数，在onOpen方法中接收
  - `mkId`：菜单编码，默认为空，一般只有链接菜单需要传值以固定权限
  - `title`：窗口标题
- 返回：无
- 代码片段：`openMainWin(${1:pageId},${2:params}[,${3:mkId}])`

### 35. openMainWin(pageId:string,params:object,mkId:string):void

- 方法名：`openMainWin`
- 签名：`openMainWin(pageId:string,params:object,mkId:string):void`
- 说明：动态打开主窗口
- 参数：
  - `pageId`：需要打开的主窗口编码或别名
  - `params`：需要传递给主窗口的参数，在onOpen方法中接收
  - `mkId`：菜单编码，默认为空，一般只有链接菜单需要传值以固定权限
- 返回：无
- 代码片段：`openMainWin(${1:pageId},${2:params}[,${3:mkId}])`

### 36. openMainWin(pageId:string,params:object):void

- 方法名：`openMainWin`
- 签名：`openMainWin(pageId:string,params:object):void`
- 说明：动态打开主窗口
- 参数：
  - `pageId`：需要打开的主窗口编码或别名
  - `params`：需要传递给主窗口的参数，在onOpen方法中接收
- 返回：无
- 代码片段：`openMainWin(${1:pageId},${2:params})`

### 37. openSubWin(pageId:string,params:object,openType:any,isClone:boolean,title:string,callback:function,mkId:string):void

- 方法名：`openSubWin`
- 签名：`openSubWin(pageId:string,params:object,openType:any,isClone:boolean,title:string,callback:function,mkId:string):void`
- 说明：动态打开子页面
- 参数：
  - `pageId`：需要打开的子页面编码或别名（支持打开插件子页面）
  - `params`：需要传递给子页面的参数
  - `openType`：需要传递给子页面的自定义参数
  - `isClone`：是否复制单据
  - `title`：窗口标题
  - `callback`：回调函数，在窗口初始化完成，并显示，且 onOpen 方法调用之后回调； (page,params,openType) => {}
  - `mkId`：菜单编码，默认为空，一般只有链接菜单需要传值以固定权限
- 返回：无
- 代码片段：`openSubWin(${1:pageId},${2:params},${3:openType}[,false,title])`

### 38. openSubWin(pageId:string,params:object,openType:any,isClone:boolean,title:string,callback:function):void

- 方法名：`openSubWin`
- 签名：`openSubWin(pageId:string,params:object,openType:any,isClone:boolean,title:string,callback:function):void`
- 说明：动态打开子页面
- 参数：
  - `pageId`：需要打开的子页面编码或别名（支持打开插件子页面）
  - `params`：需要传递给子页面的参数
  - `openType`：需要传递给子页面的自定义参数
  - `isClone`：是否复制单据
  - `title`：窗口标题
  - `callback`：回调函数，在窗口初始化完成，并显示，且 onOpen 方法调用之后回调； (page,params,openType) => {}
- 返回：无
- 代码片段：`openSubWin(${1:pageId},${2:params},${3:openType}[,false,title])`

### 39. openSubWin(pageId:string,params:object,openType:any,isClone:boolean,title:string):void

- 方法名：`openSubWin`
- 签名：`openSubWin(pageId:string,params:object,openType:any,isClone:boolean,title:string):void`
- 说明：动态打开子页面
- 参数：
  - `pageId`：需要打开的子页面编码或别名（支持打开插件子页面）
  - `params`：需要传递给子页面的参数
  - `openType`：需要传递给子页面的自定义参数
  - `isClone`：是否复制单据
  - `title`：窗口标题
- 返回：无
- 代码片段：`openSubWin(${1:pageId},${2:params},${3:openType}[,false,title])`

### 40. openMultipleSubWin(winId:string,pageId:string,params:object,openType:any,isClone:boolean,title:string):void

- 方法名：`openMultipleSubWin`
- 签名：`openMultipleSubWin(winId:string,pageId:string,params:object,openType:any,isClone:boolean,title:string):void`
- 说明：动态打开子页面（支持子页面多开）
- 参数：
  - `winId`：窗口编码(必须)，如：单据号码
  - `pageId`：需要打开的子页面编码或别名（支持打开插件子页面）
  - `params`：需要传递给子页面的参数
  - `openType`：需要传递给子页面的自定义参数
  - `isClone`：是否复制单据
  - `title`：窗口标题
- 返回：无
- 代码片段：`openMultipleSubWin(${1:winId},${2:pageId},${3:params},${4:openType}[,false,title])`

### 41. isMultipleOpen():boolean

- 方法名：`isMultipleOpen`
- 签名：`isMultipleOpen():boolean`
- 说明：判断当前是否在多开子窗口的iframe内
- 参数：无
- 返回：true - 是 false - 否
- 代码片段：`isMultipleOpen()`

### 42. openDialog(dialogPageId:string,params:object,openType:any,isNew:boolean,callback:Function,inputFormId:string,title:string):void

- 方法名：`openDialog`
- 签名：`openDialog(dialogPageId:string,params:object,openType:any,isNew:boolean,callback:Function,inputFormId:string,title:string):void`
- 说明：动态打对话框页面
- 参数：
  - `dialogPageId`：需要打开的对话框页面编码或别名（支持打开插件对话框页面）
  - `params`：需要传递给对话框页面的参数
  - `openType`：需要传递给对话框页面的自定义参数
  - `isNew`：是否新增（true - 新增 false - 修改（修改模式下会自动加载数据））
  - `callback`：回调函数（可缺省）
  - `inputFormId`：对话框页面中inputForm控件的ID，如：inputForm，可选，若填值，则自动把params对应的数据赋值给页面元素
  - `title`：对话框标题
- 返回：无
- 代码片段：`openDialog(${1:dialogPageId},${2:params},${3:openType},${4:isNew}[,${5:callback},${6:inputFormId},${7:title}])`

### 43. openSideWin(sideWinPageId:string,params:object,openType:any,callback:Function,isBackDrop:boolean,title:string,isAppendToBody:boolean):void

- 方法名：`openSideWin`
- 签名：`openSideWin(sideWinPageId:string,params:object,openType:any,callback:Function,isBackDrop:boolean,title:string,isAppendToBody:boolean):void`
- 说明：动态打对话框页面
- 参数：
  - `sideWinPageId`：需要打开的侧边框页面编码或别名
  - `params`：需要传递给侧边框页面的参数
  - `openType`：需要传递给侧边框页面的自定义参数
  - `callback`：回调函数（可缺省）
  - `isBackDrop`：是否显示遮罩层，默认：true
  - `title`：侧边框标题（可缺省）
  - `isAppendToBody`：是否添加到`body`元素，默认：false，添加到打开他的页面
- 返回：无
- 代码片段：`openSideWin(${1:sideWinPageId},${2:params},${3:openType}[,${4:callback},${5:isBackDrop},${6:title},false])`

### 46. closeCurTabWin(isForceClose:boolean,succfun:Function):boolean

- 方法名：`closeCurTabWin`
- 签名：`closeCurTabWin(isForceClose:boolean,succfun:Function):boolean`
- 说明：关闭当前子页面
- 参数：
  - `isForceClose`：是否强制关闭（跳过onBeforeWinClose事件)
  - `succfun`：关闭窗口成功后回调（若关闭失败不回调）
- 返回：true - 找到关闭对象 false - 未找到关闭对象（如：当前没有打开的窗口）
- 代码片段：`closeCurTabWin([false,succfun])`

### 47. closeTabWin(pageId:string,isForceClose:boolean,succfun:Function):boolean

- 方法名：`closeTabWin`
- 签名：`closeTabWin(pageId:string,isForceClose:boolean,succfun:Function):boolean`
- 说明：关闭指定的子页面（或主页面）
- 参数：
  - `pageId`：页面编码（不支持页面别名，如：PG-C7BF-B6AB-52AC4ED6，若关闭当前页，您可以用 self.pageId 代替）
  - `isForceClose`：是否强制关闭（跳过onBeforeWinClose事件)
  - `succfun`：关闭窗口成功后回调（若关闭失败不回调）
- 返回：true - 找到关闭对象 false - 未找到关闭对象（如：当前没有打开的窗口）
- 代码片段：`closeTabWin(self.pageId,[false,succfun])`

### 87. openWorkflowAuditWin(billNo:string,billTypeCode:string,callback:function):void

- 方法名：`openWorkflowAuditWin`
- 签名：`openWorkflowAuditWin(billNo:string,billTypeCode:string,callback:function):void`
- 说明：打开谷神内置的审批窗口（侧边窗模式）
- 参数：
  - `billNo`：单据号
  - `billTypeCode`：标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码
  - `callback`：审核后回调
- 返回：无
- 代码片段：`openWorkflowAuditWin(${1:billNo},${2:billTypeCode})`

### 88. openWorkflowViewWin(billNo:string,billTypeCode:string):void

- 方法名：`openWorkflowViewWin`
- 签名：`openWorkflowViewWin(billNo:string,billTypeCode:string):void`
- 说明：打开谷神内置的审批窗口（侧边窗模式，仅查看，无审核）
- 参数：
  - `billNo`：单据号
  - `billTypeCode`：标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码
- 返回：无
- 代码片段：`openWorkflowViewWin(${1:billNo},${2:billTypeCode})`

### 89. openWorkflowDesignWin():void

- 方法名：`openWorkflowDesignWin`
- 签名：`openWorkflowDesignWin():void`
- 说明：打开审批流设计器（需要当前登录用户为管理员权限）
- 参数：无
- 返回：无
- 代码片段：`openWorkflowDesignWin()`

### 90. openWorkflowEntrustWin():void

- 方法名：`openWorkflowEntrustWin`
- 签名：`openWorkflowEntrustWin():void`
- 说明：打开审批委托（指派）窗口
- 参数：无
- 返回：无
- 代码片段：`openWorkflowEntrustWin()`

### 91. openWorkflowFactorWin():void

- 方法名：`openWorkflowFactorWin`
- 签名：`openWorkflowFactorWin():void`
- 说明：打开审批要素窗口
- 参数：无
- 返回：无
- 代码片段：`openWorkflowFactorWin()`

### 92. openWorkflowMatrixWin():void

- 方法名：`openWorkflowMatrixWin`
- 签名：`openWorkflowMatrixWin():void`
- 说明：打开审批矩阵窗口
- 参数：无
- 返回：无
- 代码片段：`openWorkflowMatrixWin()`

### 102. resetDialogHeight(pageId:string,height:int):void

- 方法名：`resetDialogHeight`
- 签名：`resetDialogHeight(pageId:string,height:int):void`
- 说明：重新计算对话框（及其内控件）的高度
- 参数：
  - `pageId`：页面编码（不支持页面别名，如：PG-C7BF-B6AB-52AC4ED6，若关闭当前页，您可以用 self.pageId 代替）
  - `height`：对话框内容区预期高度（若缺省，则采用对话框内控件高度）
- 返回：无
- 代码片段：`resetDialogHeight(${1:pageId},${2:height})`

### 103. resetDialogHeight(pageId:string):void

- 方法名：`resetDialogHeight`
- 签名：`resetDialogHeight(pageId:string):void`
- 说明：重新计算对话框（及其内控件）的高度
- 参数：
  - `pageId`：页面编码（不支持页面别名，如：PG-C7BF-B6AB-52AC4ED6，若关闭当前页，您可以用 self.pageId 代替）
- 返回：无
- 代码片段：`resetDialogHeight(self.pageId)`

### 106. showBillTempListDialog(page, onAfterLoad:function):void

- 方法名：`showBillTempListDialog`
- 签名：`showBillTempListDialog(page, onAfterLoad:function):void`
- 说明：调起单据草稿选择窗口
- 参数：
  - `page`：页面对象，如： self
  - `onAfterLoad`：加载后回调
- 返回：无
- 代码片段：`showBillTempListDialog(${1:page},${2:onAfterLoad})`

## 权限、用户和系统变量

### 31. getUserInfo():object

- 方法名：`getUserInfo`
- 签名：`getUserInfo():object`
- 说明：获取当前登录用户
- 参数：无
- 返回：当前登录用户对象
- 代码片段：`getUserInfo()`

### 32. getUserId():string

- 方法名：`getUserId`
- 签名：`getUserId():string`
- 说明：获取当前登录用户ID
- 参数：无
- 返回：当前登录用户ID
- 代码片段：`getUserId()`

### 79. getUserAuths(mkId,auths,callback,pageId):void

- 方法名：`getUserAuths`
- 签名：`getUserAuths(mkId,auths,callback,pageId):void`
- 说明：获取当前登录用户对指定模式是否存在指定的按钮权限（异步）
- 参数：
  - `mkId`：菜单编码
  - `auths`：按钮权限编码，`*`或者空，表示查询所有，如：`edit`，请求多个按钮权限，请使用“,”分隔，如：`edit,select,audit`，若要判断用户是否具有打开模块的权限，则传值 `select`
  - `callback`：回调函数，参数为返回的权限对象使用 `if (auth["select"] == 1) alert("有权限");`
  - `pageId`：页面编码，如：子页编码或者主页面编码，其他编码无效，若存在页面编码，则复合判断菜单是否存在权限，若不存在，则会判断页面所属的菜单是否存在权限，若存在，则视为有权限
- 返回：无
- 代码片段：`getUserAuths(${1:mkId},${2:auths},function(auth){},${3:pageId})`

### 80. getUserAuths(mkId,auths,callback):void

- 方法名：`getUserAuths`
- 签名：`getUserAuths(mkId,auths,callback):void`
- 说明：获取当前登录用户对指定模式是否存在指定的按钮权限（异步）
- 参数：
  - `mkId`：菜单编码
  - `auths`：按钮权限编码，`*`或者空，表示查询所有，如：`edit`，请求多个按钮权限，请使用“,”分隔，如：`edit,select,audit`，若要判断用户是否具有打开模块的权限，则传值 `select`
  - `callback`：回调函数，参数为返回的权限对象使用 `if (auth["select"] == 1) alert("有权限");`
- 返回：无
- 代码片段：`getUserAuths(${1:mkId},${2:auths},function(auth){})`

### 81. getUserAuthsSynch(mkId,auths,pageId):object

- 方法名：`getUserAuthsSynch`
- 签名：`getUserAuthsSynch(mkId,auths,pageId):object`
- 说明：获取当前登录用户对指定模式是否存在指定的按钮权限（同步）
- 参数：
  - `mkId`：菜单编码
  - `auths`：按钮权限编码，`*`或者空，表示查询所有，如：`edit`，请求多个按钮权限，请使用“,”分隔，如：`edit,select,audit`，若要判断用户是否具有打开模块的权限，则传值 `select`
  - `pageId`：页面编码，如：子页编码或者主页面编码，其他编码无效，若存在页面编码，则复合判断菜单是否存在权限，若不存在，则会判断页面所属的菜单是否存在权限，若存在，则视为有权限
- 返回：返回是否拥有权限对象，如：`result.select` = 1
- 代码片段：`getUserAuthsSynch(${1:mkId},${2:auths},${3:pageId})`

### 82. getUserAuthsSynch(mkId,auths):object

- 方法名：`getUserAuthsSynch`
- 签名：`getUserAuthsSynch(mkId,auths):object`
- 说明：获取当前登录用户对指定模式是否存在指定的按钮权限（同步）
- 参数：
  - `mkId`：菜单编码
  - `auths`：按钮权限编码，`*`或者空，表示查询所有，如：`edit`，请求多个按钮权限，请使用“,”分隔，如：`edit,select,audit`，若要判断用户是否具有打开模块的权限，则传值 `select`
- 返回：返回是否拥有权限对象，如：`result.select` = 1
- 代码片段：`getUserAuthsSynch(${1:mkId},${2:auths})`

## 日期、数字和精度

### 10. getTimeStamp():number

- 方法名：`getTimeStamp`
- 签名：`getTimeStamp():number`
- 说明：获得当前客户端电脑的时间戳
- 参数：无
- 返回：时间戳，如：1568948767437
- 代码片段：`getTimeStamp()`

### 11. precise(num1:number,num2:number,opt:string,scale:number=null):number

- 方法名：`precise`
- 签名：`precise(num1:number,num2:number,opt:string,scale:number=null):number`
- 说明：算术加减乘除操作
- 参数：
  - `num1`：被操作数
  - `num2`：操作数
  - `opt`：操作符，只接受：‘`+`’、‘`-`’、‘`*`’、‘`/`’
  - `scale`：小数保留精度（允许为空）
- 返回：计算后的结果
- 代码片段：`precise(${1:num1},${2:num2},${3:stropt}[,${4:scale}])`

### 14. isNumber(num:any):boolean

- 方法名：`isNumber`
- 签名：`isNumber(num:any):boolean`
- 说明：判断给定的对象是否数字
- 参数：
  - `num`：需要判断的对象
- 返回：`true` - 是 `false` -否
- 代码片段：`isNumber(${1:num})`

### 23. formatDate(date:any, type:string=null):string

- 方法名：`formatDate`
- 签名：`formatDate(date:any, type:string=null):string`
- 说明：格式化日期
- 参数：
  - `date`：需要格式化的日期，可以是`Date`类型或者`String`类型；当是`String`类型时，格式可以是：`2019-09-20 12:13:14`
  - `type`：日期格式，如：`yyyy-MM-dd HH:mm:ss`
- 返回：格式化后的日期字符串
- 代码片段：`formatDate(${1:date},"yyyy-MM-dd")`

### 25. formatNumber(num:number,fmt:string):string

- 方法名：`formatNumber`
- 签名：`formatNumber(num:number,fmt:string):string`
- 说明：金额转大写
- 参数：
  - `num`：需要格式化的数字
  - `fmt`：数字格式，如：#,##0.00
- 返回：格式化后的数字
- 代码片段：`formatNumber(${1:val},"0.00")`

### 50. showTimeLoading(msg:string,timeout:int):void

- 方法名：`showTimeLoading`
- 签名：`showTimeLoading(msg:string,timeout:int):void`
- 说明：显示超时自动关闭的加载动画
- 参数：
  - `msg`：加载窗口显示的文字，可缺省
  - `timeout`：指定时间内关闭加载窗口，单位：毫秒，默认：300ms，可缺省
- 返回：无
- 代码片段：`showTimeLoading([${1:msg},${2:timeout}])`

### 53. toNumber(str:any):float

- 方法名：`toNumber`
- 签名：`toNumber(str:any):float`
- 说明：转换为数字
- 参数：
  - `str`：要转换的字符串
- 返回：转换后的数字
- 代码片段：`toNumber(${1:str})`

### 54. toInteger(str:any):int

- 方法名：`toInteger`
- 签名：`toInteger(str:any):int`
- 说明：转换为数字
- 参数：
  - `str`：要转换的字符串
- 返回：转换后的数字
- 代码片段：`toInteger(${1:str})`

### 61. dateIntervalDAY(date1,date2):date

- 方法名：`dateIntervalDAY`
- 签名：`dateIntervalDAY(date1,date2):date`
- 说明：计算两个日期相差天数
- 参数：
  - `date1`：日期1
  - `date2`：日期2
- 返回：返回两个日期相差的天数，当date2晚于date1时返回正数，如：date1=2020-10-01 date2=2020-10-02 则本函数返回 1；
- 代码片段：`dateIntervalDAY(${1:date1},${2:date2})`

### 62. dateYearAdd(date,year):date

- 方法名：`dateYearAdd`
- 签名：`dateYearAdd(date,year):date`
- 说明：给指定日期添加年
- 参数：
  - `date`：日期
  - `year`：需要添加的年数
- 返回：返回添加后的日期
- 代码片段：`dateYearAdd(${1:date},${2:year})`

### 63. dateMonthAdd(date,month):date

- 方法名：`dateMonthAdd`
- 签名：`dateMonthAdd(date,month):date`
- 说明：给指定日期添加月
- 参数：
  - `date`：日期
  - `month`：需要添加的月数
- 返回：返回添加后的日期
- 代码片段：`dateMonthAdd(${1:date},${2:month})`

### 64. dateAdd(date,day):date

- 方法名：`dateAdd`
- 签名：`dateAdd(date,day):date`
- 说明：给指定日期添加天数
- 参数：
  - `date`：日期
  - `day`：需要添加的天数
- 返回：返回添加后的日期
- 代码片段：`dateAdd(${1:date},${2:day})`

### 65. dateHourAdd(date,hour):date

- 方法名：`dateHourAdd`
- 签名：`dateHourAdd(date,hour):date`
- 说明：给指定日期添加小时数
- 参数：
  - `date`：日期
  - `hour`：需要添加的小时数
- 返回：返回添加后的日期
- 代码片段：`dateHourAdd(${1:date},${2:hour})`

### 66. dateMinuteAdd(date,minute):date

- 方法名：`dateMinuteAdd`
- 签名：`dateMinuteAdd(date,minute):date`
- 说明：给指定日期添加分钟数
- 参数：
  - `date`：日期
  - `minute`：需要添加的分钟数
- 返回：返回添加后的日期
- 代码片段：`dateMinuteAdd(${1:date},${2:minute})`

### 67. getMonthFirstDay(date):date

- 方法名：`getMonthFirstDay`
- 签名：`getMonthFirstDay(date):date`
- 说明：获取一个日期的首月第一天
- 参数：
  - `date`：日期
- 返回：返回当前月的第一天的日期
- 代码片段：`getMonthFirstDay(${1:date})`

### 68. getMonthLastDay(date):date

- 方法名：`getMonthLastDay`
- 签名：`getMonthLastDay(date):date`
- 说明：获取一个日期的首月最后一天
- 参数：
  - `date`：日期
- 返回：返回当前月的最后一天的日期
- 代码片段：`getMonthLastDay(${1:date})`

### 75. getMonthDays(date):int

- 方法名：`getMonthDays`
- 签名：`getMonthDays(date):int`
- 说明：获取一个日期月份的天数，如：`gUtil.getMonthDays("2020-02-13")`返回29
- 参数：
  - `date`：基准日期，不许为空
- 返回：返回日期所含月份的天数
- 代码片段：`getMonthDays(${1:date})`

### 77. getMonthRange(date):{stDate,etDate}

- 方法名：`getMonthRange`
- 签名：`getMonthRange(date):{stDate,etDate}`
- 说明：获取给定日期的前一月（1号 到 月末最后一天）
- 参数：
  - `date`：给定的参考日期（允许null，null 默认当天)
- 返回：{stDate,etDate}
- 代码片段：`getMonthRange(${1:date})`

### 78. getYearRange(date):{stDate,etDate}

- 方法名：`getYearRange`
- 签名：`getYearRange(date):{stDate,etDate}`
- 说明：获取给定日期的前一年（1月1号 到 年末最后一天）
- 参数：
  - `date`：给定的参考日期（允许null，null 默认当天)
- 返回：{stDate,etDate}
- 代码片段：`getYearRange(${1:date})`

## 字符串、对象和通用工具

### 1. GUID():string

- 方法名：`GUID`
- 签名：`GUID():string`
- 说明：产生全球唯一码（`GUID`）
- 参数：无
- 返回：32位长度的全球唯一码
- 代码片段：`GUID()`

### 2. list2Map(id:string,list:object[]):object

- 方法名：`list2Map`
- 签名：`list2Map(id:string,list:object[]):object`
- 说明：数组转成对象
- 参数：
  - `id`：数组对象的唯一键值
  - `list`：数组对象
- 返回：Map; 如：ret[id].field
- 代码片段：`list2Map(${1:id},${2:list})`

### 3. listToMap(id:string,list:object[]):object

- 方法名：`listToMap`
- 签名：`listToMap(id:string,list:object[]):object`
- 说明：数组转成对象
- 参数：
  - `id`：数组对象的唯一键值
  - `list`：数组对象
- 返回：Map; 如：ret[id].field
- 代码片段：`listToMap(${1:id},${2:list})`

### 4. trimLeft(str:string):string

- 方法名：`trimLeft`
- 签名：`trimLeft(str:string):string`
- 说明：去掉给定字符串左边的不可见字符（空格、换行、回车、TAB等）
- 参数：
  - `str`：需要处理的字符串
- 返回：处理后的字符串
- 代码片段：`trimLeft(${1:str})`

### 5. trimRight(str:string):string

- 方法名：`trimRight`
- 签名：`trimRight(str:string):string`
- 说明：去掉给定字符串右边的不可见字符（空格、换行、回车、TAB等）
- 参数：
  - `str`：需要处理的字符串
- 返回：处理后的字符串
- 代码片段：`trimRight(${1:str})`

### 6. trim(str:string):string

- 方法名：`trim`
- 签名：`trim(str:string):string`
- 说明：去掉给定字符串左右两边的不可见字符（空格、换行、回车、TAB等）
- 参数：
  - `str`：需要处理的字符串
- 返回：处理后的字符串
- 代码片段：`trim(${1:str})`

### 7. isNull(obj:any):boolean

- 方法名：`isNull`
- 签名：`isNull(obj:any):boolean`
- 说明：判断给定对象是否为空
- 参数：
  - `obj`：判断给定的对象是否为空（`undefined`、`null`；若为字符串，则判断是否为空字符串）
- 返回：`true` - 为空 `false` - 非空
- 代码片段：`isNull(${1:obj})`

### 8. isNotNull(obj:any):boolean

- 方法名：`isNotNull`
- 签名：`isNotNull(obj:any):boolean`
- 说明：判断给定对象是否非空
- 参数：
  - `obj`：判断给定的对象是否非空（`undefined`、`null`；若为字符串，则判断是否为空字符串）
- 返回：`false` - 为空 `true` - 非空
- 代码片段：`isNotNull(${1:obj})`

### 9. ifNull(obj:any,defaultValue:any):object

- 方法名：`ifNull`
- 签名：`ifNull(obj:any,defaultValue:any):object`
- 说明：判断对象是否为空，若为空，则返回默认值；若非空则返回对象原值
- 参数：
  - `obj`：判断的对象
  - `defaultValue`：若对象为空时返回的值
- 返回：返回处理后的值
- 代码片段：`ifNull(${1:obj},${2:defaultValue})`

### 13. replaceAll(str:string,substr:string,newstr:string):string

- 方法名：`replaceAll`
- 签名：`replaceAll(str:string,substr:string,newstr:string):string`
- 说明：替换给定字符串里的子串
- 参数：
  - `str`：字符串
  - `substr`：要替换的字符串
  - `newstr`：替换成目标字符串
- 返回：替换后的字符串
- 代码片段：`replaceAll(${1:str},${2:substr},${3:newstr})`

### 15. clone(obj:object):object

- 方法名：`clone`
- 签名：`clone(obj:object):object`
- 说明：克隆对象
- 参数：
  - `obj`：需要克隆的对象（或数组）
- 返回：新对象
- 代码片段：`clone(${1:obj})`

### 16. copy(source:object,target:object):object

- 方法名：`copy`
- 签名：`copy(source:object,target:object):object`
- 说明：复制（合并）对象属性
- 参数：
  - `source`：源对象
  - `target`：目标对象
- 返回：合并后的对象target
- 代码片段：`copy(${1:source},${2:target})`

### 48. equals(a:string,b:string):boolean

- 方法名：`equals`
- 签名：`equals(a:string,b:string):boolean`
- 说明：判断两个值是否相同（区分大小写）
- 参数：
  - `a`：值1
  - `b`：值2
- 返回：true - a==b ; false - a != b
- 代码片段：`equals(a,b)`

### 49. equalsIgnoreCase(a:string,b:string):boolean

- 方法名：`equalsIgnoreCase`
- 签名：`equalsIgnoreCase(a:string,b:string):boolean`
- 说明：判断两个值是否相同（不区分大小写）
- 参数：
  - `a`：值1
  - `b`：值2
- 返回：true - a==b ; false - a != b
- 代码片段：`equalsIgnoreCase(a,b)`

## 文件、图片、音频和剪贴板

### 55. getSmallImageFilePath(bigFilePath:string):int

- 方法名：`getSmallImageFilePath`
- 签名：`getSmallImageFilePath(bigFilePath:string):int`
- 说明：转换大图地址为缩率图地址
- 参数：
  - `bigFilePath`：要转换的大图地址
- 返回：缩率图地址
- 代码片段：`getSmallImageFilePath(${1:bigFilePath})`

### 56. startImagePreview(imageFilePath:string):int

- 方法名：`startImagePreview`
- 签名：`startImagePreview(imageFilePath:string):int`
- 说明：显示图片预览窗口
- 参数：
  - `imageFilePath`：需要预览的图片地址（如：http://xxxx/image.png)
- 返回：无
- 代码片段：`startImagePreview(${1:imageFilePath})`

### 71. downloadWebFile(path,disName):void

- 方法名：`downloadWebFile`
- 签名：`downloadWebFile(path,disName):void`
- 说明：从文件服务器上下载一个公有文件（注意，私有文件无法用此方法下载)
- 参数：
  - `path`：文件保存地址，如： /upload/aa/bb/cc/dd/ee.txt
  - `disName`：下载时，默认的文件名称，如：文本文件.txt
- 返回：无
- 代码片段：`downloadWebFile(${1:path},${2:disName})`

### 72. downloadWebFile(path)

- 方法名：`downloadWebFile`
- 签名：`downloadWebFile(path)`
- 说明：从文件服务器上下载一个公有文件（注意，私有文件无法用此方法下载)
- 参数：
  - `path`：文件保存地址，如： /upload/aa/bb/cc/dd/ee.txt
- 返回：无
- 代码片段：`downloadWebFile(${1:path})`

### 73. playAudio(text)

- 方法名：`playAudio`
- 签名：`playAudio(text)`
- 说明：将文字转成语音并播放（需要启用华为AI)
- 参数：
  - `text`：需要合成语音的文本内容
- 返回：无
- 代码片段：`playAudio(${1:text})`

### 83. setClipboardData(text:string)

- 方法名：`setClipboardData`
- 签名：`setClipboardData(text:string)`
- 说明：将文本内容放到剪贴板
- 参数：
  - `text`：要放到剪贴板的文本内容
- 返回：无
- 代码片段：`setClipboardData(${1:text})`

### 93. isImage(imgurl:string):boolean

- 方法名：`isImage`
- 签名：`isImage(imgurl:string):boolean`
- 说明：根据文件url地址或图片名称判断是否为图片
- 参数：
  - `imgurl`：文件名称或者url地址
- 返回：无
- 代码片段：`isImage(${1:imgurl})`

### 98. isImage(url:string):boolean

- 方法名：`isImage`
- 签名：`isImage(url:string):boolean`
- 说明：根据文件扩展名判断是否为图片
- 参数：
  - `url`：文件名或者url地址
- 返回：true - 是 other - 否
- 代码片段：`isImage(${1:url})`

## 其它页面控件方法

### 12. isFunction(fun:any):boolean

- 方法名：`isFunction`
- 签名：`isFunction(fun:any):boolean`
- 说明：判断给定的对象是否是函数
- 参数：
  - `fun`：需要判断的对象
- 返回：`true` - 是 `false` -否
- 代码片段：`isFunction(${1:fun})`

### 24. turnCapital(num:number):string

- 方法名：`turnCapital`
- 签名：`turnCapital(num:number):string`
- 说明：金额转大写
- 参数：
  - `num`：需要格式化的金额
- 返回：格式化后的金额
- 代码片段：`turnCapital(${1:num})`

### 26. getMd5(str:string):string

- 方法名：`getMd5`
- 签名：`getMd5(str:string):string`
- 说明：产生MD5值
- 参数：
  - `str`：需要产生的字符串明文
- 返回：32位16进制字符串
- 代码片段：`getMd5(${1:str})`

### 27. getSM3(str:string):string

- 方法名：`getSM3`
- 签名：`getSM3(str:string):string`
- 说明：国密3摘要
- 参数：
  - `str`：需要产生的字符串明文
- 返回：国密3字符串
- 代码片段：`getSM3(${1:str})`

### 28. zIndexUp(arr:any[],index:number):void

- 方法名：`zIndexUp`
- 签名：`zIndexUp(arr:any[],index:number):void`
- 说明：数组项向上移动一位
- 参数：
  - `arr`：需要移动的数组
  - `index`：需要移动项的位置索引
- 返回：无
- 代码片段：`zIndexUp(${1:arr},${2:index})`

### 29. zIndexDown(arr:any[],index:number):void

- 方法名：`zIndexDown`
- 签名：`zIndexDown(arr:any[],index:number):void`
- 说明：数组项向下移动一位
- 参数：
  - `arr`：需要移动的数组
  - `index`：需要移动项的位置索引
- 返回：无
- 代码片段：`zIndexDown(${1:arr},${2:index})`

### 30. getPinYinCode(str:string):string

- 方法名：`getPinYinCode`
- 签名：`getPinYinCode(str:string):string`
- 说明：获取拼音
- 参数：
  - `str`：汉字字符串
- 返回：汉字拼音首字母
- 代码片段：`getPinYinCode(${1:str})`

### 57. base64encode(str:string):str

- 方法名：`base64encode`
- 签名：`base64encode(str:string):str`
- 说明：base64编码
- 参数：
  - `str`：明文字符串
- 返回：base64字符串
- 代码片段：`base64encode(${1:str})`

### 58. base64decode(base64str:string):str

- 方法名：`base64decode`
- 签名：`base64decode(base64str:string):str`
- 说明：base64解码
- 参数：
  - `base64str`：base64字符串
- 返回：明文字符串
- 代码片段：`base64decode(${1:base64str})`

### 59. loadScript(url:string,callback:function,error:function):int

- 方法名：`loadScript`
- 签名：`loadScript(url:string,callback:function,error:function):int`
- 说明：动态加载JS文件（一般在系统脚本中使用，不要在模块窗口中使用，容易导致重复加载)
- 参数：
  - `url`：JS文件路径
  - `callback`：加载成功回调
  - `error`：加载失败回调（可缺省)
- 返回：无
- 代码片段：`loadScript(${1:url},${2:callback}[,${3:error}])`

### 60. loadStyle(url:string):int

- 方法名：`loadStyle`
- 签名：`loadStyle(url:string):int`
- 说明：动态加载CSS文件（一般在系统脚本中使用，不要在模块窗口中使用，容易导致重复加载)
- 参数：
  - `url`：CSS文件的路径
- 返回：无
- 代码片段：`loadStyle(${1:url})`

### 69. getSystemVarValue(systemId,varId,defValue):string

- 方法名：`getSystemVarValue`
- 签名：`getSystemVarValue(systemId,varId,defValue):string`
- 说明：获取应用参数配置值，若为窗口JS代码，请调用快捷方法： $vm.getSystemVarValue()
- 参数：
  - `systemId`：系统编码
  - `varId`：配置编码，如： com.golden.bdp.color
  - `defValue`：默认值
- 返回：系统参数值，若不存在，则返回 `defValue`
- 代码片段：`getSystemVarValue(${1:systemId},${2:varId},null)`

### 70. getSystemVarValue(systemId,varId):string

- 方法名：`getSystemVarValue`
- 签名：`getSystemVarValue(systemId,varId):string`
- 说明：获取应用参数配置值，若为窗口JS代码，请调用快捷方法： $vm.getSystemVarValue()
- 参数：
  - `systemId`：系统编码
  - `varId`：配置编码，如： com.golden.bdp.color
- 返回：系统参数值，若不存在，则返回 `undefined`
- 代码片段：`getSystemVarValue(${1:systemId},${2:varId})`

### 74. getHostUrl():string

- 方法名：`getHostUrl`
- 签名：`getHostUrl():string`
- 说明：获取当前页面地址
- 参数：无
- 返回：返回当前页面的域名，`https://www.xxx.com:8088/gdpaas/home/index.htm`  --> `https://www.xxx.com:8088`
- 代码片段：`getHostUrl()`

### 76. getWeekRange(date):{stDate,etDate}

- 方法名：`getWeekRange`
- 签名：`getWeekRange(date):{stDate,etDate}`
- 说明：获取给定日期的前一周（周一 至 周日）的起止日期
- 参数：
  - `date`：给定的参考日期（允许null，null 默认当天)
- 返回：{stDate,etDate}
- 代码片段：`getWeekRange(${1:date})`

### 84. random(len:int):string

- 方法名：`random`
- 签名：`random(len:int):string`
- 说明：返回指定位数的随机数字字符串
- 参数：
  - `len`：指定位数，必须大于0
- 返回：随机数字字符串
- 代码片段：`random(${1:len})`

### 85. randomInt(max:int):int

- 方法名：`randomInt`
- 签名：`randomInt(max:int):int`
- 说明：返回[0,max]之间的整数
- 参数：
  - `max`：最大数，如：10
- 返回：随机数字
- 代码片段：`randomInt(${1:max})`

### 86. isMobile():boolean

- 方法名：`isMobile`
- 签名：`isMobile():boolean`
- 说明：返回当前运行环境是否移动端(H5)
- 参数：无
- 返回：true - H5 false - PC
- 代码片段：`isMobile()`

### 94. isChinese(str:string):boolean

- 方法名：`isChinese`
- 签名：`isChinese(str:string):boolean`
- 说明：判断字符串是否由纯中文组成
- 参数：
  - `str`：字符串
- 返回：true - 是 other - 否
- 代码片段：`isChinese(${1:str})`

### 95. isHaveChinese(str:string):boolean

- 方法名：`isHaveChinese`
- 签名：`isHaveChinese(str:string):boolean`
- 说明：判断字符串是否含有中文字符
- 参数：
  - `str`：字符串
- 返回：true - 是 other - 否
- 代码片段：`isHaveChinese(${1:str})`

### 96. isChineseOrNumbOrLett(str:string):boolean

- 方法名：`isChineseOrNumbOrLett`
- 签名：`isChineseOrNumbOrLett(str:string):boolean`
- 说明：检查输入字符串是否只由汉字、字母、数字组成
- 参数：
  - `str`：字符串
- 返回：true - 是 other - 否
- 代码片段：`isChineseOrNumbOrLett(${1:str})`

### 97. isCarPlateNum(str:string):boolean

- 方法名：`isCarPlateNum`
- 签名：`isCarPlateNum(str:string):boolean`
- 说明：判断字符串是否符合车牌号规则
- 参数：
  - `str`：字符串
- 返回：true - 是 other - 否
- 代码片段：`isCarPlateNum(${1:str})`

### 99. isUrl(url:string):boolean

- 方法名：`isUrl`
- 签名：`isUrl(url:string):boolean`
- 说明：根据字符串返回是否为http地址
- 参数：
  - `url`：url地址
- 返回：true - 是 other - 否
- 代码片段：`isUrl(${1:url})`

### 100. startsWith(str:string,ch:string):boolean

- 方法名：`startsWith`
- 签名：`startsWith(str:string,ch:string):boolean`
- 说明：判断字符串是否以指定字符串开头
- 参数：
  - `str`：判断的字符串
  - `ch`：比较的字符串
- 返回：true - 是 other - 否
- 代码片段：`startsWith(${1:str},${2:ch})`

### 101. endsWith(str:string,ch:string):boolean

- 方法名：`endsWith`
- 签名：`endsWith(str:string,ch:string):boolean`
- 说明：判断字符串是否以指定字符串结尾
- 参数：
  - `str`：判断的字符串
  - `ch`：比较的字符串
- 返回：true - 是 other - 否
- 代码片段：`endsWith(${1:str},${2:ch})`

### 104. getUrlParameter(name:string):void

- 方法名：`getUrlParameter`
- 签名：`getUrlParameter(name:string):void`
- 说明：获取浏览器地址上的请求参数
- 参数：
  - `name`：参数名称
- 返回：无
- 代码片段：`getUrlParameter(${1:name})`

### 105. saveTempBill(page, compScriptId:string, extconfig:object, beforeSaveCheck:function, onBeforeSave:function, succCallback:function, errCallback:function):void

- 方法名：`saveTempBill`
- 签名：`saveTempBill(page, compScriptId:string, extconfig:object, beforeSaveCheck:function, onBeforeSave:function, succCallback:function, errCallback:function):void`
- 说明：保存当前编辑页面（新增状态)为单据草稿
- 参数：
  - `page`：页面对象，如： self
  - `compScriptId`：调起后台服务组件编码（可选，若配置则必须是主数据的服务组件，用于对数据进行保存前修正）
  - `extconfig`：基础配置，可选： {mainPageId:主页面（父页面编码）,mainForm:编辑页面主表控件编码,mainTable:主页面主表格控件编码}
  - `beforeSaveCheck`：保存前检查，可选，必须返回true，否则保存不再继续,参数continueCallback为回调函数，当return false时，可以调起此函数继续保存，如：function(continueCallback){return true;}
  - `onBeforeSave`：数据发送到服务器前回调，可选 function(form){}。
  - `succCallback`：保存后成功回调，可选，如：function(result){console.log(result)}。
  - `errCallback`：保存失败后回调，可选，如：function(msg){gUtil.alert(msg)}
- 返回：无
- 代码片段：`saveTempBill(${1:page},${2:compScriptId},${3:extconfig},${4:beforeSaveCheck},${5:onBeforeSave},${6:succCallback},${7:errCallback})`
