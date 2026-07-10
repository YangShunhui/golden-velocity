# $vs Service Script API Reference

This reference is extracted from API Center > 服务脚本. Use it for method signatures and method selection. Team Golden rules in SKILL.md and golden-rules.md still take priority when there is a conflict.

## Usage Notes

- Read this file when an exact `$vs.*` method signature, parameter shape, or return type is needed.
- Keep overloads separate; do not merge methods with different signatures.
- For HTTP calls, choose the actual `$vs.http.*` method from the interface document rather than hardcoding one method.
- High-frequency business rules remain in `golden-rules.md`; this file is API reference only.

## Category Index

- `$vs.ai`: AI智能操作对象(5)
- `$vs.auth`: 用户权限对象(19)
- `$vs.billNoTools`: 单据号码对象(11)
- `$vs.barcode`: 二维码、条形码生成和识别(43)
- `$vs.cache`: 缓存类(18)
- `$vs.cipher`: 数据加解密对象(50)
- `$vs.cookie`: cookie操作对象(8)
- `$vs.dbTools`: 数据库对象(45)
- `$vs.date`: 日期工具对象(21)
- `$vs.exception`: 异常类对象(1)
- `$vs.format`: 格式化对象(4)
- `$vs.file`: 文件操作对象(55)
- `$vs.http`: HTTP请求对象(32)
- `$vs.log`: 日志类对象(6)
- `$vs.mail`: 邮件发送对象(3)
- `$vs.math`: 数学方法对象(19)
- `$vs.message`: 消息通知对象(22)
- `$vs.mq`: MQ订阅及发送对象(12)
- `$vs.ocr`: 图像识别(8)
- `$vs.page`: 谷神页面对象信息(2)
- `$vs.proc`: 过程访问对象(35)
- `$vs.properties`: 配置文件对象(28)
- `$vs.redis`: REDIS访问对象(70)
- `$vs.regexp`: 正则表达式操作对象(15)
- `$vs.report`: 报表导出文件对象(8)
- `$vs.request`: http request 原生对象(23)
- `$vs.response`: http response 原生对象(5)
- `$vs.service`: 插件服务调用对象(1)
- `$vs.sqlTools`: SQL条件对象(13)
- `$vs.sqlHelper`: SQL帮助类(20)
- `$vs.thread`: 异步线程队列对象(10)
- `$vs.user`: 当前登录用户(13, includes nested `$vs.user.member` entries in the API tree)
- `$vs.user.member`: 会员信息类(2)
- `$vs.util`: 公共工具类对象(88)
- `$vs.workflow`: 工作流对象(28)

## $vs.ai - AI智能操作对象(5 methods)

### `$vs.ai.textModeration($text:string):TextModerationResult`
- 说明： 文字内容审核（仅华为AI，需要配置华为AI服务) 
- 参数： $text:string: 需要审核的文字。 
- 返回： 审核结果对象，$result.code = 0表示成功，其他失败，$result.errmsg 中有失败的单词

### `$vs.ai.textToAudio($text:string,$voiceName:string,$speechSpeed:int):string`
- 说明： 文字合成语音（仅华为AI，需要配置华为AI服务) 
- 参数： $text:string: 需要合成的文字。 $voiceName:string: 声音类型： `F` - 女声；`M` - 男声。 $speechSpeed:int: 语速，取值 0 ~ 100，默认：`50` 正常语速，数字越高，语速越快。 
- 返回： 语音文件在当前服务器的位置临时目录位置，您需要把这个文件上传到文件服务器公共区，然后返回给浏览器JS进行播放，播放完成后，请删除语音文件，否则可能导致文件服务器垃圾文件过多问题

### `$vs.ai.textToAudio($text:string,$voiceName:string):string`
- 说明： 文字合成语音（仅华为AI，需要配置华为AI服务) 
- 参数： $text:string: 需要合成的文字。 $voiceName:string: 声音类型： `F` - 女声；`M` - 男声。 
- 返回： 语音文件在当前服务器的位置临时目录位置，您需要把这个文件上传到文件服务器公共区，然后返回给浏览器JS进行播放，播放完成后，请删除语音文件，否则可能导致文件服务器垃圾文件过多问题

### `$vs.ai.textTranslation($text:string,$toLang:string,$fromLang:string):string`
- 说明： 文字翻译（仅华为AI，需要配置华为AI服务) 
- 参数： $text:string: 需要翻译的文字。 $toLang:string: 翻译目标语言，`zh` - 中文; `en` - 英文; `ja` - 日文; `ru` - 俄文; `ko` - 韩语; `fr` - 法语; `es` - 西班牙语; `de` - 德语;。 $fromLang:string: 需要翻译的文字的语言，`zh` - 中文; `en` - 英文; `ja` - 日文; `ru` - 俄文; `ko` - 韩语; `fr` - 法语; `es` - 西班牙语; `de` - 德语;。 
- 返回： 翻译后的文字

### `$vs.ai.textTranslation($text:string,$toLang:string):string`
- 说明： 文字翻译（仅华为AI，需要配置华为AI服务) 
- 参数： $text:string: 需要翻译的文字。 $toLang:string: 翻译目标语言，`zh` - 中文; `en` - 英文; `ja` - 日文; `ru` - 俄文; `ko` - 韩语; `fr` - 法语; `es` - 西班牙语; `de` - 德语;。 
- 返回： 翻译后的文字

## $vs.auth - 用户权限对象(19 methods)

### `$vs.auth.andDataAuth($tableId:string,$tableAliasName:string):string`
- 说明： 获取当前用户数据权限SQL。 
- 参数： $tableId:string: 需要判断的表。 $tableAliasName:string: 表在查询SQL中的别名，默认`$tableId`。 
- 返回： 返回对应用户的数据权限SQL条件

### `$vs.auth.andDataAuth($tableId:string):string`
- 说明： 获取当前用户数据权限SQL。 
- 参数： $tableId:string: 需要判断的表。 
- 返回： 返回对应用户的数据权限SQL条件

### `$vs.auth.doUserFieldLoginAPP($userId:string,$loginField:string,$langId:string):User`
- 说明： 使用用户唯一编码初始化当前浏览器的登录环境（一般用于三方系统单点登录），注意：本方法只可在主数据环境下运行。 
- 参数： $userId:string: 用户编码（$loginField字段指向的值）。 $loginField:string: 登录用户表中，识别用户的唯一字段，如：USER_ID，或者 MOBILE等。 $langId:string: 语言编码，如： en。 
- 返回： 登录用户信息

### `$vs.auth.doUserFieldLoginAPP($userId:string,$loginField:string):User`
- 说明： 使用用户唯一编码初始化当前浏览器的登录环境（一般用于三方系统单点登录），注意：本方法只可在主数据环境下运行。 
- 参数： $userId:string: 用户编码（$loginField字段指向的值）。 $loginField:string: 登录用户表中，识别用户的唯一字段，如：USER_ID，或者 MOBILE等。 
- 返回： 登录用户信息

### `$vs.auth.doUserFieldLoginPC($userId:string,$loginField:string,$langId:string):User`
- 说明： 使用用户唯一编码初始化当前浏览器的登录环境（一般用于三方系统单点登录），注意：本方法只可在主数据环境下运行。 
- 参数： $userId:string: 用户编码（$loginField字段指向的值），可以是USER_ID、MOBILE、LOGIN_ID。 $loginField:string: 登录用户表中，识别用户的唯一字段，如：USER_ID，或者 MOBILE等。 $langId:string: 语言编码，如： en。 
- 返回： 登录用户信息

### `$vs.auth.doUserFieldLoginPC($userId:string,$loginField:string):User`
- 说明： 使用用户唯一编码初始化当前浏览器的登录环境（一般用于三方系统单点登录），注意：本方法只可在主数据环境下运行。 
- 参数： $userId:string: 用户编码（$loginField字段指向的值），可以是USER_ID、MOBILE、LOGIN_ID。 $loginField:string: 登录用户表中，识别用户的唯一字段，如：USER_ID，或者 MOBILE等。 
- 返回： 登录用户信息

### `$vs.auth.doUserTaskLogin($userId:string,$systemId:string):User`
- 说明： 以服务端身份登录，并初始化登录场景，一般用于接口调用时初始化当前请求的用户执行身份（注意：不可在用户发起的请求里调用本方法，只可在服务调用环境中心运行）。 
- 参数： $userId:string: 用户编码。 $systemId:string: 用户所在的主数据系统编码，默认当前调起的系统的编码。 
- 返回： 登录用户信息

### `$vs.auth.doUserTaskLogin($userId:string):User`
- 说明： 以服务端身份登录，并初始化登录场景，一般用于接口调用时初始化当前请求的用户执行身份（注意：不可在用户发起的请求里调用本方法，只可在服务调用环境中心运行）。 
- 参数： $userId:string: 用户编码。 
- 返回： 登录用户信息

### `$vs.auth.getDataAuthCode($authFieldId:string):List<String>`
- 说明： 获取用户拥有的数据权限代码列表（查询数据权限）。 
- 参数： $authFieldId:string: 数据权限ID。 
- 返回： 返回值说明： 1、若返回值为 `null` 表示当前数据权限未启用或者不控制当前操作员的权限（如果系统管理员或者其他豁免权限的用户） 2、若返回值为 empty 数组 null!=$list && $list.size() == 0，则表示当前用户没有任何权限 3、其他情况正常。

### `$vs.auth.getMenus($mkId:string):Menus`
- 说明： 获取菜单信息。 
- 参数： $mkId:string: 菜单编码。 
- 返回： 返回菜单信息，若菜单不存在，则返回`null`

### `$vs.auth.getUserAuths($mkId:string,$auths:string,$userId:string):Map<String,Integer>`
- 说明： 获取指定用户对指定模式是否存在指定的按钮权限。 
- 参数： $mkId:string: 菜单编码。 $auths:string: 按钮权限编码，`*`或者空，表示查询所有，如：`edit`，请求多个按钮权限，请使用“,”分隔，如：`edit,select,audit`，若要判断用户是否具有打开模块的权限，则传值 `select`。 $userId:string: 需要查询的用户编码，不存在或者`null`表示当前登录的用户。 
- 返回： 返回对应的按钮权限

### `$vs.auth.getUserAuths($mkId:string,$auths:string):Map<String,Integer>`
- 说明： 获取当前登录用户对指定模式是否存在指定的按钮权限。 
- 参数： $mkId:string: 菜单编码。 $auths:string: 按钮权限编码，`*`或者空，表示查询所有，如：`edit`，请求多个按钮权限，请使用“,”分隔，如：`edit,select,audit`，若要判断用户是否具有打开模块的权限，则传值 `select`。 
- 返回： 返回对应的按钮权限

### `$vs.auth.getUserAuthsWithPageId($mkId:string,$auths:string,$pageId:string,$userId:string):Map<String,Integer>`
- 说明： 获取指定用户对指定模式是否存在指定的按钮权限。 
- 参数： $mkId:string: 菜单编码。 $auths:string: 按钮权限编码，`*`或者空，表示查询所有，如：`edit`，请求多个按钮权限，请使用“,”分隔，如：`edit,select,audit`，若要判断用户是否具有打开模块的权限，则传值 `select`。 pageId: 页面编码，如：子页编码或者主页面编码，其他编码无效；若为`null`则效果同`$vs.auth.getUserAuths($mkId,$auths,$userId)`；若存在页面编码，则复合判断菜单是否存在权限，若不存在，则会判断页面所属的菜单是否存在权限，若存在，则视为有权限。 $userId:string: 需要查询的用户编码，不存在或者`null`表示当前登录的用户。 
- 返回： 返回对应的按钮权限

### `$vs.auth.getUserAuthsWithPageId($mkId:string,$auths:string,$pageId:string):Map<String,Integer>`
- 说明： 获取当前登录用户对指定模式是否存在指定的按钮权限。 
- 参数： $mkId:string: 菜单编码。 $auths:string: 按钮权限编码，`*`或者空，表示查询所有，如：`edit`，请求多个按钮权限，请使用“,”分隔，如：`edit,select,audit`，若要判断用户是否具有打开模块的权限，则传值 `select`。 pageId: 页面编码，如：子页编码或者主页面编码，其他编码无效；若为`null`则效果同`$vs.auth.getUserAuths($mkId,$auths)`；若存在页面编码，则复合判断菜单是否存在权限，若不存在，则会判断页面所属的菜单是否存在权限，若存在，则视为有权限。 
- 返回： 返回对应的按钮权限

### `$vs.auth.getUserDataAuths($userId:string,$authFieldId:string):Map<String, List<String>>`
- 说明： 获指定数据权限类型下用户的数据权限。`本方法需要访问数据库，尽量不要在循环中使用，否则执行效率很低。` 
- 参数： $userId:string: 用户编码。 $authFieldId:string: 数据权限编码，如：DEPT_CODE。 
- 返回： 返回用户所拥有的指定数据权限列表（注意：超级管理员用户可能返回空列表），结构：`Map<${authFieldId}_SELECT | ${authFieldId}_EDIT, List

### `$vs.auth.getUserDataAuths($userId:string):Map<String, List<String>>`
- 说明： 获用户所拥有的所有数据权限。`本方法需要访问数据库，尽量不要在循环中使用，否则执行效率很低。` 
- 参数： $userId:string: 用户编码。 
- 返回： 返回用户所拥有的指定数据权限列表（注意：超级管理员用户可能返回空列表），结构：`Map<${authFieldId}_SELECT | ${authFieldId}_EDIT, List

### `$vs.auth.getUsersDataAuths($userIds:List<string>,$authFieldId:string):Map<String, Map<String, List<String>>>`
- 说明： 获指定数据权限类型下用户的数据权限。`本方法需要访问数据库，尽量不要在循环中使用，否则执行效率很低。` 
- 参数： $userIds:List : 用户编码数组。 $authFieldId:string: 数据权限编码，如：DEPT_CODE。 
- 返回： 返回拥有的指定数据权限列表（注意：超级管理员用户可能返回空列表），结构：`Map<${userId},Map<${authFieldId}_SELECT | ${authFieldId}_EDIT, List

### `$vs.auth.getUsersDataAuths($userIds:List<string>):Map<String, Map<String, List<String>>>`
- 说明： 获指定数据权限类型下用户的数据权限。`本方法需要访问数据库，尽量不要在循环中使用，否则执行效率很低。` 
- 参数： $userIds:List : 用户编码数组。 
- 返回： 返回拥有的指定数据权限列表（注意：超级管理员用户可能返回空列表），结构：`Map<${userId},Map<${authFieldId}_SELECT | ${authFieldId}_EDIT, List

### `$vs.auth.offCurThreadDataAuth():void`
- 说明： 禁用当前线程的所有数据权限校验（支持跨微服务调用和子线程）。 
- 参数： 无 
- 返回： 无

## $vs.billNoTools - 单据号码对象(11 methods)

### `$vs.billNoTools.createBillBatchNo($strBillCode:string,$intMaxBatichNo:int,$intBatchNoLen:int,$strFrontChar:string):string`
- 说明： 创建单据明细流水码 
- 参数： $strBillCode:string: 单据主表号码。 $intMaxBatichNo:int: 当前明细的序号。 $intBatchNoLen:int: 明细批号自增流水号码长度，默认：4位，可缺省。 $strFrontChar:string: 明细批号中，单据主表号码和序号间隔字符，默认为空，可缺省。 
- 返回： 新创建的单据号码

### `$vs.billNoTools.createBillBatchNo($strBillCode:string,$intMaxBatichNo:int,$intBatchNoLen:int):string`
- 说明： 创建单据明细流水码 
- 参数： $strBillCode:string: 单据主表号码。 $intMaxBatichNo:int: 当前明细的序号。 $intBatchNoLen:int: 明细批号自增流水号码长度，默认：4位，可缺省。 
- 返回： 新创建的单据号码

### `$vs.billNoTools.createBillBatchNo($strBillCode:string,$intMaxBatichNo:int):string`
- 说明： 创建单据明细流水码 
- 参数： $strBillCode:string: 单据主表号码。 $intMaxBatichNo:int: 当前明细的序号。 
- 返回： 新创建的单据号码

### `$vs.billNoTools.getBatchBillNo($form:Map<string,?>,$count:int):List<string>`
- 说明： 根据单据号码规则批量创建单据号码 
- 参数： $form:Map: 主表数据对象（必须指定单据类型）。 $count:int: 要批量创建的单据号码个数，必须大于等于1。 
- 返回： 新创建的单据号码

### `$vs.billNoTools.getBatchBillNo($strBillTypeCode:string,$form:Map<string,?>,$count:int):List<string>`
- 说明： 根据单据号码规则批量创建单据号码 
- 参数： $strBillTypeCode:string: 单据类型编码。 $form:Map: 主表数据对象。 $count:int: 要批量创建的单据号码个数，必须大于等于1。 
- 返回： 新创建的单据号码

### `$vs.billNoTools.getBillNo($form:Map<string,?>):string`
- 说明： 根据单据号码规则创建单据号码 
- 参数： $form:Map: 主表数据对象（必须指定单据类型）。 
- 返回： 新创建的单据号码

### `$vs.billNoTools.getBillNo($strBillTypeCode:string,$form:Map<string,?>)`
- 说明： 根据单据号码规则创建单据号码 
- 参数： $strBillTypeCode:string: 单据类型编码。 $form:Map: 主表数据对象。 
- 返回： 新创建的单据号码

### `$vs.billNoTools.getMaxBillBatchNo($strTableName:string,$strBillCodeFieldId:string,$strBillCode:string,$strBillBatchFieldId:string,$intBatchNoLen:int):int`
- 说明： 获取当前单据下明细批号的最大流水码 
- 参数： $strTableName:string: 单据明细表名。 $strBillCodeFieldId:string: 单据明细表中，单据编码字段。 $strBillCode:string: 单据明细表中，单据编码值。 $strBillBatchFieldId:string: 单据明细表中，明细批号字段。 $intBatchNoLen:int: 明细批号自增流水号码长度，默认：4位，可缺省。 
- 返回： 单据下明细批号的最大流水码数字序号

### `$vs.billNoTools.getMaxBillBatchNo($strTableName:string,$strBillCodeFieldId:string,$strBillCode:string,$strBillBatchFieldId:string):int`
- 说明： 获取当前单据下明细批号的最大流水码 
- 参数： $strTableName:string: 单据明细表名。 $strBillCodeFieldId:string: 单据明细表中，单据编码字段。 $strBillCode:string: 单据明细表中，单据编码值。 $strBillBatchFieldId:string: 单据明细表中，明细批号字段。 
- 返回： 单据下明细批号的最大流水码数字序号

### `$vs.billNoTools.getSeqNo($strTableName:string,$strHead:string,$intLen:int):string`
- 说明： 创建流水码 
- 参数： $strTableName:string: 流水码标识（建议用表名）。 $strHead:string: 流水码头标识（可为`null`），如：M，则生成的代码类似`M01001`。 $intLen:int: 流水码长度。 
- 返回： 新创建的单据号码

### `$vs.billNoTools.parseBillNoHeader($strBillTypeCode:string,$form:Map<string,?>):string`
- 说明： 解析单据类型，生产单据号码头（含日期【若有】，不含流水号部分） 
- 参数： $strBillTypeCode:string: 单据类型编码。 $form:int: 单据主表。 
- 返回： 推测的单据头号码

## $vs.barcode - 二维码、条形码生成和识别(43 methods)

### `$vs.barcode.createCode128($text:string,$hideText:boolean,$dpi:int,$width:int,$height:int):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 $width:int: 图片宽度，可缺省，若缺省或传值`null`，且传值 `$height`， 则保持图片高宽比，宽度采用图片高度等比缩放。。 $height:int: 图片高度，可缺省，若缺省或传值`null`，且传值 `$width`， 则保持图片高宽比，高度采用图片宽度等比缩放。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createCode128($text:string,$hideText:boolean,$dpi:int,$width:int):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 $width:int: 图片宽度，可缺省，若传值，则图片宽度采用此值，图片高度采用图片宽度等比缩放。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createCode128($text:string,$hideText:boolean,$dpi:int):byte[]`
- 说明： 创建Code128类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createCode128($text:string,$hideText:boolean):byte[]`
- 说明： 创建Code128类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createCode128($text:string):byte[]`
- 说明： 创建Code128类型的条码 
- 参数： $text:string: 条码文字内容。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createCode39($text:string,$hideText:boolean,$dpi:int,$width:int,$height:int):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 $width:int: 图片宽度，可缺省，若缺省或传值`null`，且传值 `$height`， 则保持图片高宽比，宽度采用图片高度等比缩放。。 $height:int: 图片高度，可缺省，若缺省或传值`null`，且传值 `$width`， 则保持图片高宽比，高度采用图片宽度等比缩放。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createCode39($text:string,$hideText:boolean,$dpi:int,$width:int):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 $width:int: 图片宽度，可缺省，若传值，则图片宽度采用此值，图片高度采用图片宽度等比缩放。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createCode39($text:string,$hideText:boolean,$dpi:int):byte[]`
- 说明： 创建Code39类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createCode39($text:string,$hideText:boolean):byte[]`
- 说明： 创建Code39类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createCode39($text:string):byte[]`
- 说明： 创建Code39类型的条码 
- 参数： $text:string: 条码文字内容。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createEAN128($text:string,$hideText:boolean,$dpi:int,$width:int,$height:int):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 $width:int: 图片宽度，可缺省，若缺省或传值`null`，且传值 `$height`， 则保持图片高宽比，宽度采用图片高度等比缩放。。 $height:int: 图片高度，可缺省，若缺省或传值`null`，且传值 `$width`， 则保持图片高宽比，高度采用图片宽度等比缩放。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createEAN128($text:string,$hideText:boolean,$dpi:int,$width:int):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 $width:int: 图片宽度，可缺省，若传值，则图片宽度采用此值，图片高度采用图片宽度等比缩放。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createEAN128($text:string,$hideText:boolean,$dpi:int):byte[]`
- 说明： 创建EAN128类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createEAN128($text:string,$hideText:boolean):byte[]`
- 说明： 创建EAN128类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createEAN128($text:string):byte[]`
- 说明： 创建EAN128类型的条码 
- 参数： $text:string: 条码文字内容。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createEAN13($text:string,$hideText:boolean,$dpi:int,$width:int,$height:int):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 $width:int: 图片宽度，可缺省，若缺省或传值`null`，且传值 `$height`， 则保持图片高宽比，宽度采用图片高度等比缩放。。 $height:int: 图片高度，可缺省，若缺省或传值`null`，且传值 `$width`， 则保持图片高宽比，高度采用图片宽度等比缩放。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createEAN13($text:string,$hideText:boolean,$dpi:int,$width:int):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 $width:int: 图片宽度，可缺省，若传值，则图片宽度采用此值，图片高度采用图片宽度等比缩放。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createEAN13($text:string,$hideText:boolean,$dpi:int):byte[]`
- 说明： 创建EAN13类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createEAN13($text:string,$hideText:boolean):byte[]`
- 说明： 创建EAN13类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createEAN13($text:string):byte[]`
- 说明： 创建EAN13类型的条码 
- 参数： $text:string: 条码文字内容。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createEAN8($text:string,$hideText:boolean,$dpi:int,$width:int,$height:int):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 $width:int: 图片宽度，可缺省，若缺省或传值`null`，且传值 `$height`， 则保持图片高宽比，宽度采用图片高度等比缩放。。 $height:int: 图片高度，可缺省，若缺省或传值`null`，且传值 `$width`， 则保持图片高宽比，高度采用图片宽度等比缩放。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createEAN8($text:string,$hideText:boolean,$dpi:int,$width:int):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 $width:int: 图片宽度，可缺省，若传值，则图片宽度采用此值，图片高度采用图片宽度等比缩放。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createEAN8($text:string,$hideText:boolean,$dpi:int):byte[]`
- 说明： 创建EAN8类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createEAN8($text:string,$hideText:boolean):byte[]`
- 说明： 创建EAN8类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createEAN8($text:string):byte[]`
- 说明： 创建EAN8类型的条码 
- 参数： $text:string: 条码文字内容。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createQrCode($text:string,$width:int,$charset:string):byte[]`
- 说明： 创建二维码图片(无LOGO图片) 
- 参数： $text:string: 二维码文字内容。 $width:string: 二维码宽度、高度。 $charset:string: 字符集，默认：UTF-8。 
- 返回： 二维码图片二进制内容

### `$vs.barcode.createQrCode($text:string,$width:int):byte[]`
- 说明： 创建二维码图片(无LOGO图片) 
- 参数： $text:string: 二维码文字内容。 $width:string: 二维码宽度、高度。 
- 返回： 二维码图片二进制内容

### `$vs.barcode.createQrCode($text:string):byte[]`
- 说明： 创建二维码图片(无LOGO图片) 
- 参数： $text:string: 二维码文字内容。 
- 返回： 二维码图片二进制内容

### `$vs.barcode.createQrCodeWithLogo($text:string,$logoFilePath:string,$width:int,$charset:string):byte[]`
- 说明： 创建二维码图片(含LOGO图片) 
- 参数： $text:string: 二维码文字内容。 $logoFilePath:string: 图片相对路径，可以放在本地临时目录或者文件服务器上。 $width:string: 二维码宽度、高度。 $charset:string: 字符集，默认：UTF-8。 
- 返回： 二维码图片二进制内容

### `$vs.barcode.createQrCodeWithLogo($text:string,$logoFilePath:string,$width:int):byte[]`
- 说明： 创建二维码图片(含LOGO图片) 
- 参数： $text:string: 二维码文字内容。 $logoFilePath:string: 图片相对路径，可以放在本地临时目录或者文件服务器上。 $width:string: 二维码宽度、高度。 
- 返回： 二维码图片二进制内容

### `$vs.barcode.createQrCodeWithLogo($text:string,$logoFilePath:string):byte[]`
- 说明： 创建二维码图片(含LOGO图片) 
- 参数： $text:string: 二维码文字内容。 $logoFilePath:string: 图片相对路径，可以放在本地临时目录或者文件服务器上。 
- 返回： 二维码图片二进制内容

### `$vs.barcode.createUPCA($text:string,$hideText:boolean,$dpi:int,$width:int,$height:int):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 $width:int: 图片宽度，可缺省，若缺省或传值`null`，且传值 `$height`， 则保持图片高宽比，宽度采用图片高度等比缩放。。 $height:int: 图片高度，可缺省，若缺省或传值`null`，且传值 `$width`， 则保持图片高宽比，高度采用图片宽度等比缩放。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createUPCA($text:string,$hideText:boolean,$dpi:int,$width:int):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 $width:int: 图片宽度，可缺省，若传值，则图片宽度采用此值，图片高度采用图片宽度等比缩放。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createUPCA($text:string,$hideText:boolean,$dpi:int):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createUPCA($text:string,$hideText:boolean):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createUPCA($text:string):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createUPCE($text:string,$hideText:boolean,$dpi:int,$width:int,$height:int):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 $width:int: 图片宽度，可缺省，若缺省或传值`null`，且传值 `$height`， 则保持图片高宽比，宽度采用图片高度等比缩放。。 $height:int: 图片高度，可缺省，若缺省或传值`null`，且传值 `$width`， 则保持图片高宽比，高度采用图片宽度等比缩放。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createUPCE($text:string,$hideText:boolean,$dpi:int,$width:int):byte[]`
- 说明： 创建UPC_A类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 $width:int: 图片宽度，可缺省，若传值，则图片宽度采用此值，图片高度采用图片宽度等比缩放。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createUPCE($text:string,$hideText:boolean,$dpi:int):byte[]`
- 说明： 创建UPC_E类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 $dpi:int: 分辨率，默认：200，数字越高，条码宽横比越高，同时图片清晰度越高。。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createUPCE($text:string,$hideText:boolean):byte[]`
- 说明： 创建UPC_E类型的条码 
- 参数： $text:string: 条码文字内容。 $hideText:string: 是否隐藏文字（不在条码上显示文字） true - 不显示文字 false - 显示（默认）。 
- 返回： 条码图片二进制内容

### `$vs.barcode.createUPCE($text:string):byte[]`
- 说明： 创建UPC_E类型的条码 
- 参数： $text:string: 条码文字内容。 
- 返回： 条码图片二进制内容

### `$vs.barcode.decode($path:string,$charset:string):string`
- 说明： 解析二维码、条形码 
- 参数： $path:string: 二维码图片相对路径，可以放在本地临时目录或者文件服务器上。 $charset:string: 字符集，默认：UTF-8。 
- 返回： 二维码/条码内容

### `$vs.barcode.decode($path:string):string`
- 说明： 解析二维码、条形码 
- 参数： $path:string: 二维码图片相对路径，可以放在本地临时目录或者文件服务器上。 
- 返回： 二维码/条码内容

## $vs.cache - 缓存类(18 methods)

### `$vs.cache.getBean($strTableId:string,$dataFieldValue:object):Map<string,?>`
- 说明： 获取缓存对象 
- 参数： $strTableId:string: 表名称。 $dataFieldValue:object: 表缓存字段对应的值。 
- 返回： 缓存对象

### `$vs.cache.getCache($strCacheKEY:string):object`
- 说明： 从缓存中获取数据 
- 参数： $strCacheKEY:string: 键值。 
- 返回： 缓存中的数据，若缓存不存在或者数据已超时，则返回`null`

### `$vs.cache.getCodes($strCodeType:string,$hasAll:boolean):List`
- 说明： 获取数据字典对应的集合 
- 参数： $strCodeType:string: 数据字典类型，如：`合同状态`。 $hasAll:boolean: 是否包含所有状态，`true` - 所有记录 `false` - 只含启用记录。 
- 返回： 数据字典对应的集合(`List`类型)

### `$vs.cache.getCodes($strCodeType:string):List`
- 说明： 获取数据字典对应的集合（所有记录，含未启用记录） 
- 参数： $strCodeType:string: 数据字典类型，如：`合同状态`。 
- 返回： 数据字典对应的集合(`List`类型)

### `$vs.cache.getCodesValue($strCodeType:string,$strCodeValue:string,$defValue:string):string`
- 说明： 获取数据字典对应的显示值 
- 参数： $strCodeType:string: 数据字典类型，如：`合同状态`。 $strCodeValue:string: 数据字典对应的值，如：`1`。 $defValue:string: 当前对应的数据字典不存在时，返回的默认值。 
- 返回： 数据字典对应的显示值

### `$vs.cache.getCodesValue($strCodeType:string,$strCodeValue:string):string`
- 说明： 获取数据字典对应的显示值 
- 参数： $strCodeType:string: 数据字典类型，如：`合同状态`。 $strCodeValue:string: 数据字典对应的值，如：`1`。 
- 返回： 数据字典对应的显示值

### `$vs.cache.getImageRandomCode():string`
- 说明： 从缓存中获取图片验证码，图片验证码加载地址：`ROOT_PATH/authimg.img?width=100&height=50` ``` 如： ``` 
- 参数： 无 
- 返回： 自动产生的图片验证码随机字符串

### `$vs.cache.getUserSessionCache($strCacheKEY:string):object`
- 说明： 从用户会话缓存中获取数据 
- 参数： $strCacheKEY:string: 键值。 
- 返回： 缓存中的数据，若缓存不存在，则返回`null`

### `$vs.cache.getValue($strTableId:string,$fieldName:string,$dataFieldValue:object):object`
- 说明： 获取缓存对象（单字段数据唯一性） 
- 参数： $strTableId:string: 表名称。 $fieldName:string: 需要获取的字段名称。 $dataFieldValue:object: 表缓存字段对应的值。 
- 返回： 缓存对象对应字段`$fieldName`的值

### `$vs.cache.putCache($strCacheKEY:string,$data:object,$timeout:int):void`
- 说明： 把数据放到缓存（若redis启用则放到redis否则放到服务器本地内容) 
- 参数： $strCacheKEY:string: 键值。 $data:object: 数据。 $timeout:object: 数据生存时间（秒)。 
- 返回： 无

### `$vs.cache.putCache($strCacheKEY:string,$data:object):void`
- 说明： 把数据放到缓存（若redis启用则放到redis否则放到服务器本地内容)，数据永久有效 
- 参数： $strCacheKEY:string: 键值。 $data:object: 数据。 
- 返回： 无

### `$vs.cache.putUserSessionCache($strCacheKEY:string,$data:object):void`
- 说明： 把数据放到用户会话缓存中（用户退出登录后数据连带删除) 
- 参数： $strCacheKEY:string: 键值。 $data:string: 数据。 
- 返回： 无

### `$vs.cache.refreshUserSession($userId:string,$systemId:string):void`
- 说明： 刷新用户缓存，刷新内容包括：操作权限、数据权限、会员信息（协同用户）、用户身份（管理or系统管理员）、登录初始化脚本执行等。 
- 参数： $userId:string: 要刷新的用户编码。 $systemId:string: 用户对应的系统编码（默认调用系统系主系统编码）。 
- 返回： 无

### `$vs.cache.refreshUserSession($userId:string):void`
- 说明： 刷新用户缓存，刷新内容包括：操作权限、数据权限、会员信息（协同用户）、用户身份（管理or系统管理员）、登录初始化脚本执行等。 
- 参数： $userId:string: 要刷新的用户编码。 
- 返回： 无

### `$vs.cache.removeCache($strCacheKEY:string):void`
- 说明： 从缓存中删除数据 
- 参数： $strCacheKEY:string: 键值。 
- 返回： 无

### `$vs.cache.removeCacheBean($strTableId:string,$dataFieldValue:object):void`
- 说明： 删除缓存对象（用于刷新缓存数据） 
- 参数： $strTableId:string: 表名称。 $dataFieldValue:object: 表缓存字段对应的值。 
- 返回： 无

### `$vs.cache.removeUserSessionCache($strCacheKEY:string):object`
- 说明： 从用户会话缓存中删除数据 
- 参数： $strCacheKEY:string: 键值。 
- 返回： 无

### `$vs.cache.reputUserSession():void`
- 说明： 重新更新REDIS中的当前登录用户会话信息 
- 参数： 无 
- 返回： 无

## $vs.cipher - 数据加解密对象(50 methods)

### `$vs.cipher.base64DeCode($base64str:string):byte[]`
- 说明： 对BASE64字符串解码，并返回二进制数组 
- 参数： $base64str:string: BASE64字符串。 
- 返回： BASE64字符串解码后的二进制数组

### `$vs.cipher.base64EnCode($bytes:byte[]):string`
- 说明： 对二进制数组进行BASE64编码，返回base64字符串 
- 参数： $bytes:byte[]: 二进制数组。 
- 返回： BASE64字符串

### `$vs.cipher.bytesToHex($bytes:byte[]):string`
- 说明： 将二进制字节数组转为十六进制字符串（大写） 
- 参数： $bytes:byte[]: 二进制字节数组。 
- 返回： 16进制字符串

### `$vs.cipher.createSm2Keys():List<string>`
- 说明： 创建国密非对称加密秘钥对 
- 参数： 无 
- 返回： [0:公钥base64字符串,1:私钥base64字符串]

### `$vs.cipher.createUserPassword($userId:string,$password:string):string`
- 说明： 创建用户登录密码字符串 
- 参数： $userId:string: 用户编码。 $password:string: 密码明文。 
- 返回： 用户登录密码字符串

### `$vs.cipher.decodeAES($base64:string,$key:string):string`
- 说明： 对数据进行AES解密 
- 参数： $base64:string: 需解密的密文Base64格式。 $key:string: 加密密钥。 
- 返回： 数据原文

### `$vs.cipher.decodeData($data:string):string`
- 说明： 对数据进行解密 
- 参数： $data:string: 数据密文Base64字符串。 
- 返回： 数据明文

### `$vs.cipher.decodeDES($base64:string,$key:string):string`
- 说明： 对数据进行DES解密 
- 参数： $base64:string: 需解密的密文Base64格式。 $key:string: 加密密钥。 
- 返回： 数据原文

### `$vs.cipher.encodeAES($data:string,$key:string):string`
- 说明： 对数据进行AES加密 
- 参数： $data:string: 需要加密的数据原文。 $key:string: 加密密钥。 
- 返回： 数据密文BASE64字符串

### `$vs.cipher.encodeData($data:string):string`
- 说明： 对数据进行加密 
- 参数： $data:string: 数据明文。 
- 返回： 数据密文Base64字符串

### `$vs.cipher.encodeDES($data:string,$key:string):string`
- 说明： 对数据进行DES加密 
- 参数： $data:string: 需要加密的数据原文。 $key:string: 加密密钥。 
- 返回： 数据密文BASE64字符串

### `$vs.cipher.hexToBytes($str:string):byte[]`
- 说明： 将十六进制字符串转为二进制字节数组 
- 参数： $str:string: 十六进制字符串。 
- 返回： 二进制数组

### `$vs.cipher.hmacSHA256($data:string,$secret:string,$charset:string):string`
- 说明： HmacSHA256摘要算法 
- 参数： $data:string: 要摘要的数据明文。 $secret:string: 密钥。 $charset:string: `$data`及`$secret`字符集，如：utf-8。 
- 返回： 摘要后的32位16进制字符串

### `$vs.cipher.hmacSHA256($data:string,$secret:string):string`
- 说明： HmacSHA256摘要算法 
- 参数： $data:string: 要摘要的数据明文。 $secret:string: 密钥。 
- 返回： 摘要后的32位16进制字符串

### `$vs.cipher.hmacSHA256B($data:byte[],$secret:byte[]):byte[]`
- 说明： HmacSHA256摘要算法（字节版） 
- 参数： $data:byte[]: 要摘要的数据明文。 $secret:byte[]: 密钥。 
- 返回： 摘要后的字节数组

### `$vs.cipher.hmacSHA256S($data:string,$secret:string):byte[]`
- 说明： HmacSHA256摘要算法（字节版） 
- 参数： $data:string: 要摘要的数据明文。 $secret:string: 密钥。 
- 返回： 摘要后的字节数组

### `$vs.cipher.hmacSHA512($data:string,$secret:string,$charset:string):string`
- 说明： HmacSHA512摘要算法 
- 参数： $data:string: 要摘要的数据明文。 $secret:string: 密钥。 $charset:string: `$data`及`$secret`字符集，如：utf-8。 
- 返回： 摘要后的32位16进制字符串

### `$vs.cipher.hmacSHA512($data:string,$secret:string):string`
- 说明： HmacSHA512摘要算法 
- 参数： $data:string: 要摘要的数据明文。 $secret:string: 密钥。 
- 返回： 摘要后的32位16进制字符串

### `$vs.cipher.hmacSHA512B($data:byte[],$secret:byte[]):byte[]`
- 说明： HmacSHA512摘要算法（字节版） 
- 参数： $data:byte[]: 要摘要的数据明文。 $secret:byte[]: 密钥。 
- 返回： 摘要后的字节数组

### `$vs.cipher.hmacSHA512S($data:string,$secret:string):byte[]`
- 说明： HmacSHA512摘要算法（字节版） 
- 参数： $data:string: 要摘要的数据明文。 $secret:string: 密钥。 
- 返回： 摘要后的字节数组

### `$vs.cipher.replaceHtmlToStr($htmlstr:string):string`
- 说明： 将HTML字符串转义（如： 空格 转义为 ） 
- 参数： $htmlstr:string: HTML字符串。 
- 返回： 转义的字符串

### `$vs.cipher.replaceStrToHtml($str:string):string`
- 说明： 将字符串转义HTML（如： 转义为 空格 ） 
- 参数： $str:string: 字符串。 
- 返回： 转义的字符串

### `$vs.cipher.rsaPrivateDecode($str:string, $key:string,$len:int):string`
- 说明： 用RSA私钥解密公钥加密的密文 
- 参数： $str:string: 数据密文。 $key:string: 私钥base64字符串。 $len:int: 证书算法长度，如：1024、2048。 
- 返回： 明文字符串

### `$vs.cipher.rsaPublicDecode($str:string, $key:string,$len:int):string`
- 说明： 用RSA公钥解密私钥加密的密文 
- 参数： $str:string: 数据密文。 $key:string: 公钥base64字符串。 $len:int: 证书算法长度，如：1024、2048。 
- 返回： 明文字符串

### `$vs.cipher.rsaPublicEncode($str:string, $key:string,$len:int):string`
- 说明： 用RSA公钥对数据进行加密 
- 参数： $str:string: 数据明文（若需要加密的数据为二进制格式，则请自行加密为base64格式的字符串，然后再进行加密操作）。 $key:string: 公钥base64字符串。 $len:int: 证书算法长度，如：1024、2048。 
- 返回： 加密后的base64字符串

### `$vs.cipher.rsaSign($str:string, $key:string,$type:string):string`
- 说明： 用RSA私钥签名 
- 参数： $str:string: 要签名的数据明文。 $key:string: 私钥base64字符串。 $type:string: 签名算法（具体传值详见证书属性），可选值：NONEwithRSA, MD2withRSA, MD5withRSA, SHA1withRSA, SHA224withRSA, SHA256withRSA, SHA384withRSA, SHA512withRSA。 
- 返回： 明文字符串

### `$vs.cipher.rsaVerify($str:string, $sign:string, $key:string,$type:string):boolean`
- 说明： 用RSA公钥验签 
- 参数： $str:string: 数据明文。 $sign:string: 数据签名摘要。 $key:string: 公钥base64字符串。 $type:string: 签名算法（具体传值详见证书属性），可选值：NONEwithRSA, MD2withRSA, MD5withRSA, SHA1withRSA, SHA224withRSA, SHA256withRSA, SHA384withRSA, SHA512withRSA。 
- 返回： true - 正确 false - 错误

### `$vs.cipher.sha($src:string,$type:string):string`
- 说明： 字符串摘要SHA-X系列算法 
- 参数： $src:string: 明文字符串。 $type:string: 算法类型：MD2, MD5, SHA-1, SHA-224, SHA-256, SHA-512, SHA-384, SHA-512/224, SHA-512/256, SHA3-224, SHA3-256, SHA3-384, SHA3-512。 
- 返回： 加密后的16进制字符串

### `$vs.cipher.signHmac($hmacType:string,$data:string,$secret:string):string`
- 说明： Hmac算法通用版（base64版） 
- 参数： $hmacType:string: 算法类型，如：HmacMD5、HmacSHA1、HmacSHA224、HmacSHA256、HmacSHA384、HmacSHA512。 $data:string: 要摘要的数据明文。 $secret:string: 密钥。 
- 返回： 摘要后的base64字符串

### `$vs.cipher.signHmacMD5($data:string,$secret:string):string`
- 说明： HmacDM5摘要算法（base64版） 
- 参数： $data:string: 要摘要的数据明文。 $secret:string: 密钥。 
- 返回： 摘要后的base64字符串

### `$vs.cipher.signHmacSHA1($data:string,$secret:string):string`
- 说明： HmacSHA1摘要算法（base64版） 
- 参数： $data:string: 要摘要的数据明文。 $secret:string: 密钥。 
- 返回： 摘要后的base64字符串

### `$vs.cipher.signHmacSHA224($data:string,$secret:string):string`
- 说明： HmacSHA224摘要算法（base64版） 
- 参数： $data:string: 要摘要的数据明文。 $secret:string: 密钥。 
- 返回： 摘要后的base64字符串

### `$vs.cipher.signHmacSHA256($data:string,$secret:string):string`
- 说明： signHmacSHA256摘要算法（base64版） 
- 参数： $data:string: 要摘要的数据明文。 $secret:string: 密钥。 
- 返回： 摘要后的base64字符串

### `$vs.cipher.signHmacSHA384($data:string,$secret:string):string`
- 说明： signHmacSHA384摘要算法（base64版） 
- 参数： $data:string: 要摘要的数据明文。 $secret:string: 密钥。 
- 返回： 摘要后的base64字符串

### `$vs.cipher.signHmacSHA512($data:string,$secret:string):string`
- 说明： signHmacSHA512摘要算法（base64版） 
- 参数： $data:string: 要摘要的数据明文。 $secret:string: 密钥。 
- 返回： 摘要后的base64字符串

### `$vs.cipher.sm2decrypt($base64:string,$privatestr:string):string`
- 说明： 使用国密非对称算法用私钥对数据进行解密 
- 参数： $base64:string: 需要解密的字符串明文。 $privatestr:string: 私钥字符串。 
- 返回： 字符串明文

### `$vs.cipher.sm2encrypt($str:string,$publicstr:string):string`
- 说明： 使用国密非对称算法用公钥对数据进行加密 
- 参数： $str:string: 需要加密的字符串明文。 $publicstr:string: 公钥字符串。 
- 返回： 加密后的base64字符串

### `$vs.cipher.sm2sign($str:string,$privatestr:string):string`
- 说明： 使用国密非对称算法用私钥对数据进行签名 
- 参数： $str:string: 需要签名的字符串明文。 $privatestr:string: 私钥字符串。 
- 返回： 签名后的base64字符串

### `$vs.cipher.sm2verify($str:string,$publicstr:string,$signbase64:string):boolean`
- 说明： 使用国密非对称算法用公钥对数据进行验签 
- 参数： $str:string: 需要验证的字符串明文。 $publicstr:string: 公钥字符串。 $signbase64:string: 签名后的base64字符串。 
- 返回： 是否通过，true - 通过 false - 不通过

### `$vs.cipher.sm3encode($str:string):string`
- 说明： 使用国密对数据进行摘要（类似MD5） 
- 参数： $str:string: 需要摘要的字符串明文。 
- 返回： 摘要后的数据（64位长度16进制字符串）

### `$vs.cipher.sm4decode($cipherbase64:string,$key:string,$mode:string,$padding:string,$iv:string):string`
- 说明： 使用国密对称加密算法对数据进行解密（类似DES） 
- 参数： $cipherbase64:string: 需要解密的密文base64字符串。 $key:string: 加密秘钥（尽量16位字节长度的数据，否则会算法强制补充到16位长度）。 $mode:string: 加密模式，可选值：NONE,CBC,CFB,CTR,CTS,ECB,OFB,PCBC。 $padding:string: 补码规则，可选值：NoPadding,ZeroPadding,ISO10126Padding,OAEPPadding,PKCS1Padding,PKCS5Padding,SSL3Padding。 $iv:string: 可选，偏移量（盐）。 
- 返回： 解密后的字符串明文

### `$vs.cipher.sm4decode($cipherbase64:string,$key:string,$mode:string,$padding:string):string`
- 说明： 使用国密对称加密算法对数据进行解密（类似DES） 
- 参数： $cipherbase64:string: 需要解密的密文base64字符串。 $key:string: 加密秘钥（尽量16位字节长度的数据，否则会算法强制补充到16位长度）。 $mode:string: 加密模式，可选值：NONE,CBC,CFB,CTR,CTS,ECB,OFB,PCBC。 $padding:string: 补码规则，可选值：NoPadding,ZeroPadding,ISO10126Padding,OAEPPadding,PKCS1Padding,PKCS5Padding,SSL3Padding。 
- 返回： 解密后的字符串明文

### `$vs.cipher.sm4decode($cipherbase64:string,$key:string):string`
- 说明： 使用国密对称加密算法对数据进行解密（类似DES） 
- 参数： $cipherbase64:string: 需要解密的密文base64字符串。 $key:string: 加密秘钥（尽量16位字节长度的数据，否则会算法强制补充到16位长度）。 
- 返回： 解密后的字符串明文

### `$vs.cipher.sm4encode($str:string,$key:string,$mode:string,$padding:string,$iv:string):string`
- 说明： 使用国密对称加密算法对数据进行加密（类似DES） 
- 参数： $str:string: 需要加密的字符串明文。 $key:string: 加密秘钥（尽量16位字节长度的数据，否则会算法强制补充到16位长度）。 $mode:string: 加密模式，可选值：NONE,CBC,CFB,CTR,CTS,ECB,OFB,PCBC。 $padding:string: 补码规则，可选值：NoPadding,ZeroPadding,ISO10126Padding,OAEPPadding,PKCS1Padding,PKCS5Padding,SSL3Padding。 $iv:string: 可选，偏移量（盐）。 
- 返回： 加密后的base64字符串

### `$vs.cipher.sm4encode($str:string,$key:string,$mode:string,$padding:string):string`
- 说明： 使用国密对称加密算法对数据进行加密（类似DES） 
- 参数： $str:string: 需要加密的字符串明文。 $key:string: 加密秘钥（尽量16位字节长度的数据，否则会算法强制补充到16位长度）。 $mode:string: 加密模式，可选值：NONE,CBC,CFB,CTR,CTS,ECB,OFB,PCBC。 $padding:string: 补码规则，可选值：NoPadding,ZeroPadding,ISO10126Padding,OAEPPadding,PKCS1Padding,PKCS5Padding,SSL3Padding。 
- 返回： 加密后的base64字符串

### `$vs.cipher.sm4encode($str:string,$key:string):string`
- 说明： 使用国密对称加密算法对数据进行加密（类似DES） 
- 参数： $str:string: 需要加密的字符串明文。 $key:string: 加密秘钥（尽量16位字节长度的数据，否则会算法强制补充到16位长度）。 
- 返回： 加密后的base64字符串

### `$vs.cipher.urlDeCode($str:string,$charset:string):string`
- 说明： 对字符串进行URL解码 
- 参数： $str:string: 目标字符串。 $charset:string: 字符编码，如：GBK。 
- 返回： 处理后的字符串

### `$vs.cipher.urlDeCode($str:string):string`
- 说明： 对字符串进行URL解码 
- 参数： $str:string: 目标字符串。 
- 返回： 处理后的字符串

### `$vs.cipher.urlEnCode($str:string,$charset:string):string`
- 说明： 获取字符串的URL编码 
- 参数： $str:string: 目标字符串。 $charset:string: 字符编码，如：GBK。 
- 返回： 处理后的字符串

### `$vs.cipher.urlEnCode($str:string):string`
- 说明： 获取字符串的URL编码 
- 参数： $str:string: 目标字符串。 
- 返回： 处理后的字符串

## $vs.cookie - cookie操作对象(8 methods)

### `$vs.cookie.getCookie($cookieName:string):string`
- 说明： 获取浏览器传回的cookie值 
- 参数： $cookieName:string: cookie名称。 
- 返回： cookie值

### `$vs.cookie.removeCookie($cookieName:string,$path:string):void`
- 说明： 向浏览器发送删除cookie指令 
- 参数： $cookieName:string: cookie名称。 $path:string: cookie有路径，默认：`null`。 
- 返回： 无

### `$vs.cookie.removeCookie($cookieName:string):void`
- 说明： 向浏览器发送删除cookie指令 
- 参数： $cookieName:string: cookie名称。 
- 返回： 无

### `$vs.cookie.writeCookie($cookieName:string,$cookieValue:string,$expTime:int,$path:string):void`
- 说明： 向浏览器写入普通cookie 
- 参数： $cookieName:string: cookie名称。 $cookieValue:string: cookie值。 $expTime:int: cookie有效时间（秒)。 $path:string: cookie有路径，默认：`/`。 
- 返回： 无

### `$vs.cookie.writeCookie($cookieName:string,$cookieValue:string,$expTime:int):void`
- 说明： 向浏览器写入普通cookie 
- 参数： $cookieName:string: cookie名称。 $cookieValue:string: cookie值。 $expTime:int: cookie有效时间（秒)。 
- 返回： 无

### `$vs.cookie.writeSessionCookie($cookieName:string,$cookieValue:string,$path:string,$httpOnly:boolean):void`
- 说明： 向浏览器写入会话cookie 
- 参数： $cookieName:string: cookie名称。 $cookieValue:string: cookie值。 $path:string: cookie有路径，默认：`/`。 $httpOnly:boolean: 是否禁止JS访问，`true` - JS无法获取（默认) `false` - JS可以获取。 
- 返回： 无

### `$vs.cookie.writeSessionCookie($cookieName:string,$cookieValue:string,$path:string):void`
- 说明： 向浏览器写入会话cookie 
- 参数： $cookieName:string: cookie名称。 $cookieValue:string: cookie值。 $path:string: cookie有路径，默认：`/`。 
- 返回： 无

### `$vs.cookie.writeSessionCookie($cookieName:string,$cookieValue:string):void`
- 说明： 向浏览器写入会话cookie 
- 参数： $cookieName:string: cookie名称。 $cookieValue:string: cookie值。 
- 返回： 无

## $vs.dbTools - 数据库对象(45 methods)

### `$vs.dbTools.batchInsert($strTableName:string,$datas:List<Map<string,?>>,$isNeedDataAuth:boolean):int`
- 说明： 往表`$strTableName`中批量新增一条记录，注意：`$datas`中的所有键值必须是表`$strTableName`的字段，否则操作失败 
- 参数： $strTableName:string: 要新增记录的数据表名。 $datas:List>: 数据（`List`类型）。 $isNeedDataAuth:boolean: 是否需要数据权限控制，可选，默认true。 
- 返回： 执行SQL后变更的数据记录行数

### `$vs.dbTools.batchInsert($strTableName:string,$datas:List<Map<string,?>>):int`
- 说明： 往表`$strTableName`中批量新增一条记录（含数据权限），注意：`$datas`中的所有键值必须是表`$strTableName`的字段，否则操作失败 
- 参数： $strTableName:string: 要新增记录的数据表名。 $datas:List>: 数据（`List`类型）。 
- 返回： 执行SQL后变更的数据记录行数

### `$vs.dbTools.batchUpdate($strTableName:string,$datas:List<Map<string,?>>,$wheres:List<Map<string,?>>):int`
- 说明： 修改表`$strTableName`中符合条件的记录（不含数据权限）。 注意： 1、`$datas`和`$wheres`中的记录数、顺序必须相同（即一对数据一对条件必须匹配）； 2、`$datas`中每组的字段个数必须相同； 3、`$wheres`中每组的字段个数必须相同； 4、`$datas`中每组的字段必须是表`$strTableName`的字段，否则操作失败; 5、`$where`必须包含条件（也就是不允许全表更新），否则操作失败 
- 参数： $strTableName:string: 要更新记录的数据表名。 $datas:List >: 数据（`List `类型）。 $where:List >: 查询条件（`List`类型）。 
- 返回： 执行SQL后被修改的数据记录行数

### `$vs.dbTools.clearDatabaseCache():void`
- 说明： 清理当前线程内的MYBATIS一级缓存（一般用于需要实时读取数据库同一条记录的情况） 
- 参数： 无 
- 返回： 无

### `$vs.dbTools.connect($ip:string,$port:int,$userName:string,$pass:string,$dbType:int,$dbName:string,$instName:string):dbTools`
- 说明： 创建外数据库连接器 
- 参数： $ip:string: 数据库地址。 $port:int: 数据库端口。 $userName:string: 数据库登录用户。 $pass:string: 登录密码（明文）。 $dbType:int: 数据库类型：1 - MYSQL 2 - ORACLE 3- SQLSERVER 4 - 达梦。 $dbName:string: 数据库名。 $instName:string: 数据库实例（SQLSERVER）。 
- 返回： 远程数据库执行器

### `$vs.dbTools.connect($ip:string,$port:int,$userName:string,$pass:string,$dbType:int,$dbName:string):dbTools`
- 说明： 创建外数据库连接器 
- 参数： $ip:string: 数据库地址。 $port:int: 数据库端口。 $userName:string: 数据库登录用户。 $pass:string: 登录密码（明文）。 $dbType:int: 数据库类型：1 - MYSQL 2 - ORACLE 3- SQLSERVER 4 - 达梦。 $dbName:string: 数据库名。 
- 返回： 远程数据库执行器

### `$vs.dbTools.count($strTableName:string,$where:Map<string,?>,$isNeedDataAuth:boolean):int`
- 说明： 查询表`$strTableName`中符合条件的记录数（含数据权限） 
- 参数： $strTableName:string: 要更新记录的数据表名。 $where:Map: 查询条件（`Map`类型）。 $isNeedDataAuth:boolean: 是否需要数据权限判断，默认：true。 
- 返回： 符合条件的记录数

### `$vs.dbTools.count($strTableName:string,$where:Map<string,?>):int`
- 说明： 查询表`$strTableName`中符合条件的记录数（含数据权限） 
- 参数： $strTableName:string: 要更新记录的数据表名。 $where:Map: 查询条件（`Map`类型）。 
- 返回： 符合条件的记录数

### `$vs.dbTools.countSQL($strSql:string,$where:Map<string,?>):int`
- 说明： 执行SQL语句的统计结果 
- 参数： $strSql:string: 执行SQL，注意：只能有1个字段，如： select count(0) from table where code=#{code}。 $where:Map: 查询条件(`Map`类型)。 
- 返回： SQL执行的count结果

### `$vs.dbTools.createTempTable($strSql:string,$where:Map<string,?>,$isEnableDataAuth:boolean):string`
- 说明： 创建临时表，警告：调用本语句时，数据库会隐式发起commit操作，本语句前，所有对数据库记录的修改将自动提交，无法回滚。 
- 参数： $strSql:string: 临时表建表语句（不管当前使用的是什么数据库，此处必须使用`MYSQL`建表语法，且一次编写所有谷神支持的数据库都可使用）。 $where:Map: 查询条件(`Map`类型)。 $isEnableDataAuth:boolean: 是否启用数据权限，默认：`false`。 
- 返回： 临时表的数据库表名

### `$vs.dbTools.createTempTable($strSql:string,$where:Map<string,?>):string`
- 说明： 创建临时表，警告：调用本语句时，数据库会隐式发起commit操作，本语句前，所有对数据库记录的修改将自动提交，无法回滚。 
- 参数： $strSql:string: 临时表建表语句（不管当前使用的是什么数据库，此处必须使用`MYSQL`建表语法，且一次编写所有谷神支持的数据库都可使用）。 $where:Map: 查询条件(`Map`类型)。 
- 返回： 临时表的数据库表名

### `$vs.dbTools.createTempTable($strSql:string):string`
- 说明： 创建临时表，警告：调用本语句时，数据库会隐式发起commit操作，本语句前，所有对数据库记录的修改将自动提交，无法回滚。 
- 参数： $strSql:string: 临时表建表语句（不管当前使用的是什么数据库，此处必须使用`MYSQL`建表语法，且一次编写所有谷神支持的数据库都可使用）。 
- 返回： 临时表的数据库表名

### `$vs.dbTools.delete($strTableName:string,$where:Map<string,?>,$isNeedDataAuth:boolean):int`
- 说明： 删除表`$strTableName`中符合条件的记录（含数据权限），注意：`$where`必须包含条件（也就是不允许全表删除），否则操作失败 
- 参数： $strTableName:string: 要删除记录的数据表名。 $where:Map: 查询条件（`Map`类型）。 $isNeedDataAuth:boolean: 是否需要数据权限控制，可选，默认true。 
- 返回： 执行SQL后被删除的数据记录行数

### `$vs.dbTools.delete($strTableName:string,$where:Map<string,?>):int`
- 说明： 删除表`$strTableName`中符合条件的记录（含数据权限），注意：`$where`必须包含条件（也就是不允许全表删除），否则操作失败 
- 参数： $strTableName:string: 要删除记录的数据表名。 $where:Map: 查询条件（`Map`类型）。 
- 返回： 执行SQL后被删除的数据记录行数

### `$vs.dbTools.dropAllTempTable():void`
- 说明： 本方法已废弃，请不要使用 请使用 dropTempTable 方法 
- 参数： 无 
- 返回： 无

### `$vs.dbTools.dropTempTable($tableId:string):void`
- 说明： 删除临时表，警告：调用本语句时，数据库会隐式发起commit操作，本语句前，所有对数据库记录的修改将自动提交，无法回滚。 
- 参数： $tableId:string: 临时表ID。 
- 返回： 无

### `$vs.dbTools.execute($strSql:string,$where:Map<string,?>,$isEnableDataAuth:boolean):int`
- 说明： 执行数据库更新语句（无数据权限） 
- 参数： $strSql:string: 执行SQL。 $where:Map: 查询条件(`Map`类型)。 $isEnableDataAuth:boolean: 是否启用数据权限，默认：`false`。 
- 返回： 执行SQL后变更的数据记录行数

### `$vs.dbTools.execute($strSql:string,$where:Map<string,?>):int`
- 说明： 执行数据库更新语句（无数据权限） 
- 参数： $strSql:string: 执行SQL。 $where:Map: 查询条件(`Map`类型)。 
- 返回： 执行SQL后变更的数据记录行数

### `$vs.dbTools.executeDDL($strSql:string,$where:Map<string,?>):void`
- 说明： 执行非事务SQL语句，如：truncate、create、drop等语句。 
- 参数： $strSql:string: 执行SQL。 $where:Map: 查询条件(`Map`类型)。 
- 返回： 无

### `$vs.dbTools.findPage($sql:string,$form:Map<string,?>,$isEnableDataAuth:boolean):Page`
- 说明： 分页查询 
- 参数： $sql:string: 查询SQL语句。 $where:Map: 查询条件（`Map`类型），必须包含pageSize,pageNumber属性。 $isEnableDataAuth:boolean: 是否启用数据权限，默认：`false`。 
- 返回： 符合条件的记录数

### `$vs.dbTools.findPage($sql:string,$form:Map<string,?>):Page`
- 说明： 分页查询 
- 参数： $sql:string: 查询SQL语句。 $where:Map: 查询条件（`Map`类型），必须包含pageSize,pageNumber属性。 
- 返回： 符合条件的记录数

### `$vs.dbTools.findPage($sql:string,$where:Map<string,?>,$pageSize:int,$pageNumber:int,$isEnableDataAuth:boolean):Page`
- 说明： 分页查询 
- 参数： $sql:string: 查询SQL语句。 $where:Map: 查询条件（`Map`类型）。 $pageSize:int: 每页大小。 $pageNumber:int: 第n页（从1开始)。 $isEnableDataAuth:boolean: 是否启用数据权限，默认：`false`。 
- 返回： 符合条件的记录数

### `$vs.dbTools.findPage($sql:string,$where:Map<string,?>,$pageSize:int,$pageNumber:int):Page`
- 说明： 分页查询 
- 参数： $sql:string: 查询SQL语句。 $where:Map: 查询条件（`Map`类型）。 $pageSize:int: 每页大小。 $pageNumber:int: 第n页（从1开始)。 
- 返回： 符合条件的记录数

### `$vs.dbTools.getDbType():int`
- 说明： 获取当前运行的数据库类型 
- 参数： 无 
- 返回： 1 - MYSQL 2 - ORACLE 3 - SQLSERVER 4 - 达梦 5 - PostgreSql 6 - GAUSS 7 - 神通 8 - OceanBase 0 - 未知

### `$vs.dbTools.getDbTypeName():string`
- 说明： 获取当前运行的数据库类型名称 
- 参数： 无 
- 返回： MYSQL or ORACLE or SQLSERVER or DM or POSTGRESQL or GAUSS or SHENTONG or OCEANBASE or UNKNOWN

### `$vs.dbTools.globalTransContinue():void`
- 说明： 继续分布式事务 
- 参数： 无 
- 返回： 无

### `$vs.dbTools.globalTransPause():void`
- 说明： 暂停分布式事务 
- 参数： 无 
- 返回： 无

### `$vs.dbTools.insert($strTableName:string,$data:Map<string,?>,$isNeedDataAuth:boolean):int`
- 说明： 往表`$strTableName`中新增一条记录（含数据权限），注意：`$data`中的所有键值必须是表`$strTableName`的字段，否则操作失败 
- 参数： $strTableName:string: 要新增记录的数据表名。 $data:Map: 数据（`Map`类型）。 $isNeedDataAuth:boolean: 是否需要数据权限控制，可选，默认true。 
- 返回： 执行SQL后变更的数据记录行数

### `$vs.dbTools.insert($strTableName:string,$data:Map<string,?>):int`
- 说明： 往表`$strTableName`中新增一条记录（含数据权限），注意：`$data`中的所有键值必须是表`$strTableName`的字段，否则操作失败 
- 参数： $strTableName:string: 要新增记录的数据表名。 $data:Map: 数据（`Map`类型）。 
- 返回： 执行SQL后变更的数据记录行数

### `$vs.dbTools.isTempTableExists($tableId:string):void`
- 说明： 判断当前线程中指定的临时表是否是否已经被创建 
- 参数： $tableId:string: 临时表ID。 
- 返回： 无

### `$vs.dbTools.list($strSql:string,$where:Map<string,?>,$isEnableDataAuth:boolean):List<Map<string,?>>`
- 说明： 执行数据库查询语句（无数据权限） 
- 参数： $strSql:string: 执行SQL。 $where:Map: 查询条件(`Map`类型)。 $isEnableDataAuth:boolean: 是否启用数据权限，默认：`false`。 
- 返回： 执行SQL后获取的数据集合(`List`)类型

### `$vs.dbTools.list($strSql:string,$where:Map<string,?>):List<Map<string,?>>`
- 说明： 执行数据库查询语句（无数据权限） 
- 参数： $strSql:string: 执行SQL。 $where:Map: 查询条件(`Map`类型)。 
- 返回： 执行SQL后获取的数据集合(`List`)类型

### `$vs.dbTools.remoteFindPage($systemId:string,$strSql:string,$where:Map<string,?>,$pageSize:int,$pageNo:int,$isNeedDataAuth:boolean):Page<Map<string,?>>`
- 说明： 执行远程数据库分页查询语句 
- 参数： $systemId:string: 系统ID。 $strSql:string: 执行SQL。 $where:Map: 查询条件(`Map`类型)。 $pageSize:int: 分页大小。 $pageNo:int: 第几页。 $isNeedDataAuth:boolean: 是否启用数据权限（默认：false）。 
- 返回： 执行SQL后获取的数据集合(`Page`)类型

### `$vs.dbTools.remoteFindPage($systemId:string,$strSql:string,$where:Map<string,?>,$pageSize:int,$pageNo:int):Page<Map<string,?>>`
- 说明： 执行远程数据库分页查询语句 
- 参数： $systemId:string: 系统ID。 $strSql:string: 执行SQL。 $where:Map: 查询条件(`Map`类型)。 $pageSize:int: 分页大小。 $pageNo:int: 第几页。 
- 返回： 执行SQL后获取的数据集合(`Page`)类型

### `$vs.dbTools.remoteList($systemId:string,$strSql:string,$where:Map<string,?>,$isNeedDataAuth:boolean):List<Map<string,?>>`
- 说明： 执行远程数据库查询语句（无数据权限） 
- 参数： $systemId:string: 系统ID。 $strSql:string: 执行SQL。 $where:Map: 查询条件(`Map`类型)。 $isNeedDataAuth:boolean: 是否需要数据权限，true - 是 false - 否(默认)。 
- 返回： 执行SQL后获取的数据集合(`List`)类型

### `$vs.dbTools.remoteList($systemId:string,$strSql:string,$where:Map<string,?>):List<Map<string,?>>`
- 说明： 执行远程数据库查询语句（无数据权限） 
- 参数： $systemId:string: 系统ID。 $strSql:string: 执行SQL。 $where:Map: 查询条件(`Map`类型)。 
- 返回： 执行SQL后获取的数据集合(`List`)类型

### `$vs.dbTools.remoteUniqueResult($systemId:string,$strSql:string,$where:Map<string,?>):List<Map<string,?>>`
- 说明： 执行远程数据库查询语句，并返回单行结果集（无数据权限） 
- 参数： $systemId:string: 系统ID。 $strSql:string: 执行SQL。 $where:Map: 查询条件(`Map`类型)。 
- 返回： 执行SQL后获取的数据(`Map`)类型

### `$vs.dbTools.select($strTableName:string,$strColumns:string,$where:Map<string,?>,$isNeedDataAuth:boolean):List<Map<string,?>>`
- 说明： 查询表`$strTableName`中符合条件的记录（根据`$isNeedDataAuth`判断是否含数据权限） 
- 参数： $strTableName:string: 要查询的数据表名。 $strColumns:string: 需要查询的字段列，如：`FIIELD1,FIELD2`，您可以用‘*’来表示查询所有字段。 $where:Map: 查询条件（`Map`类型）。 $isNeedDataAuth:boolean: 是否需要数据权限判断，默认：true。 
- 返回： 执行SQL后获取的数据集合(`List`)类型

### `$vs.dbTools.select($strTableName:string,$strColumns:string,$where:Map<string,?>):List<Map<string,?>>`
- 说明： 查询表`$strTableName`中符合条件的记录（含数据权限） 
- 参数： $strTableName:string: 要查询的数据表名。 $strColumns:string: 需要查询的字段列，如：`FIIELD1,FIELD2`，您可以用‘*’来表示查询所有字段。 $where:Map: 查询条件（`Map`类型）。 
- 返回： 执行SQL后获取的数据集合(`List`)类型

### `$vs.dbTools.select($strTableName:string,$where:Map<string,?>):List<Map<string,?>>`
- 说明： 查询表`$strTableName`中符合条件的记录（含数据权限） 
- 参数： $strTableName:string: 要查询的数据表名。 $where:Map: 查询条件（`Map`类型）。 
- 返回： 执行SQL后获取的数据集合(`List`)类型

### `$vs.dbTools.selectOne($strTableName:string,$strColumns:string,$where:Map<string,?>):Map<string,?>`
- 说明： 查询表`$strTableName`中符合条件的记录（唯一返回，若返回结果大于1行则报异常） 
- 参数： $strTableName:string: 要查询的数据表名。 $strColumns:string: 需要查询的字段列，如：`FIIELD1,FIELD2`，您可以用‘*’来表示查询所有字段。 $where:Map: 查询条件（`Map`类型）。 
- 返回： 执行SQL后获取的数据

### `$vs.dbTools.selectOne($strTableName:string,$where:Map<string,?>):Map<string,?>`
- 说明： 查询表`$strTableName`中符合条件的记录（唯一返回，若返回结果大于1行则报异常） 
- 参数： $strTableName:string: 要查询的数据表名。 $where:Map: 查询条件（`Map`类型）。 
- 返回： 执行SQL后获取的数据

### `$vs.dbTools.uniqueResult($strSql:string,$where:Map<string,?>):Map<string,?>`
- 说明： 执行数据库查询语句，并返回单行结果集（无数据权限），注意：若存在多行返回则会报异常 
- 参数： $strSql:string: 执行SQL。 $where:Map: 查询条件(`Map`类型)。 
- 返回： 执行SQL后获取的数据(`Map`)类型

### `$vs.dbTools.update($strTableName:string,$data:Map<string,?>,$where:Map<string,?>,$isNeedDataAuth:boolean):int`
- 说明： 修改表`$strTableName`中符合条件的记录（含数据权限），注意：`$data`中的所有键值必须是表`$strTableName`的字段，否则操作失败;`$where`必须包含条件（也就是不允许全表更新），否则操作失败 
- 参数： $strTableName:string: 要更新记录的数据表名。 $data:Map : 数据（`Map`类型）。 $where:Map: 查询条件（`Map`类型）。 $isNeedDataAuth:boolean: 是否需要数据权限控制，可选，默认true。 
- 返回： 执行SQL后被删除的数据记录行数

### `$vs.dbTools.update($strTableName:string,$data:Map<string,?>,$where:Map<string,?>):int`
- 说明： 修改表`$strTableName`中符合条件的记录（含数据权限），注意：`$data`中的所有键值必须是表`$strTableName`的字段，否则操作失败;`$where`必须包含条件（也就是不允许全表更新），否则操作失败 
- 参数： $strTableName:string: 要更新记录的数据表名。 $data:Map : 数据（`Map`类型）。 $where:Map: 查询条件（`Map`类型）。 
- 返回： 执行SQL后被删除的数据记录行数

## $vs.date - 日期工具对象(21 methods)

### `$vs.date.dateAdd($date:date,$intAddValue:int):date`
- 说明： 对日期加（或减）天数操作 
- 参数： $date:date: 需要操作的日期。 $intAddValue:int: 需要加（或减）的天数，如：`1`表示在当前日期(`$date`)中，增加一天；`-1`表示在当前日期(`$date`)中，减少一天。 
- 返回： 转换后的日期

### `$vs.date.dateCompare($date1:date,$date2:date):int`
- 说明： 比较两个日期大小 
- 参数： $date1:date: 需要操作的日期。 $date2:date: 需要操作的日期。 
- 返回： 两个日期的大小 - 当`$date1 < $date2`时，返回`-1` - 当`$date1 = $date2`时，返回`0` - 当`$date1 > $date2`时，返回`1` - 当`$date1`或`$date2`其中有一个值为`null`时，返回`-2`

### `$vs.date.dateHourAdd($date:date,$intAddValue:int):date`
- 说明： 对日加（或减）小时操作 
- 参数： $date:date: 需要操作的日期。 $intAddValue:int: 需要加（或减）的小时数，如：`1`表示在当前日期(`$date`)中，增加一小时；`-1`表示在当前日期(`$date`)中，减少一小时。 
- 返回： 转换后的日期

### `$vs.date.dateIntervalDAY($date1:date,$date2:date):int`
- 说明： 计算两个日期间相差天数 
- 参数： $date1:date: 需要操作的日期。 $date2:date: 需要操作的日期。 
- 返回： 两个日期间相差天数 - 当`$date2`晚于`$date1`时，返回正数；当`$date2`等于`$date1`（忽略时间差异）时返回0； 否则返回负数

### `$vs.date.dateMinuteAdd($date:date,$intAddValue:int):date`
- 说明： 对日加（或减）分钟操作 
- 参数： $date:date: 需要操作的日期。 $intAddValue:int: 需要加（或减）的分钟数，如：`1`表示在当前日期(`$date`)中，增加一分钟；`-1`表示在当前日期(`$date`)中，减少一分钟。 
- 返回： 转换后的日期

### `$vs.date.dateMonthAdd($date:date,$intAddValue:int):date`
- 说明： 对日期加（或减）月操作 
- 参数： $date:date: 需要操作的日期。 $intAddValue:int: 需要加（或减）的月数，如：`1`表示在当前日期(`$date`)中，增加一月；`-1`表示在当前日期(`$date`)中，减少一月。 
- 返回： 转换后的日期

### `$vs.date.dateSecondAdd($date:date,$intAddValue:int):date`
- 说明： 对日加（或减）秒钟操作 
- 参数： $date:date: 需要操作的日期。 $intAddValue:int: 需要加（或减）的秒钟数，如：`1`表示在当前日期(`$date`)中，增加一秒钟；`-1`表示在当前日期(`$date`)中，减少一秒钟。 
- 返回： 转换后的日期

### `$vs.date.dateYearAdd($date:date,$intAddValue:int):date`
- 说明： 对日期加（或减）年操作 
- 参数： $date:date: 需要操作的日期。 $intAddValue:int: 需要加（或减）的年数，如：`1`表示在当前日期(`$date`)中，增加一年；`-1`表示在当前日期(`$date`)中，减少一年。 
- 返回： 转换后的日期

### `$vs.date.format($date:date,$format:string):string`
- 说明： 日期格式化，同：`$vs.format.formatDate(date,format)`方法 
- 参数： $date:date: 需要操作的日期。 $format:string: 日期格式，如：yyyy-MM-dd。 
- 返回： 格式化后的日期字符串

### `$vs.date.getDateWeek($date:date|string):int`
- 说明： 获取给定日期的周几 
- 参数： $date:date|string: 需要操作的日期。 
- 返回： 日期周数，0 - 周日 1 - 周一 2 - 周二 以此类推

### `$vs.date.getDbDate():date`
- 说明： 获取数据库时间（不含毫秒） 
- 参数： 无 
- 返回： 数据库当前时间

### `$vs.date.getDbTimeStamp():timestamp`
- 说明： 获取数据库时间（含毫秒） 
- 参数： 无 
- 返回： 数据库当前时间

### `$vs.date.getLocalDate():date`
- 说明： 获取应用服务器本地时间 
- 参数： 无 
- 返回： 获取应用服务器本地时间

### `$vs.date.getMonthDays($date:date|string):date`
- 说明： 获取指定日期的月份有多少天 
- 参数： $date:date|string: 需要操作的日期，`null`则返回当前月份的天数。 
- 返回： 指定日期的月份的天数

### `$vs.date.getMonthFirstDate($date:date|string):date`
- 说明： 获取指定日期的月份第一天 
- 参数： $date:date|string: 需要操作的日期，`null`则返回当前月份的第一天。 
- 返回： 指定日期的月份第一天

### `$vs.date.getMonthLastDate($date:date|string):date`
- 说明： 获取指定日期的月份最后一天 
- 参数： $date:date|string: 需要操作的日期，`null`则返回当前月份的最后一天。 
- 返回： 指定日期的月份最后一天

### `$vs.date.getTimeStamp($date:date):long`
- 说明： 获取日期的时间戳 
- 参数： $date:date: 日期。 
- 返回： 日期的时间戳

### `$vs.date.newDate($timestamp:long):date`
- 说明： 时间戳转日期 
- 参数： $timestamp:date: 日期的时间戳。 
- 返回： 转换后的日期

### `$vs.date.str2date($strDate:string,$strFmt:string):date`
- 说明： 字符串转成`$strFmt`格式的日期 
- 参数： $strDate:string: 需要转日期的字符串。 $strFmt:string: 字符串对应的日期格式，如：`yyyy-MM-dd HH:mm:ss`，可缺省。 
- 返回： 转换后的日期

### `$vs.date.str2date($strDate:string):date`
- 说明： 字符串转日期 
- 参数： $strDate:string: 需要转日期的字符串（仅支持`yyyy-MM-dd`格式的字符串）。 
- 返回： 转换后的日期

### `$vs.date.trimTimeFromDate($date:date):date`
- 说明： 去掉日期中的时间 
- 参数： $date:date: 需要操作的日期。 
- 返回： 转换后的日期

## $vs.exception - 异常类对象(1 methods)

### `$vs.exception.throwException($strMsg:string,$args...):void`
- 说明： 向用户端抛出异常提示(若当前存在事务，则会回滚事务) 
- 参数： $strMsg:string: 需要提示给用户的消息。 $args:object: 提示替换变量。 
- 返回： 无

## $vs.format - 格式化对象(4 methods)

### `$vs.format.formatDate($date:date,$strFmt:string):string`
- 说明： 格式化日期成(`$strFmt`)格式的字符串 
- 参数： $date:date: 需要格式化的日期。 $strFmt:string: 日期格式，如：yyyy-MM-dd HH:mm:ss。 
- 返回： 格式化后的字符串

### `$vs.format.formatDate($date:date):string`
- 说明： 格式化日期成默认格式(`yyyy-MM-dd`)的字符串 
- 参数： $date:date: 需要格式化的日期。 
- 返回： 格式化后的字符串

### `$vs.format.formatNumber($num:number,$strFmt:string):string`
- 说明： 格式化数字成(`$strFmt`)格式的字符串 
- 参数： $num:number: 需要格式化的数字。 $strFmt:string: 数字格式，如：#,##0.00。 
- 返回： 格式化后的字符串

### `$vs.format.numberToChinese($num:number):string`
- 说明： 数字转中文大写 
- 参数： $num:number: 需要格式化的数字。 
- 返回： 中文大写字符串

## $vs.file - 文件操作对象(55 methods)

### `$vs.file.addFileToBillAttachment($billNo:string,$billTypeCode:string,$fileName:string,$filePath:string,$extinfo:Map<string,object>):void`
- 说明： 将文件信息写到单据附件表 
- 参数： $billNo:string: 单据号码。 $billTypeCode:string: 单据类型。 $fileName:string: 文件名称（附件表显示的文件名称)。 $filePath:string: 文件路径，如：/a0c/b3e/image.png，可以是本地临时文件路径、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 $extinfo:Map: 附件业务信息（用于业务存储自定义信息，详情见单据扩展字段)。 
- 返回： 无

### `$vs.file.addFileToBillAttachment($billNo:string,$billTypeCode:string,$fileName:string,$filePath:string):void`
- 说明： 将文件信息写到单据附件表 
- 参数： $billNo:string: 单据号码。 $billTypeCode:string: 单据类型。 $fileName:string: 文件名称（附件表显示的文件名称)。 $filePath:string: 文件路径，如：/a0c/b3e/image.png，可以是本地临时文件路径、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 
- 返回： 无

### `$vs.file.batchDownload($files:List<Map<name,path>>,$fileName:string,$ignoreNotFound:boolean):void`
- 说明： 触发批量文件下载请求（注意：本方法必须在`地址映射`的服务组件下调用，JS代码可以是：`window.open(ROOT_PATH + "/gdpaas/comp/filedownload/demo.htm")`） 
- 参数： $files:List>: 要下载的文件，格式：{name:"文件名称.png",path:"/a0c/b3e/image.png"}，其中path（如：/a0c/b3e/image.png），可以是本地临时文件路径（临时文件下载完成后会自动删除）、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 $fileName:string: 文件下载时保存的文件名称，如：`批量下载文件.zip`。 $ignoreNotFound:boolean: 是否忽略不存在的文件（true - 为文件列表中，存在部分文件无法找到，则不显示错误，若所有文件都不存在则还是会报404异常； false - 默认，所有文件都必须存在，否则报异常）。 
- 返回： 无

### `$vs.file.batchDownload($files:List<Map<name,path>>,$fileName:string):void`
- 说明： 触发批量文件下载请求（注意：本方法必须在`地址映射`的服务组件下调用，JS代码可以是：`window.open(ROOT_PATH + "/gdpaas/comp/filedownload/demo.htm")`） 
- 参数： $files:List>: 要下载的文件，格式：{name:"文件名称.png",path:"/a0c/b3e/image.png"}，其中path（如：/a0c/b3e/image.png），可以是本地临时文件路径（临时文件下载完成后会自动删除）、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 $fileName:string: 文件下载时保存的文件名称，如：`批量下载文件.zip`。 
- 返回： 无

### `$vs.file.delFile($filePath:string):int`
- 说明： 删除私有区文件 
- 参数： $filePath:string: 目标文件路径，如： /upload/files/a.png。 
- 返回： 0 - 成功（含文件未找到) other 失败

### `$vs.file.delWebFile($filePath:string):int`
- 说明： 删除公有区文件 
- 参数： $filePath:string: 目标文件路径，如： /upload/files/a.png。 
- 返回： 0 - 成功（含文件未找到) other 失败

### `$vs.file.desDeCodeFile($path:string,$pass:string):string`
- 说明： 对文件内容进行解密（注意：必须是谷神 $vs.file.desEnCodeFile 生成的密文文件，否则会解密失败) 
- 参数： $path:string: 文件保存路径，如：/a0c/b3e/image.png，可以是本地临时文件路径、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 $pass:string: 加密秘钥必须是8位长度的字符串。 
- 返回： 临时文件路径，使用完成后，务必删除此文件

### `$vs.file.desEnCodeFile($path:string,$pass:string):string`
- 说明： 对文件内容进行加密 
- 参数： $path:string: 文件保存路径，如：/a0c/b3e/image.png，可以是本地临时文件路径、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 $pass:string: 加密秘钥必须是8位长度的字符串。 
- 返回： 临时文件路径，使用完成后，务必删除此文件

### `$vs.file.download($path:string,$fileName:string):void`
- 说明： 触发文件下载请求（注意：本方法必须在`地址映射`的服务组件下调用，JS代码可以是：`window.open(ROOT_PATH + "/gdpaas/comp/filedownload/demo.htm")`） 
- 参数： $path:string: 文件保存路径，如：/a0c/b3e/image.png，可以是本地临时文件路径（临时文件下载完成后会自动删除）、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 $fileName:string: [可缺省]文件下载时保存的文件名称。 
- 返回： 无

### `$vs.file.download($path:string):void`
- 说明： 触发文件下载请求（注意：本方法必须在`地址映射`的服务组件下调用，JS代码可以是：`window.open(ROOT_PATH + "/gdpaas/comp/filedownload/demo.htm")`） 
- 参数： $path:string: 文件保存路径，如：/a0c/b3e/image.png，可以是本地临时文件路径（临时文件下载完成后会自动删除）、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 
- 返回： 无

### `$vs.file.getFileBytes($path:string):byte[]`
- 说明： 读取文件内容到byte数组中 
- 参数： $path:string: 文件保存路径，如：/a0c/b3e/image.png，可以是本地临时文件路径、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 
- 返回： 文件二进制内容

### `$vs.file.getFileDownloadURL($filePath:string,$disName:string,$desKey:string):string`
- 说明： 获取私有文件下载（访问）地址，地址15天有效（视文件服务设置） 
- 参数： $filePath:string: 目标文件路径，如：/upload/files/a.png。 $disName:string: 下载时，默认的文件名称（需带扩展名)，如： `效果图.png`。 $desKey:string: 解密密文文件的秘钥。 
- 返回： 访问地址，如： http://file.gusen.com/fileservice/vfs/...

### `$vs.file.getFileDownloadURL($filePath:string,$disName:string):string`
- 说明： 获取私有文件下载（访问）地址，地址15天有效（视文件服务设置） 
- 参数： $filePath:string: 目标文件路径，如：/upload/files/a.png。 $disName:string: 下载时，默认的文件名称（需带扩展名)，如： `效果图.png`。 
- 返回： 访问地址，如： http://file.gusen.com/fileservice/vfs/...

### `$vs.file.getFileDownloadURL($filePath:string):string`
- 说明： 获取私有文件下载（访问）地址，地址15天有效（视文件服务设置） 
- 参数： $filePath:string: 目标文件路径，如：/upload/files/a.png。 
- 返回： 访问地址，如： http://file.gusen.com/fileservice/vfs/...

### `$vs.file.getFileMac($path:string):string`
- 说明： 计算文件内容摘要 
- 参数： $path:string: 文件保存路径，如：/a0c/b3e/image.png，可以是本地临时文件路径、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 
- 返回： 文件32摘要

### `$vs.file.getFileServiceURL():string`
- 说明： 获取文件服务器URL 
- 参数： 无 
- 返回： 如： http://file.gusen.com/fileservice

### `$vs.file.getFileToTemp($filePath:string):string`
- 说明： 从文件服务器上下载私有文件到本地临时服务（若无文件服务器，则从本地文件复制到临时目录），文件使用完后需要调用 `$vs.file.removeLocalTempFile($path)`删除临时文件 
- 参数： $filePath:string: 文件存储相对路径，如：/upload/AE/XX/XXXXXXX.doc。 
- 返回： 文件存储位置，如： /temp/upload/AE/XX/XXXXXXX.doc 如果文件不存在，则返回 null

### `$vs.file.getRandTempPath():string`
- 说明： 获取一个随机的临时目录 
- 参数： 无 
- 返回： 如：/temp/1232334

### `$vs.file.getServerRunPath():string`
- 说明： 获取当前服务运行根路径 
- 参数： 无 
- 返回： 如：/app/gusen/basicdata-server

### `$vs.file.getTempPath():string`
- 说明： 获取临时目录 
- 参数： 无 
- 返回： 如：/temp

### `$vs.file.getWebFileToTemp($filePath:string):string`
- 说明： 从文件服务器上下载公有文件到本地临时服务（若无文件服务器，则从本地文件复制到临时目录），文件使用完后需要调用 `$vs.file.removeLocalTempFile($path)`删除临时文件 
- 参数： $filePath:string: 文件存储相对路径，如：/upload/AE/XX/XXXXXXX.doc。 
- 返回： 文件存储位置，如： /temp/upload/AE/XX/XXXXXXX.doc 如果文件不存在，则返回 null

### `$vs.file.isDir($path:string):boolean`
- 说明： 判断一个路径是否为目录 
- 参数： $path:string: 相对路径，如：/temp/xxx。 
- 返回： 目录返回 true 不存在或者文件 返回false

### `$vs.file.isFile($path:string):boolean`
- 说明： 判断一个路径是否为文件 
- 参数： $path:string: 相对路径，如：/temp/xxx。 
- 返回： 文件返回 true 不存在或者目录 返回false

### `$vs.file.isFileExists($path:string):boolean`
- 说明： 判断一个文件或目录是否存在 
- 参数： $path:string: 相对路径，如：/temp/xxx。 
- 返回： 文件或目录是否存在

### `$vs.file.mkdirs($path:string):boolean`
- 说明： 创建目录 
- 参数： $path:string: 要创建的目录，必须是 /temp开头，如：/temp/1232334/a0c/b3e。 
- 返回： 是否成功，true - 成功

### `$vs.file.moveFile($srcFilePath:string,$targetDir:string):string`
- 说明： 移动一个文件到指定目录。 
- 参数： $srcFilePath:string: 要移动的文件（必须是本地文件，不可以是文件服务器上的，如果文件存在文件服务器上，需要先下载到本地临时目录)。 $targetDir:string: 目标目录，必须是目录，不可带文件名称。 
- 返回： 返回文件的临时相对路径，如：/temp/download/xxx.zip

### `$vs.file.parseAndSaveFileToPrivate():Map`
- 说明： 解析当前请求中用户的上传的文件，并将文件传送到文件服务器的私有文件区 
- 参数： 无 
- 返回： 文件保存信息对象

### `$vs.file.parseAndSaveFileToPrivate($fileType:string):Map`
- 说明： 解析当前请求中用户的上传的文件，并将文件传送到文件服务器的私有文件区 
- 参数： $fileType:string: 允许上传的文件类型，如： [*.log;*.mpg;*.js;*.htm;] null 表示不控制。 
- 返回： 文件保存信息对象

### `$vs.file.parseAndSaveFileToPublic():Map`
- 说明： 解析当前请求中用户的上传的文件，并将文件传送到文件服务器的公有文件区 
- 参数： 无 
- 返回： 文件保存信息对象

### `$vs.file.parseAndSaveFileToPublic($fileType:string):Map`
- 说明： 解析当前请求中用户的上传的文件，并将文件传送到文件服务器的公有文件区 
- 参数： $fileType:string: 允许上传的文件类型，如： [*.log;*.mpg;*.js;*.htm;] null 表示不控制。 
- 返回： 文件保存信息对象

### `$vs.file.putFile($localFilePath:string,$remoteFilePath:string,$desKey:string):string`
- 说明： 加密文件，并上传一个本地文件到目标服务器（私有文件区，WEB地址不可直接访问），注意：上传成功后将会自动删除临时文件，若上传失败，则请手动删除临时文件 
- 参数： $localFilePath:string: 本地文件路径（RUN_PATH/files目录下的相对路径），如: /temp/a.xlsx -> RUN_PATH/files/temp/a.xlsx。 $remoteFilePath:string: 您期望保存到文件服务器的路径，如： /upload/files/a.xlsx。 $desKey:string: 对文件进行加密的秘钥，null 表示不加密。 
- 返回： 返回文件在目标服务器保存的路径，如：`${removeFilePath}` ； 若失败，则返回null

### `$vs.file.putFile($localFilePath:string,$remoteFilePath:string):string`
- 说明： 上传一个本地文件到目标服务器（私有文件区，WEB地址不可直接访问），注意：上传成功后将会自动删除临时文件，若上传失败，则请手动删除临时文件 
- 参数： $localFilePath:string: 本地文件路径（RUN_PATH/files目录下的相对路径），如: /temp/a.xlsx -> RUN_PATH/files/temp/a.xlsx。 $remoteFilePath:string: 您期望保存到文件服务器的路径，如： /upload/files/a.xlsx。 
- 返回： 返回文件在目标服务器保存的路径，如：`${removeFilePath}` ； 若失败，则返回null

### `$vs.file.putFile($localFilePath:string):string`
- 说明： 上传一个本地文件到目标服务器（私有文件区，WEB地址不可直接访问），注意：上传成功后将会自动删除临时文件，若上传失败，则请手动删除临时文件 
- 参数： $localFilePath:string: 本地文件路径（RUN_PATH/files目录下的相对路径），如: /temp/a.xlsx -> RUN_PATH/files/temp/a.xlsx。 
- 返回： 返回文件在目标服务器保存的路径，如：/upload/E9/33/62/BEE329EB1283C3BC79824E04F7.xlsx ； 若失败，则返回null

### `$vs.file.putWebFile($localFilePath:string,$remoteFilePath:string):string`
- 说明： 上传一个本地文件到目标服务器（公有文件区，WEB地址可以直接访问），注意：上传成功后将会自动删除临时文件，若上传失败，则请手动删除临时文件 
- 参数： $localFilePath:string: 本地文件路径（RUN_PATH/files目录下的相对路径），如: /temp/a.xlsx -> RUN_PATH/files/temp/a.xlsx。 $remoteFilePath:string: 您期望保存到文件服务器的路径，如： /upload/files/a.xlsx。 
- 返回： 返回文件在目标服务器保存的路径，如：`${removeFilePath}` ； 若失败，则返回null

### `$vs.file.putWebFile($localFilePath:string):string`
- 说明： 上传一个本地文件到目标服务器（公有文件区，WEB地址可以直接访问），注意：上传成功后将会自动删除临时文件，若上传失败，则请手动删除临时文件 
- 参数： $localFilePath:string: 本地文件路径（RUN_PATH/files目录下的相对路径），如: /temp/a.xlsx -> RUN_PATH/files/temp/a.xlsx。 
- 返回： 返回文件在目标服务器保存的路径，如：/upload/E9/33/62/BEE329EB1283C3BC79824E04F7.xlsx ； 若失败，则返回null

### `$vs.file.putWebImage($localFilePath:string,$remoteFilePath:string):string`
- 说明： 上传一个本地图片到目标服务器（公有文件区，WEB地址可以直接访问），并生成（中小）2张缩略图，注意：上传成功后将会自动删除临时文件，若上传失败，则请手动删除临时文件 
- 参数： $localFilePath:string: 本地文件路径（RUN_PATH/files目录下的相对路径），如: /temp/a.png -> RUN_PATH/files/temp/a.png。 $remoteFilePath:string: 您期望保存到文件服务器的路径，如： /upload/files/a.xlsx。 
- 返回： 返回文件在目标服务器保存的路径，如：`${removeFilePath}` ； 若失败，则返回null

### `$vs.file.putWebImage($localFilePath:string):string`
- 说明： 上传一个本地图片到目标服务器（公有文件区，WEB地址可以直接访问），并生成（中小）2张缩略图，注意：上传成功后将会自动删除临时文件，若上传失败，则请手动删除临时文件 
- 参数： $localFilePath:string: 本地文件路径（RUN_PATH/files目录下的相对路径），如: /temp/a.png -> RUN_PATH/files/temp/a.png。 
- 返回： 返回文件在目标服务器保存的路径，如：/upload/E9/33/62/BEE329EB1283C3BC79824E04F7.png ； 若失败，则返回null

### `$vs.file.readCsvFile($strFilePath:string,$charset:string):List<CsvRow>`
- 说明： 读取Csv文件 
- 参数： $strFilePath:string: Excel文件保存的服务器相对路径。 $charset:string: 文件字符编码，如： UTF-8、GBK、GB2312。 
- 返回： Csv的集合（第一行数据为标题)

### `$vs.file.readCsvFile($strFilePath:string):List<CsvRow>`
- 说明： 读取Excel文件 
- 参数： $strFilePath:string: Excel文件保存的服务器相对路径。 
- 返回： Csv的集合（第一行数据为标题)

### `$vs.file.readExcelFile($strFilePath:string,$dataStartRowNo:int):List<Sheet>`
- 说明： 读取Excel文件 
- 参数： $strFilePath:string: Excel文件保存的服务器相对路径。 $dataStartRowNo:int: 数据开始行，默认1，（0为标题行，1数据开始行），若存在特殊Excel模版第一行不是标题行，则请设置此参数。 
- 返回： Excel的Sheet集合

### `$vs.file.readExcelFile($strFilePath:string):List<Sheet>`
- 说明： 读取Excel文件 
- 参数： $strFilePath:string: Excel文件保存的服务器相对路径。 
- 返回： Excel的Sheet集合

### `$vs.file.readExcelFileSheet($strFilePath:string,$sheetNo:int,$dataStartRowNo:int):Sheet`
- 说明： 读取Excel文件 
- 参数： $strFilePath:string: Excel文件保存的服务器相对路径。 $sheetNo:int: sheet号，从1开始。 $dataStartRowNo:int: 数据开始行，默认1，（0为标题行，1数据开始行），若存在特殊Excel模版第一行不是标题行，则请设置此参数。 
- 返回： Excel的Sheet

### `$vs.file.readExcelFileSheet($strFilePath:string,$sheetNo:int):Sheet`
- 说明： 读取Excel文件 
- 参数： $strFilePath:string: Excel文件保存的服务器相对路径。 $sheetNo:int: sheet号，从1开始。 
- 返回： Excel的Sheet

### `$vs.file.readFreeExcelFile($strFilePath:string,$dataStartRowNo:int):List<Sheet>`
- 说明： 读取自由格式的Excel文件 
- 参数： $strFilePath:string: Excel文件保存的服务器相对路径。 $dataStartRowNo:int: 数据开始行，默认1，（0为标题行，1数据开始行），若存在特殊Excel模版第一行不是标题行，则请设置此参数。 
- 返回： Excel的Sheet集合

### `$vs.file.readFreeExcelFile($strFilePath:string):List<Sheet>`
- 说明： 读取自由格式的Excel文件 
- 参数： $strFilePath:string: Excel文件保存的服务器相对路径。 
- 返回： Excel的Sheet集合

### `$vs.file.readFreeExcelFileSheet($strFilePath:string,$sheetNo:int,$dataStartRowNo:int):Sheet`
- 说明： 读取自由格式的Excel文件 
- 参数： $strFilePath:string: Excel文件保存的服务器相对路径。 $sheetNo:int: sheet号，从1开始。 $dataStartRowNo:int: 数据开始行，默认1，（0为标题行，1数据开始行），若存在特殊Excel模版第一行不是标题行，则请设置此参数。 
- 返回： Excel的Sheet

### `$vs.file.readFreeExcelFileSheet($strFilePath:string,$sheetNo:int):Sheet`
- 说明： 读取自由格式的Excel文件 
- 参数： $strFilePath:string: Excel文件保存的服务器相对路径。 $sheetNo:int: sheet号，从1开始。 
- 返回： Excel的Sheet

### `$vs.file.removeLocalTempDir($filePath:string):boolean`
- 说明： 删除本地临时目录（递归删除目录下所有文件及子目录） 
- 参数： $filePath:string: 目标文件路径必须以 /temp/ 开头，如： /temp/upload。 
- 返回： true - 成功（含文件未找到) false 失败

### `$vs.file.removeLocalTempFile($filePath:string):int`
- 说明： 删除本地临时目录文件 
- 参数： $filePath:string: 要删除的文件路径及名称，必须以 /temp/ 开头，/temp/a.png -> RUN_PATH/files/temp/a.png。 
- 返回： 0 - 成功（含文件未找到) other 失败

### `$vs.file.rename($filePath:string,$newName:string):boolean`
- 说明： 修改一个文件的名称。 
- 参数： $filePath:string: 要修改的文件（必须是本地文件，不可以是文件服务器上的，如果文件存在文件服务器上，需要先下载到本地临时目录)。 $newName:string: 新文件名称，如： newFileName.png 。 
- 返回： true - 成功 false - 文件不存在或修改失败

### `$vs.file.saveBytesToFile($fileName:string,$buffer:byte[]):string`
- 说明： 保存二进制内容到文件 
- 参数： $fileName:string: 要保存的文件名称及路径，如：/a0c/b3e/image.png。 $buffer:byte[]: 要保存到文件的二进制内容。 
- 返回： 文件保存路径，如：/temp/a0c/b3e/image.png

### `$vs.file.saveStringToFile($fileName:string,$context:string):string`
- 说明： 保存字符串内容到文件 
- 参数： $fileName:string: 要保存的文件名称及路径，如：/a0c/b3e/file.txt。 $context:string: 要保存到文件的字符串内容。 
- 返回： 文件保存路径，如：/temp/a0c/b3e/file.txt

### `$vs.file.unzip($zipFile:string):Map<string,Object>`
- 说明： 解压缩一个文件并返回解压后的目录结构。 
- 参数： $zipFile:string: 要解压缩的文件，如：/a0c/b3e/image.zip，可以是本地临时文件路径、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 
- 返回： 目录结构

### `$vs.file.zipDir($dirPath:string):string`
- 说明： 压缩一个目录并返回压缩文件的相对路径。 
- 参数： $dirPath:string: 文件夹路径，必须以 /temp 目录开头，如：通过 $vs.file.mkdirs("/temp/download/xxx")。 
- 返回： 返回压缩文件的临时相对路径，如：/temp/download/xxx.zip

### `$vs.file.zipFile($path:string):string`
- 说明： 压缩一个文件（注意不是目录）并返回压缩文件的相对路径。 
- 参数： $path:string: 文件保存路径，如：/a0c/b3e/image.png，可以是本地临时文件路径（临时文件下载完成后会自动删除）、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 
- 返回： 返回压缩文件的临时相对路径，如：/temp/xxxxx/xxxx.zip

## $vs.http - HTTP请求对象(32 methods)

### `$vs.http.formPost($url:string,$param:Map,$header:Map,$ignoreError:boolean):byte []`
- 说明： 表单提交的方式POST到目标URL 
- 参数： $url:string: 服务器全地址。 $param:object: 请求参数，可为`null`。 $header:object: 请求头，可以为`null`。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 目标服务器返回的二进制数组

### `$vs.http.formPost($url:string,$param:Map,$header:Map):byte []`
- 说明： 表单提交的方式POST到目标URL 
- 参数： $url:string: 服务器全地址。 $param:object: 请求参数，可为`null`。 $header:object: 请求头，可以为`null`。 
- 返回： 目标服务器返回的二进制数组

### `$vs.http.formPost($url:string,$param:Map):byte []`
- 说明： 表单提交的方式POST到目标URL 
- 参数： $url:string: 服务器全地址。 $param:object: 请求参数，可为`null`。 
- 返回： 目标服务器返回的二进制数组

### `$vs.http.formPostWithStringReturn($url:string,$param:Map,$header:Map,$ignoreError:boolean):string`
- 说明： 表单提交的方式POST到目标URL 
- 参数： $url:string: 服务器全地址。 $param:object: 请求参数，可为`null`。 $header:object: 请求头，可以为`null`。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 目标服务器返回的字符串

### `$vs.http.formPostWithStringReturn($url:string,$param:Map,$header:Map):string`
- 说明： 表单提交的方式POST到目标URL 
- 参数： $url:string: 服务器全地址。 $param:object: 请求参数，可为`null`。 $header:object: 请求头，可以为`null`。 
- 返回： 目标服务器返回的字符串

### `$vs.http.formPostWithStringReturn($url:string,$param:Map):string`
- 说明： 表单提交的方式POST到目标URL 
- 参数： $url:string: 服务器全地址。 $param:object: 请求参数，可为`null`。 
- 返回： 目标服务器返回的字符串

### `$vs.http.getClientIp():string`
- 说明： 获取客户端浏览器IP 
- 参数： 无 
- 返回： 客户端IP

### `$vs.http.getWithByteArrayReturn($url:string,$params:Map,$encode:string,$contextType:string,$header:Map,$ignoreError:boolean):byte[]`
- 说明： GET获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $params:Map: 请求参数。 $encode:string: 请求字符编码，默认UTF8。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded。 $header:Map: 请求头信息。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 返回字节数组

### `$vs.http.getWithListReturn($url:string,$params:Map,$encode:string,$contextType:string,$header:Map,$ignoreError:boolean):List`
- 说明： GET获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $params:Map: 请求参数。 $encode:string: 请求字符编码，默认UTF8。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded。 $header:Map: 请求头信息。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 返回数组对象

### `$vs.http.getWithMapReturn($url:string,$params:Map,$encode:string,$contextType:string,$header:Map,$ignoreError:boolean):Map`
- 说明： GET获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $params:Map: 请求参数。 $encode:string: 请求字符编码，默认UTF8。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded。 $header:Map: 请求头信息。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 返回对象

### `$vs.http.getWithStringReturn($url:string,$params:Map,$encode:string,$contextType:string,$header:Map,$ignoreError:boolean):string`
- 说明： GET获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $params:Map: 请求参数。 $encode:string: 请求字符编码，默认UTF8。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded。 $header:Map: 请求头信息。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 返回的字符串

### `$vs.http.postBodyWithByteArrayReturn($url:string,$buffer:object,$encode:string,$contextType:string,$header:Map,$ignoreError:boolean):byte[]`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $buffer:object: 请求内容。 $encode:string: 请求字符编码，默认UTF8。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded。 $header:Map: 请求头信息。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 返回字节数组

### `$vs.http.postBodyWithListReturn($url:string,$buffer:object,$encode:string,$contextType:string,$header:Map,$ignoreError:boolean):List`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $buffer:object: 请求内容。 $encode:string: 请求字符编码，默认UTF8。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded。 $header:Map: 请求头信息。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 返回对象列表

### `$vs.http.postBodyWithMapReturn($url:string,$buffer:object,$encode:string,$contextType:string,$header:Map,$ignoreError:boolean):Map`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $buffer:object: 请求内容。 $encode:string: 请求字符编码，默认UTF8。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded。 $header:Map: 请求头信息。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 返回对象

### `$vs.http.postBodyWithStringReturn($url:string,$buffer:object,$encode:string,$contextType:string,$header:Map,$ignoreError:boolean):string`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $buffer:object: 请求内容。 $encode:string: 请求字符编码，默认UTF8。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded。 $header:Map: 请求头信息。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 返回字符串

### `$vs.http.postBuffer($url:string,$buffer:byte[],$encode:string,$contextType:string,$header:Map,$ignoreError:boolean,$responseHeaders:Map):byte[]`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址，可带参数，如： http://www.123.com?a=1。 $buffer:byte[]: 请求参数。 $encode:string: 请求字符编码，默认UTF8。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded。 $header:Map : 请求头信息。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 $responseHeaders:Map: 输出型变量，当此对象非空时，框架会把目标返回的应答头信息填值到此对象中。 
- 返回： 返回字节数组

### `$vs.http.postByteBodyWithByteArrayReturn($url:string,$buffer:byte[],$encode:string,$contextType:string,$header:Map,$ignoreError:boolean):byte[]`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $buffer:byte[]: 请求内容。 $encode:string: 请求字符编码。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded。 $header:Map: 请求头信息。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 返回字节数组

### `$vs.http.postFile($url:string,$param:Map,$fileKey:string,$fileName:string,$localFilePath:string,$header:Map):string`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $param:object: 请求参数，可为`null`。 $fileKey:string: 文件参数KEY值（一般需要根据对方服务器的约定）。 $fileName:string: 文件名称。 $localFilePath:string: 文件存储路径，如：/temp/a.xlsx，自动查找识别，顺序为：本地、私有、公有。 $header:Map: 请求头信息（可缺省）。 
- 返回： 目标服务器返回的信息字符串

### `$vs.http.postFile($url:string,$param:Map,$fileKey:string,$fileName:string,$localFilePath:string):string`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $param:object: 请求参数，可为`null`。 $fileKey:string: 文件参数KEY值（一般需要根据对方服务器的约定）。 $fileName:string: 文件名称。 $localFilePath:string: 文件存储路径，如：/temp/a.xlsx，自动查找识别，顺序为：本地、私有、公有。 
- 返回： 目标服务器返回的信息字符串

### `$vs.http.postFileBuffer($url:string,$param:Map,$fileKey:string,$fileName:string,$buffer:byte[],$header:Map):string`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $param:object: 请求参数，可为`null`。 $fileKey:string: 文件参数KEY值（一般需要根据对方服务器的约定）。 $fileName:string: 文件名称。 $buffer:byte[]: 文件内容字节数组。 $header:Map: 请求头信息（可缺省）。 
- 返回： 目标服务器返回的信息字符串

### `$vs.http.postFileBuffer($url:string,$param:Map,$fileKey:string,$fileName:string,$buffer:byte[]):string`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $param:object: 请求参数，可为`null`。 $fileKey:string: 文件参数KEY值（一般需要根据对方服务器的约定）。 $fileName:string: 文件名称。 $buffer:byte[]: 文件内容字节数组。 
- 返回： 目标服务器返回的信息字符串

### `$vs.http.postParams($url:string,$param:Map,$encode:string,$contextType:string,$header:Map,$ignoreError:boolean,$responseHeaders:Map):byte[]`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址，可带参数，如： http://www.123.com?a=1。 $param:Map: 请求参数。 $encode:string: 请求字符编码，默认UTF8。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded。 $header:Map : 请求头信息。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 $responseHeaders:Map: 输出型变量，当此对象非空时，框架会把目标返回的应答头信息填值到此对象中。 
- 返回： 返回字节数组

### `$vs.http.postWithByteArrayReturn($url:string,$params:Map,$encode:string,$contextType:string,$header:Map,$ignoreError:boolean):byte[]`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $params:Map: 请求参数。 $encode:string: 请求字符编码，默认UTF8。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded。 $header:Map: 请求头信息。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 返回字节数组

### `$vs.http.postWithListReturn($url:string,$params:Map,$encode:string,$contextType:string,$header:Map,$ignoreError:boolean):List`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $params:Map: 请求参数。 $encode:string: 请求字符编码，默认UTF8。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded。 $header:Map: 请求头信息。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 返回数组对象

### `$vs.http.postWithMapReturn($url:string,$params:Map,$encode:string,$contextType:string,$header:Map,$ignoreError:boolean):Map`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $params:Map: 请求参数。 $encode:string: 请求字符编码，默认UTF8。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded。 $header:Map: 请求头信息。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 返回对象

### `$vs.http.postWithStringReturn($url:string,$params:Map,$encode:string,$contextType:string,$header:Map,$ignoreError:boolean):string`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址。 $params:Map: 请求参数。 $encode:string: 请求字符编码，默认UTF8。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded。 $header:Map: 请求头信息。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 返回的字符串

### `$vs.http.request($url:string,$method:string,$buffer:byte[],$encode:string,$contextType:string,$header:Map,$ignoreError:boolean):byte[]`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址，可带参数，如： http://www.123.com?a=1。 $method:string: 请求类型，如：GET、POST、DELTE、PUT等。 $buffer:byte[]: 请求内容（可为null）。 $encode:string: 请求字符编码，默认：UTF-8，可为null。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded,可为null。 $header:Map: 请求头信息，可为null。 $ignoreError:boolean: 忽略服务器返回的错误码。默认`false`（返回码超过400就会抛出异常），`true` - 不管服务端返回什么码，都会读取服务端返回的数据不会抛出异常，需要开发者自行解析请求是否正确。 
- 返回： 返回字节数组

### `$vs.http.request($url:string,$method:string,$buffer:byte[],$encode:string,$contextType:string,$header:Map):byte[]`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址，可带参数，如： http://www.123.com?a=1。 $method:string: 请求类型，如：GET、POST、DELTE、PUT等。 $buffer:byte[]: 请求内容（可为null）。 $encode:string: 请求字符编码，默认：UTF-8，可为null。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded,可为null。 $header:Map: 请求头信息，可为null。 
- 返回： 返回字节数组

### `$vs.http.request($url:string,$method:string,$buffer:byte[],$encode:string,$contextType:string):byte[]`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址，可带参数，如： http://www.123.com?a=1。 $method:string: 请求类型，如：GET、POST、DELTE、PUT等。 $buffer:byte[]: 请求内容（可为null）。 $encode:string: 请求字符编码，默认：UTF-8，可为null。 $contextType:string: 请求头类型，默认：application/x-www-form-urlencoded,可为null。 
- 返回： 返回字节数组

### `$vs.http.request($url:string,$method:string,$buffer:byte[],$encode:string):byte[]`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址，可带参数，如： http://www.123.com?a=1。 $method:string: 请求类型，如：GET、POST、DELTE、PUT等。 $buffer:byte[]: 请求内容（可为null）。 $encode:string: 请求字符编码，默认：UTF-8，可为null。 
- 返回： 返回字节数组

### `$vs.http.request($url:string,$method:string,$buffer:byte[]):byte[]`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址，可带参数，如： http://www.123.com?a=1。 $method:string: 请求类型，如：GET、POST、DELTE、PUT等。 $buffer:byte[]: 请求内容（可为null）。 
- 返回： 返回字节数组

### `$vs.http.request($url:string,$method:string):byte[]`
- 说明： POST获取目标URL的数据 
- 参数： $url:string: 服务器全地址，可带参数，如： http://www.123.com?a=1。 $method:string: 请求类型，如：GET、POST、DELTE、PUT等。 
- 返回： 返回字节数组

## $vs.log - 日志类对象(6 methods)

### `$vs.log.error($obj:object,$args:object...):void`
- 说明： 向服务控制台输出`ERROR`级别的日志信息 
- 参数： $obj:object: 需要输出的对象。 $args:object...: 变长参数，用于字符串替换，如：$vs.log.error("hello [{}][{}]", $name1, $name2)。 
- 返回： 无

### `$vs.log.error($obj:object):void`
- 说明： 向服务控制台输出`ERROR`级别的日志信息 
- 参数： $obj:object: 需要输出的对象。 
- 返回： 无

### `$vs.log.info($obj:object,$args:object...):void`
- 说明： 向服务控制台输出`INFO`级别的日志信息 
- 参数： $obj:object: 需要输出的对象。 $args:object...: 变长参数，用于字符串替换，如：$vs.log.info("hello [{}][{}]", $name1, $name2)。 
- 返回： 无

### `$vs.log.info($obj:object):void`
- 说明： 向服务控制台输出`INFO`级别的日志信息 
- 参数： $obj:object: 需要输出的对象。 
- 返回： 无

### `$vs.log.writeBusLog($billTypeCode:string,$billNo:string,$optType:string,$bill:object,$systemId:string):void`
- 说明： 记录业务日志 
- 参数： $billTypeCode:string: 必须且非空，业务单据类型，如：BT0001。 $billNo:string: 必须且非空，当前发生的业务单据号，如：HT202109180002。 $optType:string: 必须且非空，当前发生的业务类型，如：审核 or audit。 $bill:object: 必须且非空，当前发生的业务数据，可以是字符串也可以是对象，若为对象，则自动转换为json字符串。 $systemId:string: 系统编码，可缺省，默认当前系统编码。 
- 返回： 无

### `$vs.log.writeBusLog($billTypeCode:string,$billNo:string,$optType:string,$bill:object):void`
- 说明： 记录业务日志 
- 参数： $billTypeCode:string: 必须且非空，业务单据类型，如：BT0001。 $billNo:string: 必须且非空，当前发生的业务单据号，如：HT202109180002。 $optType:string: 必须且非空，当前发生的业务类型，如：审核 or audit。 $bill:object: 必须且非空，当前发生的业务数据，可以是字符串也可以是对象，若为对象，则自动转换为json字符串。 
- 返回： 无

## $vs.mail - 邮件发送对象(3 methods)

### `$vs.mail.createMailService():mailService`
- 说明： 创建高级邮件发送服务 
- 参数： 无 
- 返回： 邮件发送服务

### `$vs.mail.sendSimpleMail($mailTitle:string,$context:string,$revicerMails:string...):int`
- 说明： 发送普通邮件 
- 参数： $mailTitle:string: 邮件标题。 $context:string: 邮件内容（支持HTML）。 $revicerMails:string...: 邮件接收者（支持多个参数）。 
- 返回： 0 - 成功 other 失败

### `$vs.mail.sendTemplateMail($msgTypeId:string,$bill:object,$revicerMails:string...):int`
- 说明： 发送普通模版邮件 
- 参数： $msgTypeId:string: 邮件模版编码。 $bill:object: 邮件模版变量对象。 $revicerMails:string...: 邮件接收者（支持多个参数）。 
- 返回： 0 - 成功 other 失败

## $vs.math - 数学方法对象(19 methods)

### `$vs.math.abs($d:double):double`
- 说明： 计算绝对值 
- 参数： $d:double: 数值。 
- 返回： 绝对值

### `$vs.math.acos($d:double):double`
- 说明： acos 
- 参数： $d:double: 。 
- 返回： acos值

### `$vs.math.asin($d:double):double`
- 说明： asin 
- 参数： $d:double: 。 
- 返回： asin值

### `$vs.math.cbrt($d:double):double`
- 说明： 计算立方根 cbrt(8) = 2.0 
- 参数： $d:double: 数值。 
- 返回： 立方根

### `$vs.math.ceil($d:double):int`
- 说明： 计算最接近给定值的最大整数 
- 参数： $d:double: 数值。 
- 返回： 最大整数

### `$vs.math.cos($d:double):double`
- 说明： cos 
- 参数： $d:double: 。 
- 返回： cos值

### `$vs.math.floor($d:double):int`
- 说明： 计算最接近给定值的最小整数 
- 参数： $d:double: 数值。 
- 返回： 最小整数

### `$vs.math.max($d:double,$dn:double...):double`
- 说明： 再给定的数字中，返回最大的一个数字 
- 参数： $d:double: 数字。 $d2:double: 数字。 $dn:double...: 数字，这里可以是0-n个参数。 
- 返回： 最大的数字

### `$vs.math.min($d:double,$dn:double...):double`
- 说明： 再给定的数字中，返回最小的一个数字 
- 参数： $d:double: 数字。 $d2:double: 数字。 $dn:double...: 数字，这里可以是0-n个参数。 
- 返回： 最小的数字

### `$vs.math.mod($a:int,$b:int):int`
- 说明： 取余数 
- 参数： $a:int: 。 $b:int: 。 
- 返回： $a % $b

### `$vs.math.pow($d:double,$x:int):double`
- 说明： 计算X次方 
- 参数： $d:double: 数值。 $x:int: 次方数。 
- 返回： X次方值

### `$vs.math.precise($num1:number,$num2:number,$stropt:string,$intScale:int):double`
- 说明： 数字‘+’、‘-’、‘*’、‘/’运算，功能同：`$vs.util.precise` 
- 参数： $num1:number: 被操作数，注意：若数值为`null`，则视为`0`。 $num2:number: 操作数，注意：若数值为`null`，则视为`0`。 $stropt:string: 运算符，须：‘+’、‘-’、‘*’、‘/’之一。 $intScale:int: 期望保留的小数位，仅‘*’、‘/’有效。 
- 返回： 运算后的数字

### `$vs.math.precise($num1:number,$num2:number,$stropt:string):double`
- 说明： 数字‘+’、‘-’、‘*’、‘/’运算，功能同：`$vs.util.precise` 
- 参数： $num1:number: 被操作数，注意：若数值为`null`，则视为`0`。 $num2:number: 操作数，注意：若数值为`null`，则视为`0`。 $stropt:string: 运算符，须：‘+’、‘-’、‘*’、‘/’之一。 
- 返回： 运算后的数字

### `$vs.math.random():double`
- 说明： 获取 0 - 1 的随机数 
- 参数： 无 
- 返回： 随机数

### `$vs.math.random($max:int):int`
- 说明： 返回 0 - ($max - 1)的整数 
- 参数： $max:double: 最大值。 
- 返回： 随机数

### `$vs.math.sin($d:double):double`
- 说明： sin 
- 参数： $d:double: 。 
- 返回： sin值

### `$vs.math.sqrt($d:double):double`
- 说明： 计算平方根 sqrt(16) = 4.0 
- 参数： $d:double: 数值。 
- 返回： 平方根

### `$vs.math.toDegrees($d:double):double`
- 说明： toDegrees 
- 参数： $d:double: 。 
- 返回： toDegrees值

### `$vs.math.toRadians($d:double):double`
- 说明： toRadians 
- 参数： $d:double: 。 
- 返回： toRadians值

## $vs.message - 消息通知对象(22 methods)

### `$vs.message.buildMessageContext($userId:string,$msgTypeId:string,$bill:object,$systemId:string):string`
- 说明： 编译并返回消息模版内容 
- 参数： $userId:string: 操作员用户编码。 $msgTypeId:string: 消息模版编码。 $bill:object: 单据内容（用于产生消息通知信息)。 $systemId:string: 操作员所属的系统编码。 
- 返回： 编译后的消息模版内容

### `$vs.message.buildMessageContext($userId:string,$msgTypeId:string,$bill:object):string`
- 说明： 编译并返回消息模版内容 
- 参数： $userId:string: 操作员用户编码。 $msgTypeId:string: 消息模版编码。 $bill:object: 单据内容（用于产生消息通知信息)。 
- 返回： 编译后的消息模版内容

### `$vs.message.buildMessageTitle($userId:string,$msgTypeId:string,$bill:object,$systemId:string):string`
- 说明： 编译并返回消息模版标题 
- 参数： $userId:string: 操作员用户编码。 $msgTypeId:string: 消息模版编码。 $bill:object: 单据内容（用于产生消息通知信息)。 $systemId:string: 操作员所属的系统编码。 
- 返回： 编译后的消息模版标题

### `$vs.message.buildMessageTitle($userId:string,$msgTypeId:string,$bill:object):string`
- 说明： 编译并返回消息模版标题 
- 参数： $userId:string: 操作员用户编码。 $msgTypeId:string: 消息模版编码。 $bill:object: 单据内容（用于产生消息通知信息)。 
- 返回： 编译后的消息模版标题

### `$vs.message.createCalendarNotice($userId:string,$theme:string,$startDate:string,$endDate:string,$content:string,$promptTime:int,$detailUrl:string):string`
- 说明： 新建日程消息 
- 参数： $userId:string: 接收者标识（必须），如：手机号，用于记录谁的日程消息，任意值不超过50字节长度。 $theme:string: 日程主题（必须），任意值不超过50字节长度。 $startDate:string: 日程开始时间（必须），格式 yyyy-MM-dd。 $endDate:string: 日程结束时间（必须），格式 yyyy-MM-dd。 $content:string: 日程描述（必须），任意值不超过150字节长度。 $promptTime:int: 提醒时间（必须），取值范围（-1不提醒 ；0-当天；1-1天前；2-2天前）。 $detailUrl:string: 日程链接，任意值不超过100字节长度。 
- 返回： 返回消息发送状态，'success' - 成功 other 失败信息

### `$vs.message.removeCalendarNotice($userId:string,$noticeId:long):string`
- 说明： 新建日程消息 
- 参数： $userId:string: 接收者标识（必须），如：手机号，用于记录谁的日程消息，任意值不超过50字节长度。 $noticeId:long: 日程ID（必须）。 
- 返回： 返回消息发送状态，'success' - 成功 other 失败信息

### `$vs.message.sendAdvanceMessage($userId:string,$msgTypeId:string,$context:string,$param:string|Map,$systemId:string):int`
- 说明： 发送一个基于消息模版的消息给用户 
- 参数： $userId:string: 操作员用户编码。 $msgTypeId:string: 消息模版编码。 $context:string: 消息内容（500字节内)。 $param:object: 用于打开关联窗口时，传递给窗口的参数。 $systemId:string: 操作员所属的系统编码。 
- 返回： 0 - 未发送（用户不存在？消息未启用？或者其他错误） 1 - 发送成功

### `$vs.message.sendAdvanceMessage($userId:string,$msgTypeId:string,$context:string,$param:string|Map):int`
- 说明： 发送一个基于消息模版的消息给用户 
- 参数： $userId:string: 操作员用户编码。 $msgTypeId:string: 消息模版编码。 $context:string: 消息内容（500字节内)。 $param:object: 用于打开关联窗口时，传递给窗口的参数。 
- 返回： 0 - 未发送（用户不存在？消息未启用？或者其他错误） 1 - 发送成功

### `$vs.message.sendCropWxMessage($userId:string,$userName:string,$openId:string,$msgTypeId:string,$bill:object,$extitems:Map<string,object>):int`
- 说明： 发送微信企业号消息给指定人（不是系统内的人，站内信不发） 
- 参数： $userId:string: 接收者标识（必须），如：手机号，用于记录发送日志，任意值不超过50字节长度。 $userName:string: 接收者姓名（必须），用于记录发送日志，任意值不超过50字节长度。 $openId:string: 接收者企业微信openId。 $msgTypeId:string: 消息模版编码。 $bill:object: 单据内容（用于产生消息通知信息)。 $extitems:Map: 可选（允许为`null`），自定义消息项（钉钉和企业微信有效），允许开发者自定义消息项目。 
- 返回： 返回消息发送状态，0 - 成功 1 - 消息模版被禁用 other 失败

### `$vs.message.sendCropWxMessage($userId:string,$userName:string,$openId:string,$msgTypeId:string,$bill:object):int`
- 说明： 发送微信企业号消息给指定人（不是系统内的人，站内信不发） 
- 参数： $userId:string: 接收者标识（必须），如：手机号，用于记录发送日志，任意值不超过50字节长度。 $userName:string: 接收者姓名（必须），用于记录发送日志，任意值不超过50字节长度。 $openId:string: 接收者企业微信openId。 $msgTypeId:string: 消息模版编码。 $bill:object: 单据内容（用于产生消息通知信息)。 
- 返回： 返回消息发送状态，0 - 成功 1 - 消息模版被禁用 other 失败

### `$vs.message.sendDingTalkMessage($userId:string,$userName:string,$openId:string,$msgTypeId:string,$bill:object,$extitems:Map<string,object>):int`
- 说明： 发送钉钉消息给指定人（不是系统内的人，站内信不发） 
- 参数： $userId:string: 接收者标识（必须），如：手机号，用于记录发送日志，任意值不超过50字节长度。 $userName:string: 接收者姓名（必须），用于记录发送日志，任意值不超过50字节长度。 $openId:string: 接收者钉钉openId。 $msgTypeId:string: 消息模版编码。 $bill:object: 单据内容（用于产生消息通知信息)。 $extitems:Map: 可选（允许为`null`），自定义消息项（钉钉和企业微信有效），允许开发者自定义消息项目。 
- 返回： 返回消息发送状态，0 - 成功 1 - 消息模版被禁用 other 失败

### `$vs.message.sendDingTalkMessage($userId:string,$userName:string,$openId:string,$msgTypeId:string,$bill:object):int`
- 说明： 发送钉钉消息给指定人（不是系统内的人，站内信不发） 
- 参数： $userId:string: 接收者标识（必须），如：手机号，用于记录发送日志，任意值不超过50字节长度。 $userName:string: 接收者姓名（必须），用于记录发送日志，任意值不超过50字节长度。 $openId:string: 接收者钉钉openId。 $msgTypeId:string: 消息模版编码。 $bill:object: 单据内容（用于产生消息通知信息)。 
- 返回： 返回消息发送状态，0 - 成功 1 - 消息模版被禁用 other 失败

### `$vs.message.sendInterTargetSystemMessage($appId:string,$data:object):void`
- 说明： 发送接口通知消息（仅用于通知第三方接口有新消息需要获取用) 
- 参数： $appId:string: 第三方系统编码。 $data:object: 需要推送给对方的业务数据（内容由业务系统和第三方系统协商)。 
- 返回： 无

### `$vs.message.sendSimpleMessage($userId:string,$msgTitle:string,$context:string,$systemId:string):int`
- 说明： 发送一个简单消息给用户 
- 参数： $userId:string: 操作员用户编码。 $msgTitle:string: 消息标题（200字节内)。 $context:string: 消息内容（500字节内)。 $systemId:string: 操作员所属的系统编码。 
- 返回： 0 - 未发送（用户不存在？消息未启用？或者其他错误） 1 - 发送成功

### `$vs.message.sendSimpleMessage($userId:string,$msgTitle:string,$context:string):int`
- 说明： 发送一个简单消息给用户（当前系统内的操作员) 
- 参数： $userId:string: 操作员用户编码。 $msgTitle:string: 消息标题（200字节内)。 $context:string: 消息内容（500字节内)。 
- 返回： 0 - 未发送（用户不存在？消息未启用？或者其他错误） 1 - 发送成功

### `$vs.message.sendSmsCode($mobile:string,$context:string,$code:string,$busCode:string):void`
- 说明： 发送验证码短信（注：需要实现过程函数`system.common.callback.sendSmsCode`才可发送） 
- 参数： $mobile:string: 接收者手机号。 $context:string: 短信内容（允许开发者修改）。 $code:string: 验证码。 $busCode:string: 业务识别码，如：sysLoginSms，开发者可以自己定义，在`system.common.callback.sendSmsCode`的`$busCode`参数接收。 
- 返回： 无

### `$vs.message.sendSmsMessage($mobile:string,$context:string,$busCode:string):void`
- 说明： 发送验证码短信（注：需要实现过程函数`system.common.callback.sendSmsMessage`才可发送） 
- 参数： $mobile:string: 接收者手机号。 $context:string: 短信内容（允许开发者修改）。 $busCode:string: 业务识别码，如：sysSmsMessage，开发者可以自己定义，在`system.common.callback.sendSmsMessage`的`$busCode`参数接收。 
- 返回： 无

### `$vs.message.sendTemplateMessage($userId:string,$msgTypeId:string,$bill:object,$param:string|Map,$systemId:string,$extitems:Map<string,object>):int`
- 说明： 发送一个基于消息模版的消息给用户 
- 参数： $userId:string: 操作员用户编码。 $msgTypeId:string: 消息模版编码。 $bill:object: 单据内容（用于产生消息通知信息)。 $param:object: 用于打开关联窗口时，传递给窗口的参数。 $systemId:string: 可选（允许为`null`），操作员所属的系统编码。 $extitems:Map: 可选（允许为`null`），自定义消息项（钉钉和企业微信有效），允许开发者自定义消息项目。 
- 返回： 0 - 未发送（用户不存在？消息未启用？或者其他错误） 1 - 发送成功

### `$vs.message.sendTemplateMessage($userId:string,$msgTypeId:string,$bill:object,$param:string|Map,$systemId:string):int`
- 说明： 发送一个基于消息模版的消息给用户 
- 参数： $userId:string: 操作员用户编码。 $msgTypeId:string: 消息模版编码。 $bill:object: 单据内容（用于产生消息通知信息)。 $param:object: 用于打开关联窗口时，传递给窗口的参数。 $systemId:string: 操作员所属的系统编码。 
- 返回： 0 - 未发送（用户不存在？消息未启用？或者其他错误） 1 - 发送成功

### `$vs.message.sendTemplateMessage($userId:string,$msgTypeId:string,$bill:object,$param:string|Map):int`
- 说明： 发送一个基于消息模版的消息给用户 
- 参数： $userId:string: 操作员用户编码。 $msgTypeId:string: 消息模版编码。 $bill:object: 单据内容（用于产生消息通知信息)。 $param:object: 用于打开关联窗口时，传递给窗口的参数。 
- 返回： 0 - 未发送（用户不存在？消息未启用？或者其他错误） 1 - 发送成功

### `$vs.message.sendWeChatMessage($userId:string,$userName:string,$openId:string,$msgTypeId:string,$bill:object,$extitems:Map<string,object>):int`
- 说明： 发送微信公众号消息给指定人（不是系统内的人，站内信不发） 
- 参数： $userId:string: 接收者标识（必须），如：手机号，用于记录发送日志，任意值不超过50字节长度。 $userName:string: 接收者姓名（必须），用于记录发送日志，任意值不超过50字节长度。 $openId:string: 接收者微信openId。 $msgTypeId:string: 消息模版编码。 $bill:object: 单据内容（用于产生消息通知信息)。 $extitems:Map: 可选（允许为`null`），自定义消息项（钉钉和企业微信有效），允许开发者自定义消息项目。 
- 返回： 返回消息发送状态，0 - 成功 1 - 消息模版被禁用 other 失败

### `$vs.message.sendWeChatMessage($userId:string,$userName:string,$openId:string,$msgTypeId:string,$bill:object):int`
- 说明： 发送微信公众号消息给指定人（不是系统内的人，站内信不发） 
- 参数： $userId:string: 接收者标识（必须），如：手机号，用于记录发送日志，任意值不超过50字节长度。 $userName:string: 接收者姓名（必须），用于记录发送日志，任意值不超过50字节长度。 $openId:string: 接收者微信openId。 $msgTypeId:string: 消息模版编码。 $bill:object: 单据内容（用于产生消息通知信息)。 
- 返回： 返回消息发送状态，0 - 成功 1 - 消息模版被禁用 other 失败

## $vs.mq - MQ订阅及发送对象(12 methods)

### `$vs.mq.batchSend($topic:string,$datas:List<object>):SendResult`
- 说明： 批量发起MQ消息（不可使用秘钥功能）。（注意：从1.5.0版本开始，谷神框架不再默认支持RocketMQ功能，若项目需要用到RocketMQ，请下载插件包放到libs目录中） 
- 参数： $topic:string: 消息主题。 $datas:List: 需要推送的数据。 
- 返回： MQ应答结果

### `$vs.mq.batchSend($topic:string,$tag:string,$datas:List<object>):SendResult`
- 说明： 批量发起MQ消息（不可使用秘钥功能）。（注意：从1.5.0版本开始，谷神框架不再默认支持RocketMQ功能，若项目需要用到RocketMQ，请下载插件包放到libs目录中） 
- 参数： $topic:string: 消息主题。 $tag:string: MQ标签，可缺省。 $datas:List: 需要推送的数据。 
- 返回： MQ应答结果

### `$vs.mq.send($topic:string,$data:object):SendResult`
- 说明： 发送MQ消息。（注意：从1.5.0版本开始，谷神框架不再默认支持RocketMQ功能，若项目需要用到RocketMQ，请下载插件包放到libs目录中） 
- 参数： $topic:string: 消息主题。 $data:object: 需要推送的数据。 
- 返回： MQ应答结果

### `$vs.mq.send($topic:string,$tag:string,$data:object):SendResult`
- 说明： 发送MQ消息。（注意：从1.5.0版本开始，谷神框架不再默认支持RocketMQ功能，若项目需要用到RocketMQ，请下载插件包放到libs目录中） 
- 参数： $topic:string: 消息主题。 $tag:string: MQ标签，可缺省。 $data:object: 需要推送的数据。 
- 返回： MQ应答结果

### `$vs.mq.start($topic:string,$accessKey:string,$secretKey:string):boolean`
- 说明： 有密链接频道。（注意：从1.5.0版本开始，谷神框架不再默认支持RocketMQ功能，若项目需要用到RocketMQ，请下载插件包放到libs目录中） 
- 参数： $topic:string: 消息主题。 $accessKey:string: 通信秘钥。 $secretKey:string: 通信秘钥。 
- 返回： MQ应答结果

### `$vs.mq.starts($topic:List<string>,$accessKey:string,$secretKey:string):boolean`
- 说明： 有密链接频道（所有频道秘钥相同）。（注意：从1.5.0版本开始，谷神框架不再默认支持RocketMQ功能，若项目需要用到RocketMQ，请下载插件包放到libs目录中） 
- 参数： $topic:string: 消息主题。 $accessKey:string: 通信秘钥。 $secretKey:string: 通信秘钥。 
- 返回： MQ应答结果

### `$vs.mq.subscribe($topic:string,$procName:string,$funName:string):void`
- 说明： 发起MQ消息订阅（注意：从1.5.0版本开始，谷神框架不再默认支持RocketMQ功能，若项目需要用到RocketMQ，请下载插件包放到libs目录中）。 过程脚本： ``` com.golden.xxx.subscribe($topic:string,$tag:strig,$msgs:list)``` 
- 参数： $topic:string: 订阅消息主题。 $procName:string: 应答过程脚本ID。 $funName:string: 应答过程脚本方法名称。 
- 返回： 无

### `$vs.mq.subscribe($topic:string,$tag:string,$procName:string,$funName:string,$accessKey:string,$secretKey:string):void`
- 说明： 发起MQ消息订阅（注意：从1.5.0版本开始，谷神框架不再默认支持RocketMQ功能，若项目需要用到RocketMQ，请下载插件包放到libs目录中）。 过程脚本： ``` com.golden.xxx.subscribe($topic:string,$tag:strig,$msgs:list)``` 
- 参数： $topic:string: 订阅消息主题。 $tag:string: MQ标签，可缺省。 $procName:string: 应答过程脚本ID。 $funName:string: 应答过程脚本方法名称。 $accessKey:string: 通信秘钥。 $secretKey:string: 通信秘钥。 
- 返回： 无

### `$vs.mq.subscribe($topic:string,$tag:string,$procName:string,$funName:string):void`
- 说明： 发起MQ消息订阅（注意：从1.5.0版本开始，谷神框架不再默认支持RocketMQ功能，若项目需要用到RocketMQ，请下载插件包放到libs目录中）。 过程脚本： ``` com.golden.xxx.subscribe($topic:string,$tag:strig,$msgs:list)``` 
- 参数： $topic:string: 订阅消息主题。 $tag:string: MQ标签，可缺省。 $procName:string: 应答过程脚本ID。 $funName:string: 应答过程脚本方法名称。 
- 返回： 无

### `$vs.mq.subscribes($topics:List<string>,$procName:string,$funName:string):void`
- 说明： 发起MQ消息批量订阅（注意：从1.5.0版本开始，谷神框架不再默认支持RocketMQ功能，若项目需要用到RocketMQ，请下载插件包放到libs目录中）。 过程脚本： ``` com.golden.xxx.subscribe($topic:string,$tag:strig,$msgs:list)``` 
- 参数： $topics:List: 订阅消息主题。 $procName:string: 应答过程脚本ID。 $funName:string: 应答过程脚本方法名称。 
- 返回： 无

### `$vs.mq.subscribes($topics:List<string>,$tag:string,$procName:string,$funName:string,$accessKey:String,$secretKey:String):void`
- 说明： 发起MQ消息批量订阅（注意：从1.5.0版本开始，谷神框架不再默认支持RocketMQ功能，若项目需要用到RocketMQ，请下载插件包放到libs目录中）。 过程脚本： ``` com.golden.xxx.subscribe($topic:string,$tag:strig,$msgs:list)``` 
- 参数： $topics:List: 订阅消息主题。 $tag:string: MQ标签，可缺省。 $procName:string: 应答过程脚本ID。 $funName:string: 应答过程脚本方法名称。 $accessKey:string: 通信秘钥。 $secretKey:string: 通信秘钥。 
- 返回： 无

### `$vs.mq.subscribes($topics:List<string>,$tag:string,$procName:string,$funName:string):void`
- 说明： 发起MQ消息批量订阅（注意：从1.5.0版本开始，谷神框架不再默认支持RocketMQ功能，若项目需要用到RocketMQ，请下载插件包放到libs目录中）。 过程脚本： ``` com.golden.xxx.subscribe($topic:string,$tag:strig,$msgs:list)``` 
- 参数： $topics:List: 订阅消息主题。 $tag:string: MQ标签，可缺省。 $procName:string: 应答过程脚本ID。 $funName:string: 应答过程脚本方法名称。 
- 返回： 无

## $vs.ocr - 图像识别(8 methods)

### `$vs.ocr.bankCard($filePath:string):bankCardInfo`
- 说明： 银行卡识别 
- 参数： $filePath:string: 文件系统存放路径（公有私有文件均可），如：/upload/images/AD/EB/12/239872349.png。 
- 返回： 银行卡信息

### `$vs.ocr.carPlate($filePath:string):carPlateInfo`
- 说明： 车牌号识别 
- 参数： $filePath:string: 文件系统存放路径（公有私有文件均可），如：/upload/images/AD/EB/12/239872349.png。 
- 返回： 车牌号信息

### `$vs.ocr.generalText($filePath:string,$isHaveLocation:boolean):List`
- 说明： 通用文字识别 
- 参数： $filePath:string: 文件系统存放路径（公有私有文件均可），如：/upload/images/AD/EB/12/239872349.png。 $isHaveLocation:boolean: 是否包含文字的位置信息，true - 包含 false - 不含（默认)。 
- 返回： 图片中包含的文字列表

### `$vs.ocr.generalText($filePath:string):List`
- 说明： 通用文字识别 
- 参数： $filePath:string: 文件系统存放路径（公有私有文件均可），如：/upload/images/AD/EB/12/239872349.png。 
- 返回： 图片中包含的文字列表

### `$vs.ocr.handWriting($filePath:string):List`
- 说明： 手写图片识别 
- 参数： $filePath:string: 文件系统存放路径（公有私有文件均可），如：/upload/images/AD/EB/12/239872349.png。 
- 返回： 图片中包含的文字列表

### `$vs.ocr.idCardBack($filePath:string):idCardFrontInfo`
- 说明： 识别身份证背面（国徽)信息 
- 参数： $filePath:string: 文件系统存放路径（公有私有文件均可），如：/upload/images/AD/EB/12/239872349.png。 
- 返回： 身份证背面（国徽)信息

### `$vs.ocr.idCardFront($filePath:string):idCardFrontInfo`
- 说明： 识别身份证正面（国徽)信息 
- 参数： $filePath:string: 文件系统存放路径（公有私有文件均可），如：/upload/images/AD/EB/12/239872349.png。 
- 返回： 身份证正面（国徽)信息

### `$vs.ocr.vatInvoice($filePath:string):InvoiceInfo`
- 说明： 增值税发票识别 
- 参数： $filePath:string: 文件系统存放路径（公有私有文件均可），如：/upload/images/AD/EB/12/239872349.png。 
- 返回： 发票信息

## $vs.page - 谷神页面对象信息(2 methods)

### `$vs.page.getPage($pageId:string):UiPage`
- 说明： 获取页面对象（主数据可以获取所有服务【含各个微服务】的页面对象，各个微服务调用本方法只能获取到本微服务的页面对象） 
- 参数： $pageId:string: 页面编码。 
- 返回： 返回谷神页面对象or `null` 不存在

### `$vs.page.getPageControl($pageId:string,$ctrlId:string):UiControl`
- 说明： 获取页面内的控件（主数据可以获取所有服务【含各个微服务】的页面对象，各个微服务调用本方法只能获取到本微服务的页面对象） 
- 参数： $pageId:string: 页面编码。 $ctrlId:string: 控件编码。 
- 返回： 返回谷神控件对象or `null` 不存在

## $vs.proc - 过程访问对象(35 methods)

### `$vs.proc.callDetailPageSearch($pageId:string,$form:Map<String,Object>):Map<String, Object>`
- 说明： 调用详情页面查询单据数据（支持跨微服务查询） 
- 参数： $pageId:string: 页面编码或页面别名。 $form:Map: 查询条件。 
- 返回： 查询结果

### `$vs.proc.callMainPageFind($pageId:string,$form:Map<String,Object>,$pageSize:int,$pageNo:int,$mainTableId:string):PageSearchResult`
- 说明： 调用主页面报表查询接口查询数据（分页，支持跨微服务查询） 
- 参数： $pageId:string: 主页面编码或页面别名。 $form:Map: 查询条件。 $pageSize:int: 每页大小。 $pageNo:int: 读取页数。 $mainTableId:string: 页面的主数据表格编码（若页面上只有一个主数据表格，则可以不填写此参数）。 
- 返回： 查询结果

### `$vs.proc.callMainPageFind($pageId:string,$form:Map<String,Object>,$pageSize:int,$pageNo:int):PageSearchResult`
- 说明： 调用主页面报表查询接口查询数据（分页，支持跨微服务查询） 
- 参数： $pageId:string: 主页面编码或页面别名。 $form:Map: 查询条件。 $pageSize:int: 每页大小。 $pageNo:int: 读取页数。 
- 返回： 查询结果

### `$vs.proc.callMainPageList($pageId:string,$form:Map<String,Object>,$mainTableId:string):List<Map<String, Object>>`
- 说明： 调用主页面报表查询接口查询数据（不分页，支持跨微服务查询） 
- 参数： $pageId:string: 主页面编码或页面别名。 $form:Map: 查询条件。 $mainTableId:string: 页面的主数据表格编码（若页面上只有一个主数据表格，则可以不填写此参数）。 
- 返回： 查询结果

### `$vs.proc.callMainPageList($pageId:string,$form:Map<String,Object>):List<Map<String, Object>>`
- 说明： 调用主页面报表查询接口查询数据（不分页，支持跨微服务查询） 
- 参数： $pageId:string: 主页面编码或页面别名。 $form:Map: 查询条件。 
- 返回： 查询结果

### `$vs.proc.callMainPageSum($pageId:string,$form:Map<String,Object>,$mainTableId:string):List<Map<String, Object>>`
- 说明： 调用主页面报表汇总数据（支持跨微服务查询） 
- 参数： $pageId:string: 主页面编码或页面别名。 $form:Map: 查询条件。 $mainTableId:string: 页面的主数据表格编码（若页面上只有一个主数据表格，则可以不填写此参数）。 
- 返回： 查询结果

### `$vs.proc.callMainPageSum($pageId:string,$form:Map<String,Object>):List<Map<String, Object>>`
- 说明： 调用主页面报表汇总数据（支持跨微服务查询） 
- 参数： $pageId:string: 主页面编码或页面别名。 $form:Map: 查询条件。 
- 返回： 查询结果

### `$vs.proc.callPageRemove($mainPageId:string,$editPageId:string,$whereData:Map<String,Object>,$bntId:string,$ignoreTrans:boolean,$ignoreDataAuth:boolean):void`
- 说明： 服务端调用页面的单据删除方法（一般用于接口等需要删除单据时与原保存代码复用的场景），注意：本方法必须在无事务环境下运行。 
- 参数： $mainPageId:string: 主页面编码或者页面别名。 $editPageId:string: 编辑面编码或者页面别名。 $whereData:Map: 删除条件。 $bntId:string: 主页面上删除按钮的ID，若页面上只有一个提交按钮，则此参数可以不填写，或者传值null。 $ignoreTrans:boolean: 忽略事务警告（强制在事务内运行本方法），警告：强制在事务内运行本方法极易导致死锁。 $ignoreDataAuth:boolean: 忽略数据权限，本过程不校验数据权限。 
- 返回： 数据对象

### `$vs.proc.callPageRemove($mainPageId:string,$editPageId:string,$whereData:Map<String,Object>,$bntId:string,$ignoreTrans:boolean):void`
- 说明： 服务端调用页面的单据删除方法（一般用于接口等需要删除单据时与原保存代码复用的场景），注意：本方法必须在无事务环境下运行。 
- 参数： $mainPageId:string: 主页面编码或者页面别名。 $editPageId:string: 编辑面编码或者页面别名。 $whereData:Map: 删除条件。 $bntId:string: 主页面上删除按钮的ID，若页面上只有一个提交按钮，则此参数可以不填写，或者传值null。 $ignoreTrans:boolean: 忽略事务警告（强制在事务内运行本方法），警告：强制在事务内运行本方法极易导致死锁。 
- 返回： 数据对象

### `$vs.proc.callPageRemove($mainPageId:string,$editPageId:string,$whereData:Map<String,Object>,$bntId:string):void`
- 说明： 服务端调用页面的单据删除方法（一般用于接口等需要删除单据时与原保存代码复用的场景），注意：本方法必须在无事务环境下运行。 
- 参数： $mainPageId:string: 主页面编码或者页面别名。 $editPageId:string: 编辑面编码或者页面别名。 $whereData:Map: 删除条件。 $bntId:string: 主页面上删除按钮的ID，若页面上只有一个提交按钮，则此参数可以不填写。 
- 返回： 数据对象

### `$vs.proc.callPageRemove($mainPageId:string,$editPageId:string,$whereData:Map<String,Object>):void`
- 说明： 服务端调用页面的单据删除方法（一般用于接口等需要删除单据时与原保存代码复用的场景），注意：本方法必须在无事务环境下运行。 
- 参数： $mainPageId:string: 主页面编码或者页面别名。 $editPageId:string: 编辑面编码或者页面别名。 $whereData:Map: 删除条件。 
- 返回： 数据对象

### `$vs.proc.callPageSave($pageId:string,$data:Map<String,Object>,$bntId:string,$ignoreTrans:boolean,$ignoreDataAuth:boolean):Map<String,Object>`
- 说明： 服务端调用页面的单据新增方法（一般用于接口等需要创建单据时与原保存代码复用的场景）。 
- 参数： $pageId:string: 页面编码或者页面别名。 $data:Map: 数据参数，可以参考页面提交时传输给服务器的参数。 $bntId:string: 页面上保存按钮的ID，若页面上只有一个保存按钮，则此参数可以不填写，或者传值null。 $ignoreTrans:boolean: 忽略事务警告（强制在事务内运行本方法），警告：强制在事务内运行本方法极易导致死锁。 $ignoreDataAuth:boolean: 忽略数据权限，本过程不校验数据权限。 
- 返回： 数据对象

### `$vs.proc.callPageSave($pageId:string,$data:Map<String,Object>,$bntId:string,$ignoreTrans:boolean):Map<String,Object>`
- 说明： 服务端调用页面的单据新增方法（一般用于接口等需要创建单据时与原保存代码复用的场景）。 
- 参数： $pageId:string: 页面编码或者页面别名。 $data:Map: 数据参数，可以参考页面提交时传输给服务器的参数。 $bntId:string: 页面上保存按钮的ID，若页面上只有一个保存按钮，则此参数可以不填写，或者传值null。 $ignoreTrans:boolean: 忽略事务警告（强制在事务内运行本方法），警告：强制在事务内运行本方法极易导致死锁。 
- 返回： 数据对象

### `$vs.proc.callPageSave($pageId:string,$data:Map<String,Object>,$bntId:string):Map<String,Object>`
- 说明： 服务端调用页面的单据新增方法（一般用于接口等需要创建单据时与原保存代码复用的场景）。 
- 参数： $pageId:string: 页面编码或者页面别名。 $data:Map: 数据参数，可以参考页面提交时传输给服务器的参数。 $bntId:string: 页面上保存按钮的ID，若页面上只有一个保存按钮，则此参数可以不填写。 
- 返回： 数据对象

### `$vs.proc.callPageSave($pageId:string,$data:Map<String,Object>):Map<String,Object>`
- 说明： 服务端调用页面的单据新增方法（一般用于接口等需要创建单据时与原保存代码复用的场景）。 
- 参数： $pageId:string: 页面编码或者页面别名。 $data:Map: 数据参数，可以参考页面提交时传输给服务器的参数。 
- 返回： 数据对象

### `$vs.proc.callPageUpdate($pageId:string,$data:Map<String,Object>,$bntId:string,$ignoreTrans:boolean,$ignoreDataAuth:boolean):Map<String,Object>`
- 说明： 服务端调用页面的单据修改方法（一般用于接口等需要创建单据时与原保存代码复用的场景），注意：本方法必须在无事务环境下运行。 
- 参数： $pageId:string: 页面编码或者页面别名。 $data:Map: 数据参数，可以参考页面提交时传输给服务器的参数。 $bntId:string: 页面上保存按钮的ID，若页面上只有一个保存按钮，则此参数可以不填写，或者传值null。 $ignoreTrans:boolean: 忽略事务警告（强制在事务内运行本方法），警告：强制在事务内运行本方法极易导致死锁。 $ignoreDataAuth:boolean: 忽略数据权限，本过程不校验数据权限。 
- 返回： 数据对象

### `$vs.proc.callPageUpdate($pageId:string,$data:Map<String,Object>,$bntId:string,$ignoreTrans:boolean):Map<String,Object>`
- 说明： 服务端调用页面的单据修改方法（一般用于接口等需要创建单据时与原保存代码复用的场景），注意：本方法必须在无事务环境下运行。 
- 参数： $pageId:string: 页面编码或者页面别名。 $data:Map: 数据参数，可以参考页面提交时传输给服务器的参数。 $bntId:string: 页面上保存按钮的ID，若页面上只有一个保存按钮，则此参数可以不填写，或者传值null。 $ignoreTrans:boolean: 忽略事务警告（强制在事务内运行本方法），警告：强制在事务内运行本方法极易导致死锁。 
- 返回： 数据对象

### `$vs.proc.callPageUpdate($pageId:string,$data:Map<String,Object>,$bntId:string):Map<String,Object>`
- 说明： 服务端调用页面的单据修改方法（一般用于接口等需要创建单据时与原保存代码复用的场景），注意：本方法必须在无事务环境下运行。 
- 参数： $pageId:string: 页面编码或者页面别名。 $data:Map: 数据参数，可以参考页面提交时传输给服务器的参数。 $bntId:string: 页面上保存按钮的ID，若页面上只有一个保存按钮，则此参数可以不填写。 
- 返回： 数据对象

### `$vs.proc.callPageUpdate($pageId:string,$data:Map<String,Object>):Map<String,Object>`
- 说明： 服务端调用页面的单据修改方法（一般用于接口等需要创建单据时与原保存代码复用的场景），注意：本方法必须在无事务环境下运行。 
- 参数： $pageId:string: 页面编码或者页面别名。 $data:Map: 数据参数，可以参考页面提交时传输给服务器的参数。 
- 返回： 数据对象

### `$vs.proc.executeScript($script:string,$param:Map<String,Object>):object`
- 说明： 动态执行一段谷神脚本语言 
- 参数： $script:string: 谷神脚本，如： `return ($billNo eq 1) ? true : false` 或者 `return $user.userId` 。 $param:Map: 参数变量。 
- 返回： 根据脚本确定返回值

### `$vs.proc.executeScript($script:string):object`
- 说明： 动态执行一段谷神脚本语言 
- 参数： $script:string: 谷神脚本，如： `return ($billNo eq 1) ? true : false` 或者 `return $user.userId` 。 
- 返回： 根据脚本确定返回值

### `$vs.proc.exportMainPage($pageId:string,$form:Map<String,Object>,$mainTableId:string,$fields:List<String>,$fileName:string,$title:string):string`
- 说明： 导出主页面数据为EXCEL文件（支持跨微服务查询） 
- 参数： $pageId:string: 页面编码或页面别名。 $form:Map : 查询条件。 $mainTableId:string: [可缺省]导出数据的目标主表格ID，若页面只有一个主表格可以缺省。 $fields:List: [可缺省]需要导出的字段列表，默认导出设计时的表格可视字段。 $fileName:string: [可缺省]导出文件名称，默认随机文件名称。 $title:string: [可缺省]文件标题。 
- 返回： 文件保存路径（临时文件目录）

### `$vs.proc.exportMainPage($pageId:string,$form:Map<String,Object>,$mainTableId:string,$fields:List<String>,$fileName:string):string`
- 说明： 导出主页面数据为EXCEL文件（支持跨微服务查询） 
- 参数： $pageId:string: 页面编码或页面别名。 $form:Map : 查询条件。 $mainTableId:string: [可缺省]导出数据的目标主表格ID，若页面只有一个主表格可以缺省。 $fields:List: [可缺省]需要导出的字段列表，默认导出设计时的表格可视字段。 $fileName:string: [可缺省]导出文件名称，默认随机文件名称。 
- 返回： 文件保存路径（临时文件目录）

### `$vs.proc.exportMainPage($pageId:string,$form:Map<String,Object>,$mainTableId:string,$fields:List<String>):string`
- 说明： 导出主页面数据为EXCEL文件（支持跨微服务查询） 
- 参数： $pageId:string: 页面编码或页面别名。 $form:Map : 查询条件。 $mainTableId:string: [可缺省]导出数据的目标主表格ID，若页面只有一个主表格可以缺省。 $fields:List: [可缺省]需要导出的字段列表，默认导出设计时的表格可视字段。 
- 返回： 文件保存路径（临时文件目录）

### `$vs.proc.exportMainPage($pageId:string,$form:Map<String,Object>,$mainTableId:string):string`
- 说明： 导出主页面数据为EXCEL文件（支持跨微服务查询） 
- 参数： $pageId:string: 页面编码或页面别名。 $form:Map: 查询条件。 $mainTableId:string: [可缺省]导出数据的目标主表格ID，若页面只有一个主表格可以缺省。 
- 返回： 文件保存路径（临时文件目录）

### `$vs.proc.exportMainPage($pageId:string,$form:Map<String,Object>):string`
- 说明： 导出主页面数据为EXCEL文件（支持跨微服务查询） 
- 参数： $pageId:string: 页面编码或页面别名。 $form:Map: 查询条件。 
- 返回： 文件保存路径（临时文件目录）

### `$vs.proc.find($strProcName:string,$timeout:int,$systemId:string):Proc`
- 说明： 查找过程脚本服务 
- 参数： $strProcName:string: 过程脚本编码。 $timeout:int: 超时时间（秒），0 - 表示永不超时 默认：1800（半小时）。 $systemId:string: 期望的系统编码（后台算法优先选择此系统编码，除非此编码不存在才会随机路由)。 
- 返回： 过程脚本实例

### `$vs.proc.find($strProcName:string,$timeout:int):Proc`
- 说明： 查找过程脚本服务 
- 参数： $strProcName:string: 过程脚本编码。 $timeout:int: 超时时间（秒），0 - 表示永不超时 默认：1800（半小时）。 
- 返回： 过程脚本实例

### `$vs.proc.find($strProcName:string):Proc`
- 说明： 查找过程脚本服务 
- 参数： $strProcName:string: 过程脚本编码。 
- 返回： 过程脚本实例

### `$vs.proc.invoke($strProcName:string,$funName:string,$args:Object...):Object`
- 说明： 立即执行过程脚本中的方法。 
- 用法： ``` $vs.proc.invoke("com.golden.proc","noParamFun") #set($bean=$vs.proc.invoke("com.golden.proc","get",$form,1000)) ``` 
- 参数： $strProcName:string: 过程脚本编码。 $funName:string: 过程脚本函数名称。 $args:Object...: 过程脚本函数参数，根据实际情况，这里可以是0-n个参数。 
- 返回： 过程脚本实例

### `$vs.proc.invokeWithGlobalTrans($strProcName:string,$funName:string,$args:Object...):Object`
- 说明： 立即执行过程脚本中的方法（强制使用分布式事务调用）。 
- 用法： ``` $vs.proc.invokeWithGlobalTrans("com.golden.proc","noParamFun") #set($bean=$vs.proc.invokeWithGlobalTrans("com.golden.proc","get",$form,1000)) ``` 
- 参数： $strProcName:string: 过程脚本编码。 $funName:string: 过程脚本函数名称。 $args:Object...: 过程脚本函数参数，根据实际情况，这里可以是0-n个参数。 
- 返回： 过程脚本实例

### `$vs.proc.isHaveProc($procName:string,$funName:string):boolean`
- 说明： 判断过程函数是否存在（支持跨数据库）。 
- 参数： $procName:string: 过程函数编码。 $funName:Object: 过程函数名称。 
- 返回： 存在返回`true`；不存在返回`false`

### `$vs.proc.isHaveServiceComp($compId:string):boolean`
- 说明： 判断服务组件是否存在（注意不能跨数据库）。 
- 参数： $compId:string: 服务组件编码。 
- 返回： 存在返回`true`；不存在返回`false`

### `$vs.proc.runServiceComp($strCompId:string,$args:Object,$isInGlobalTran:boolean):Object`
- 说明： 执行服务组件（注意：不支持跨数据库)。 
- 参数： $strCompId:string: 过程脚本编码。 $args:Object: 过程脚本函数名称。 $isInGlobalTran:Object: 是否强制在分布式事务内运行。 
- 返回： 服务组件中的$result对象

### `$vs.proc.runServiceComp($strCompId:string,$args:Object):Object`
- 说明： 执行服务组件（注意：不支持跨数据库)。 
- 参数： $strCompId:string: 过程脚本编码。 $args:Object: 过程脚本函数名称。 
- 返回： 服务组件中的$result对象

## $vs.properties - 配置文件对象(28 methods)

### `$vs.properties.getModuleConfig($configId:string,$systemId:string):Map`
- 说明： 获取模块配置参数根对象，取数规则：判断要求的系统是否为当前系统，若为当前系统，则读取本地库数据，若存在配置则返回，若不存在，则返回为空；若判断要求的系统编码不是本地，则漫游到要求的系统编码中读取对应的参数配置。。 
- 参数： $configId:string: 配置参数编码。 $systemId:string: 系统编码（支持跨系统漫游读取配置信息）。 
- 返回： 配置参数对象

### `$vs.properties.getModuleConfig($configId:string):Map`
- 说明： 获取模块配置参数根对象，取数规则：读取当前数据源（数据库）下的配置参数，若存在且唯一，则返回，若存在且不唯一，则抛异常，必须传值系统编码进行过滤。即，模块参数编码尽量不要设置成一样的，每个应用的参数编码区分开来，如：com.golden.bdp.BTXXX 、 com.golden.ebp.BTXXX，这样就可以通过模块编码来作为唯一条件读取模块配置，注意：本方法不支持漫游，即，不可以在主数据通过模块配置编码读取业务微服务的配置信息。 
- 参数： $configId:string: 配置参数编码。 
- 返回： 配置参数对象

### `$vs.properties.getModuleConfigValue($configId:string,$path:string,$defvalue:object,$systemId:string):Object`
- 说明： 获取模块配置参数值。取数规则：判断要求的系统是否为当前系统，若为当前系统，则读取本地库数据，若存在配置则返回，若不存在，则返回为空；若判断要求的系统编码不是本地，则漫游到要求的系统编码中读取对应的参数配置。 
- 参数： $configId:string: 配置参数编码。 $path:string: 配置参数变量名称，如：billInfo.tabTables.tableId。 $defvalue:string: 当未成功获取数据时，返回的默认结果。 $systemId:string: 系统编码（支持跨系统漫游读取配置信息）。 
- 返回： 根据配置内容不同而返回不同结果，可能是string可能是list可能是map

### `$vs.properties.getModuleConfigValue($configId:string,$path:string,$defvalue:object):Object`
- 说明： 获取模块配置参数值。取数规则：读取当前数据源（数据库）下的配置参数，若存在且唯一，则返回，若存在且不唯一，则抛异常，必须传值系统编码进行过滤。即，模块参数编码尽量不要设置成一样的，每个应用的参数编码区分开来，如：com.golden.bdp.BTXXX 、 com.golden.ebp.BTXXX，这样就可以通过模块编码来作为唯一条件读取模块配置，注意：本方法不支持漫游，即，不可以在主数据通过模块配置编码读取业务微服务的配置信息。 
- 参数： $configId:string: 配置参数编码。 $path:string: 配置参数变量名称，如：billInfo.tabTables.tableId。 $defvalue:string: 当未成功获取数据时，返回的默认结果。 
- 返回： 根据配置内容不同而返回不同结果，可能是string可能是list可能是map

### `$vs.properties.getModuleConfigValue($configId:string,$path:string):Object`
- 说明： 获取模块配置参数值。取数规则：读取当前数据源（数据库）下的配置参数，若存在且唯一，则返回，若存在且不唯一，则抛异常，必须传值系统编码进行过滤。即，模块参数编码尽量不要设置成一样的，每个应用的参数编码区分开来，如：com.golden.bdp.BTXXX 、 com.golden.ebp.BTXXX，这样就可以通过模块编码来作为唯一条件读取模块配置，注意：本方法不支持漫游，即，不可以在主数据通过模块配置编码读取业务微服务的配置信息。 
- 参数： $configId:string: 配置参数编码。 $path:string: 配置参数变量名称，如：billInfo.tabTables.tableId。 
- 返回： 根据配置内容不同而返回不同结果，可能是string可能是list可能是map

### `$vs.properties.getProperty($key:string,$defValue:string):string`
- 说明： 获取配置变量值。 
- 参数： $key:string: 配置键值，如：spring.application.name。 $defValue:string: 默认值。 
- 返回： 对应的配置值

### `$vs.properties.getProperty($key:string):string`
- 说明： 获取配置变量值。 
- 参数： $key:string: 配置键值，如：spring.application.name。 
- 返回： 对应的配置值

### `$vs.properties.getRegAuthorizeNo():String`
- 说明： 获取授权文件里的授权书编号(授权书编号为资源管理服务里客户授权里的授权书编号)。 
- 参数： 无 
- 返回： 授权文件的客户号

### `$vs.properties.getRegClient():String`
- 说明： 获取授权文件里的客户号(客户号为资源管理服务里客户管理里的客户号)。 
- 参数： 无 
- 返回： 授权文件的客户号

### `$vs.properties.getRegDate():Date`
- 说明： 获取授权日期。 
- 参数： 无 
- 返回： 开发环境无法获取

### `$vs.properties.getRegDisabledMenus():Map<String, List<String>>`
- 说明： 获取禁用菜单（null or empty 表示无）。 
- 参数： 无 
- 返回： 开发环境无法获取；数据格式：Map>

### `$vs.properties.getRegIsOnlineUserModel():boolean`
- 说明： 获取授权文件里的授权用户数控制模式是否为在线人数控制。 
- 参数： 无 
- 返回： true - 在线人数控制 false - 操作员个数控制

### `$vs.properties.getRegLastDate():Date`
- 说明： 获取授权截止日期。 
- 参数： 无 
- 返回： 开发环境无法获取

### `$vs.properties.getRegMaxOrg():int`
- 说明： 获取授权文件里的授权最大机构数。 
- 参数： 无 
- 返回： 开发环境无法获取；0 表示不限； -1 表示开发环境

### `$vs.properties.getRegMaxUser():int`
- 说明： 获取授权文件里的授权用户数。 
- 参数： 无 
- 返回： 开发环境无法获取；0 表示不限； -1 表示开发环境；注意：用户数为启用用户数，对于停用用户不在计数之内；若启用用户数超过规定数，则系统自动禁用相关多余的账户

### `$vs.properties.getRegModels():Map<String, List<String>>`
- 说明： 获取授权模块列表（null or empty 表示所有模块）。 
- 参数： 无 
- 返回： 开发环境无法获取；数据格式：Map>

### `$vs.properties.getRegOtherConfig():map`
- 说明： 获取授权文件中其他配置项。 
- 参数： 无 
- 返回： 开发环境无法获取

### `$vs.properties.getRegPublisher():string`
- 说明： 获取授权文件颁发单位名称。 
- 参数： 无 
- 返回： 开发环境无法获取

### `$vs.properties.getRegSystems():map`
- 说明： 获取授权文件里授权的系统编码。 
- 参数： 无 
- 返回： 开发环境无法获取；数据格式：Map

### `$vs.properties.getRegUnitName():string`
- 说明： 获取授权文件使用单位名称。 
- 参数： 无 
- 返回： 开发环境无法获取

### `$vs.properties.getRegVersion():Integer`
- 说明： 获取授权文件版本号。 
- 参数： 无 
- 返回： 授权文件版本号

### `$vs.properties.getSystemDbInfo():DbInfo`
- 说明： 获取当前系统数据库连接信息（用户、数据库、IP、端口等，不含密码）。 
- 参数： 无 
- 返回： 数据库连接信息

### `$vs.properties.getSystemDbInfo($systemId:string):DbInfo`
- 说明： 获取指定系统数据库连接信息（用户、数据库、IP、端口等，不含密码）本方法支持跨微服务漫游。 
- 参数： $systemId:string: 指定需要查询的系统编码。 
- 返回： 数据库连接信息

### `$vs.properties.getSystemVarValue($varId:string,$defValue:string,$systemId:string):string`
- 说明： 获取应用参数配置值。 
- 参数： $varId:string: 参数编码，如：com.golden.bdp.color。 $defValue:string: 默认值。 $systemId:string: 系统编码（必须是同数据库的系统编码，如：管理系统和协同系统，缺省为当前系统编码）。 
- 返回： 对应的配置值，若参数不存在，则返回`$defValue`

### `$vs.properties.getSystemVarValue($varId:string,$defValue:string):string`
- 说明： 获取应用参数配置值。 
- 参数： $varId:string: 参数编码，如：com.golden.bdp.color。 $defValue:string: 默认值。 
- 返回： 对应的配置值，若参数不存在，则返回`$defValue`

### `$vs.properties.getSystemVarValue($varId:string):string`
- 说明： 获取应用参数配置值。 
- 参数： $varId:string: 参数编码，如：com.golden.bdp.color。 
- 返回： 对应的配置值，若参数不存在，则返回`null`

### `$vs.properties.getUserPassType():string`
- 说明： 获取当前系统用户密码算法类型。 
- 参数： 无 
- 返回： MD5 or SM3

### `$vs.properties.isDevelop():boolean`
- 说明： 当前运行的环境是否为开发环境还是打包后的环境。 
- 参数： 无 
- 返回： `true` - 开发环境； `false` - 生产环境（打包后环境）

## $vs.redis - REDIS访问对象(70 methods)

### `$vs.redis.append($key:string,$value:string):long`
- 说明： 向redis中的字符串追加内容 
- 参数： $key:string: 数据键值。 $value:string: 要追加的数据。 
- 返回： 追加指定值之后， key 中字符串的长度

### `$vs.redis.blpop($key:string,$timeout:int):string`
- 说明： 移出并获取列表的第一个元素， 如果列表没有元素会阻塞列表直到发现可弹出元素为止。 
- 参数： $key:string: 需要操作的列表键值。 $timeout:int: 超时时间，0或不填表示无限等待。 
- 返回： 对应的字符串值

### `$vs.redis.blpopBean($key:string,$timeout:int):object`
- 说明： 移出并获取列表的最后一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。 
- 参数： $key:string: 需要操作的列表键值。 $timeout:int: 超时时间，0或不填表示无限等待。 
- 返回： 对应的对象值

### `$vs.redis.brpop($key:string,$timeout:int):string`
- 说明： 移出并获取列表的最后一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。 
- 参数： $key:string: 需要操作的列表键值。 $timeout:int: 超时时间，0或不填表示无限等待。 
- 返回： 对应的字符串值

### `$vs.redis.decr($key:string,$i:int):long`
- 说明： 将 key 中储存的数字值减`$i` 
- 参数： $key:string: 数据键值。 $i:string: 递减的数字。 
- 返回： 执行命令之后 key 的值。

### `$vs.redis.decr($key:string):long`
- 说明： 将 key 中储存的数字值减一 
- 参数： $key:string: 数据键值。 
- 返回： 执行命令之后 key 的值。

### `$vs.redis.del($key:string):int`
- 说明： 移除redis中，key指定的元素。 
- 参数： $key:string: 需要操作的列表键值。 
- 返回： 被移除的数量

### `$vs.redis.dels($keys:List<string>):int`
- 说明： 移除redis中，key指定的元素。 
- 参数： $keys:List: 需要操作的列表键值。 
- 返回： 被移除的数量

### `$vs.redis.exists($key:string):boolean`
- 说明： 判断是否存在指定的键值。 
- 参数： $key:string: 需要操作的列表键值。 
- 返回： 无

### `$vs.redis.expire($key:string,$timeout:int):boolean`
- 说明： 设置键的生存时间。 
- 参数： $key:string: 需要操作的列表键值。 $timeout:int: 生存时间（从当时间算起)，秒。 
- 返回： 无

### `$vs.redis.expireAt($key:string,$time:date):boolean`
- 说明： 设置键的生存时间。 
- 参数： $key:string: 需要操作的列表键值。 $time:date: 失效时间。 
- 返回： 无

### `$vs.redis.get($key:string):string`
- 说明： 获取redis中的数据（字符串返回) 
- 参数： $key:string: 数据键值。 
- 返回： 数据字符串

### `$vs.redis.getBean($key:string):object`
- 说明： 获取redis中的数据 
- 参数： $key:string: 数据键值。 
- 返回： 数据对象

### `$vs.redis.getset($key:string,$value:object):string`
- 说明： 获取redis中的数据，并设置新的数据 
- 参数： $key:string: 数据键值。 $value:string: 新的数据，只接受字符串和数字，若要存放对象请调用getsetBean方法。 
- 返回： 数据字符串

### `$vs.redis.getsetBean($key:string,$value:object):object`
- 说明： 获取redis中的数据，并设置新的数据 
- 参数： $key:string: 数据键值。 $value:string: 新的数据。 
- 返回： 数据对象

### `$vs.redis.hdel($key:string,$field:string):int`
- 说明： 从hash表中删除数据。 
- 参数： $key:string: 需要操作的hash表的键值。 $field:string: hash表的字段键值。 
- 返回： 被成功删除字段的数量，不包括被忽略的字段。

### `$vs.redis.hdelBean($key:string,$field:string):int`
- 说明： 从hash表中删除数据。 
- 参数： $key:string: 需要操作的hash表的键值。 $field:string: hash表的字段键值。 
- 返回： 无

### `$vs.redis.hexists($key:string,$field:string):boolean`
- 说明： 查看哈希表 key 中，指定的字段是否存在。 
- 参数： $key:string: 需要操作的hash表的键值。 $field:string: hash表的字段键值。 
- 返回： 返回键值是否存在

### `$vs.redis.hexistsBean($key:string,$field:string):int`
- 说明： 查看哈希表 key 中，指定的字段是否存在。 
- 参数： $key:string: 需要操作的hash表的键值。 $field:string: hash表的字段键值。 
- 返回： 无

### `$vs.redis.hget($key:string,$field:string):string`
- 说明： 从hash表中获取数据。 
- 参数： $key:string: 需要操作的hash表的键值。 $field:string: hash表的字段键值。 
- 返回： key对应的字符串

### `$vs.redis.hgetAll($key:string):map`
- 说明： 获取在哈希表中指定 key 的所有字段和值。 
- 参数： $key:string: 需要操作的hash表的键值。 
- 返回： 返回所有数据

### `$vs.redis.hgetAllBean($key:string):map`
- 说明： 获取在哈希表中指定 key 的所有字段和值。 
- 参数： $key:string: 需要操作的hash表的键值。 
- 返回： 无

### `$vs.redis.hgetBean($key:string,$field:string):object`
- 说明： 从hash表中获取数据。 
- 参数： $key:string: 需要操作的hash表的键值。 $field:string: hash表的字段键值。 
- 返回： key对应的对象

### `$vs.redis.hkeys($key:string):List<String>`
- 说明： 获取所有哈希表中的字段。 
- 参数： $key:string: 需要操作的hash表的键值。 
- 返回： 返回hash表中的键值列表

### `$vs.redis.hkeysBean($key:string):List<string>`
- 说明： 获取所有哈希表中的字段。 
- 参数： $key:string: 需要操作的hash表的键值。 
- 返回： hash表中的键值列表

### `$vs.redis.hlen($key:string):int`
- 说明： 获取哈希表中字段的数量。 
- 参数： $key:string: 需要操作的hash表的键值。 
- 返回： 返回字段数

### `$vs.redis.hlenBean($key:string):int`
- 说明： 获取哈希表中字段的数量。 
- 参数： $key:string: 需要操作的hash表的键值。 
- 返回： 无

### `$vs.redis.hmget($key:string,$fields:List<string):List<String>`
- 说明： 获取所有给定字段的值。 
- 参数： $key:string: 需要操作的hash表的键值。 $fields:string: 需要查询的字段列表。 
- 返回： 对应的字符串列表

### `$vs.redis.hmgetBean($key:string,$fields:List<string):List<object>`
- 说明： 获取所有给定字段的值。 
- 参数： $key:string: 需要操作的hash表的键值。 $fields:string: 需要查询的字段列表。 
- 返回： 对应的对象列表

### `$vs.redis.hmset($key:string,$value:map<string,object>):void`
- 说明： hash表多值设置。 
- 参数： $key:string: 需要操作的hash表的键值。 $value:Map: 需要添加到hash表的数据。 
- 返回： 无

### `$vs.redis.hmsetBean($key:string,$value:map<string,object>):void`
- 说明： hash表多值设置。 
- 参数： $key:string: 需要操作的hash表的键值。 $value:Map: 需要添加到hash表的数据。 
- 返回： 无

### `$vs.redis.hset($key:string,$field:string,$value:object):int`
- 说明： 将哈希表 key 中的字段 field 的值设为 value 。 
- 参数： $key:string: 需要操作的hash表的键值。 $field:string: hash表的字段键值。 $value:string: 需要存放的值，只接受字符串和数字，若需要设置Bean，则调用`hsetBean`。 
- 返回： 如果字段是哈希表中的一个新建字段，并且值设置成功，返回 1 。 如果哈希表中域字段已经存在且旧值已被新值覆盖，返回 0

### `$vs.redis.hsetBean($key:string,$field:string,$value:object):int`
- 说明： 将哈希表 key 中的字段 field 的值设为 value 。 
- 参数： $key:string: 需要操作的hash表的键值。 $field:string: hash表的字段键值。 $value:string: 需要存放的值。 
- 返回： 无

### `$vs.redis.hsetnx($key:string,$field:string,$value:object):int`
- 说明： 将哈希表 key 中的字段 field 的值设为 value (只有在字段 field 不存在时，设置哈希表字段的值)。 
- 参数： $key:string: 需要操作的hash表的键值。 $field:string: hash表的字段键值。 $value:string: 需要存放的值，只接受字符串和数字，若需要设置Bean，则调用`hsetnxBean`。 
- 返回： 设置成功，返回 1 。 如果给定字段已经存在且没有操作被执行，返回 0 。

### `$vs.redis.hsetnxBean($key:string,$field:string,$value:object):int`
- 说明： 将哈希表 key 中的字段 field 的值设为 value (只有在字段 field 不存在时，设置哈希表字段的值)。 
- 参数： $key:string: 需要操作的hash表的键值。 $field:string: hash表的字段键值。 $value:string: 需要存放的值。 
- 返回： 无

### `$vs.redis.hvals($key:string):List<String>`
- 说明： 获取所有值。 
- 参数： $key:string: 需要操作的hash表的键值。 
- 返回： 对应的字符串列表

### `$vs.redis.hvalsBean($key:string):List<object>`
- 说明： 获取所有值。 
- 参数： $key:string: 需要操作的hash表的键值。 
- 返回： 对应的对象列表

### `$vs.redis.incr($key:string,$i:int):long`
- 说明： 将 key 中储存的数字值加`$i` 
- 参数： $key:string: 数据键值。 $i:string: 增加的数字。 
- 返回： 执行命令之后 key 的值。

### `$vs.redis.incr($key:string):long`
- 说明： 将 key 中储存的数字值加`$i` 
- 参数： $key:string: 数据键值。 
- 返回： 执行命令之后 key 的值。

### `$vs.redis.lindex($key:string,$index:long):string`
- 说明： 通过索引获取列表中的元素。 
- 参数： $key:string: 需要操作的列表键值。 $index:int: 列表索引位置。 
- 返回： 对应的字符串值

### `$vs.redis.lindexBean($key:string,$index:long):object`
- 说明： 通过索引获取列表中的元素。 
- 参数： $key:string: 需要操作的列表键值。 $index:int: 列表索引位置。 
- 返回： 对应的对象值

### `$vs.redis.llen($key:string):long`
- 说明： 获取列表长度。 
- 参数： $key:string: 需要操作的列表键值。 
- 返回： 列表长度

### `$vs.redis.llenBean($key:string):long`
- 说明： 获取列表长度。 
- 参数： $key:string: 需要操作的列表键值。 
- 返回： 列表长度

### `$vs.redis.lpop($key:string):string`
- 说明： 移出并获取列表的第一个元素。 
- 参数： $key:string: 需要操作的列表键值。 
- 返回： 对应的字符串值

### `$vs.redis.lpopBean($key:string):object`
- 说明： 移出并获取列表的第一个元素。 
- 参数： $key:string: 需要操作的列表键值。 
- 返回： 对应的对象值

### `$vs.redis.lpush($key:string,$value:object):long`
- 说明： 将一个值插入到列表头部。 
- 参数： $key:string: 需要操作的列表键值。 $value:string: 需要操作的值，只接受字符串和数字，若需要设置Bean，则调用`lpushBean`。 
- 返回： 执行 LPUSH 命令后，列表的长度。

### `$vs.redis.lpushBean($key:string,$value:object):long`
- 说明： 将一个值插入到列表头部。 
- 参数： $key:string: 需要操作的列表键值。 $value:string: 需要操作的值。 
- 返回： 无

### `$vs.redis.lpushx($key:string,$value:object):long`
- 说明： 将一个值插入到已存在的列表头部。如果列表不存在，操作无效。 
- 参数： $key:string: 需要操作的列表键值。 $value:string: 需要操作的值，只接受字符串和数字，若需要设置Bean，则调用`lpushBean`。 
- 返回： LPUSHX 命令执行之后，列表的长度。

### `$vs.redis.lpushxBean($key:string,$value:object):long`
- 说明： 将一个值插入到已存在的列表头部。 
- 参数： $key:string: 需要操作的列表键值。 $value:string: 需要操作的值。 
- 返回： 无

### `$vs.redis.lrange($key:string,$start:long,$stop:long):List<string>`
- 说明： 获取列表指定范围内的元素。 
- 参数： $key:string: 需要操作的列表键值。 $start:long: 索引开始位。 $stop:long: 索引结束位。 
- 返回： 指定的列表

### `$vs.redis.lrangeBean($key:string,$start:long,$stop:long):List<object>`
- 说明： 获取列表指定范围内的元素。 
- 参数： $key:string: 需要操作的列表键值。 $start:long: 索引开始位。 $stop:long: 索引结束位。 
- 返回： 指定的对象列表

### `$vs.redis.mget($keys:List<string>):List<string>`
- 说明： 获取redis中的多个指定键值的数据 
- 参数： $keys:List: 需要的返回的键值。 
- 返回： 字符串列表

### `$vs.redis.mgetBean($keys:List<string>):List<object>`
- 说明： 获取redis中的多个指定键值的数据 
- 参数： $keys:List: 需要的返回的键值。 
- 返回： 对象列表

### `$vs.redis.persist($key:string):boolean`
- 说明： 移除指定KEY的生存时间 
- 参数： $key:string: 需要操作的列表键值。 
- 返回： 无

### `$vs.redis.rename($oldKey:string,$newKey:string)`
- 说明： 重命名KEY(当 newkey 已经存在时， RENAME 命令将覆盖旧值。) 
- 参数： $oldKey:string: 原键名。 $newKey:string: 新键名。 
- 返回： 无

### `$vs.redis.renameNx($oldKey:string,$newKey:string):long`
- 说明： 当且仅当 newkey 不存在时，将 key 改名为 newkey 。 
- 参数： $oldKey:string: 原键名。 $newKey:string: 新键名。 
- 返回： 被修改的数

### `$vs.redis.rpop($key:string):string`
- 说明： 移除列表的最后一个元素，返回值为移除的元素。 
- 参数： $key:string: 需要操作的列表键值。 
- 返回： 对应的字符串值

### `$vs.redis.rpopBean($key:string):object`
- 说明： 移除列表的最后一个元素，返回值为移除的元素。 
- 参数： $key:string: 需要操作的列表键值。 
- 返回： 对应的对象值

### `$vs.redis.rpush($key:string,$value:object):long`
- 说明： 在列表尾部中添加一个值。 
- 参数： $key:string: 需要操作的列表键值。 $value:string: 需要操作的值，只接受字符串和数字，若需要设置Bean，则调用`rpushBean`。 
- 返回： 执行 RPUSH 操作后，列表的长度。

### `$vs.redis.rpushBean($key:string,$value:object):long`
- 说明： 在列表尾部中添加一个值。 
- 参数： $key:string: 需要操作的列表键值。 $value:string: 需要操作的值。 
- 返回： 无

### `$vs.redis.rpushx($key:string,$value:object):long`
- 说明： 在列表尾部中添加一个值。如果列表不存在，操作无效。 
- 参数： $key:string: 需要操作的列表键值。 $value:string: 需要操作的值，只接受字符串和数字，若需要设置Bean，则调用`rpushxBean`。 
- 返回： 执行 RPUSHX 操作后，列表的长度。

### `$vs.redis.rpushxBean($key:string,$value:object):long`
- 说明： 在列表尾部中添加一个值。 
- 参数： $key:string: 需要操作的列表键值。 $value:string: 需要操作的值。 
- 返回： 无

### `$vs.redis.set($key:string,$value:object,$timeout):void`
- 说明： 向redis中存入数据 
- 参数： $key:string: 数据键值。 $value:object: 只接受字符串和数字，若要存放对象请调用setBean方法。 $timeout:int: 数据有效时间（秒)。 
- 返回： 无

### `$vs.redis.set($key:string,$value:object):void`
- 说明： 向redis中存入数据 
- 参数： $key:string: 数据键值。 $value:object: 只接受字符串和数字，若要存放对象请调用setBean方法。 
- 返回： 无

### `$vs.redis.setBean($key:string,$value:object,$timeout:int):void`
- 说明： 向缓存添加一个数据（对象)。 
- 参数： $key:string: 需要操作的键值。 $value:object: 数据值。 $timeout:string: 过期时间（秒)，缺省为永不过期。 
- 返回： 无

### `$vs.redis.setnx($key:string,$value:object):boolean`
- 说明： 将 key 的值设为 value ，当且仅当 key 不存在。 
- 参数： $key:string: 需要操作的键值。 $value:object: 需要设置的数据，只接受字符串和数字，若需要设置Bean，则调用`setnxBean`。 
- 返回： 锁定状态

### `$vs.redis.setnxBean($key:string,$value:object):boolean`
- 说明： 将 key 的值设为 value ，当且仅当 key 不存在。 
- 参数： $key:string: 需要操作的键值。 $value:object: 需要设置的数据。 
- 返回： 无

### `$vs.redis.setrange($key:string,$value:object,$offset:int):long`
- 说明： 用 value 参数覆写(overwrite)给定 key 所储存的字符串值，从偏移量 offset 开始。 
- 参数： $key:string: 需要操作的键值。 $value:object: 需要设置的数据，只接受字符串和数字。 $offset:int: 偏移量。 
- 返回： 返回数量

### `$vs.redis.strlen($key:string):boolean`
- 说明： 返回 key 所储存的字符串值的长度。 
- 参数： $key:string: 需要操作的键值。 
- 返回： key对应的数据长度

### `$vs.redis.ttl($key:string):long`
- 说明： 查询KEY的剩余有效时间。 
- 参数： $key:string: 需要操作的列表键值。 
- 返回： 键对应的有效时间（秒)返回0代表为永久有效

## $vs.regexp - 正则表达式操作对象(15 methods)

### `$vs.regexp.findAll($str:string,$exp:string,$groupIndex:int):list<string>`
- 说明： 通过正则表达式查找所有符合规则的字符串 
- 参数： $str:string: 被查找的字符串。 $exp:string: 正则表达式，如：[a-z]+。 $groupIndex:int: 正则分组，默认null。 
- 返回： 所有符合规则的字符串列表

### `$vs.regexp.findAll($str:string,$exp:string):list<string>`
- 说明： 通过正则表达式查找所有符合规则的字符串 
- 参数： $str:string: 被查找的字符串。 $exp:string: 正则表达式，如：[a-z]+。 
- 返回： 所有符合规则的字符串列表

### `$vs.regexp.findAllIgnore($str:string,$exp:string,$groupIndex:int):list<string>`
- 说明： 通过正则表达式查找所有符合规则的字符串（不区分大小写） 
- 参数： $str:string: 被查找的字符串。 $exp:string: 正则表达式，如：[a-z]+。 $groupIndex:int: 正则分组，默认null。 
- 返回： 所有符合规则的字符串列表

### `$vs.regexp.findAllIgnore($str:string,$exp:string):list<string>`
- 说明： 通过正则表达式查找所有符合规则的字符串（不区分大小写） 
- 参数： $str:string: 被查找的字符串。 $exp:string: 正则表达式，如：[a-z]+。 
- 返回： 所有符合规则的字符串列表

### `$vs.regexp.findFirst($str:string,$exp:string,$groupIndex:int):string`
- 说明： 通过正则表达式查找第一次出现的符合规则的字符串 
- 参数： $str:string: 被查找的字符串。 $exp:string: 正则表达式，如：[a-z]+。 $groupIndex:int: 正则分组，默认null。 
- 返回： 第一次出现的符合规则的字符串，若没有符合表达式的字符串，则返回`null`

### `$vs.regexp.findFirst($str:string,$exp:string):string`
- 说明： 通过正则表达式查找第一次出现的符合规则的字符串 
- 参数： $str:string: 被查找的字符串。 $exp:string: 正则表达式，如：[a-z]+。 
- 返回： 第一次出现的符合规则的字符串，若没有符合表达式的字符串，则返回`null`

### `$vs.regexp.findFirstIgnore($str:string,$exp:string,$groupIndex:int):string`
- 说明： 通过正则表达式查找第一次出现的符合规则的字符串（不区分大小写） 
- 参数： $str:string: 被查找的字符串。 $exp:string: 正则表达式，如：[a-z]+。 $groupIndex:int: 正则分组，默认null。 
- 返回： 第一次出现的符合规则的字符串，若没有符合表达式的字符串，则返回`null`

### `$vs.regexp.findFirstIgnore($str:string,$exp:string):string`
- 说明： 通过正则表达式查找第一次出现的符合规则的字符串（不区分大小写） 
- 参数： $str:string: 被查找的字符串。 $exp:string: 正则表达式，如：[a-z]+。 
- 返回： 第一次出现的符合规则的字符串，若没有符合表达式的字符串，则返回`null`

### `$vs.regexp.match($str:string,$exp:string):Matcher`
- 说明： 调用java的正则匹配命令，返回java正则匹配结果对象 
- 参数： $str:string: 被查找的字符串。 $exp:string: 正则表达式，如：[a-z]+。 
- 返回： java正则结果匹配对象

### `$vs.regexp.matchIgnore($str:string,$exp:string):Matcher`
- 说明： 调用java的正则匹配命令，返回java正则匹配结果对象 
- 参数： $str:string: 被查找的字符串。 $exp:string: 正则表达式，如：[a-z]+。 
- 返回： java正则结果匹配对象

### `$vs.regexp.replaceAll($str:string,$exp:string,$newstr:string):string`
- 说明： 通过正则表达式替换所有符合规则的字符串 
- 参数： $str:string: 被查找的字符串。 $exp:string: 正则表达式，如：[a-z]+。 $newstr:string: 需要被替换的字符串。 
- 返回： 替换后的字符串

### `$vs.regexp.replaceAllIgnore($str:string,$exp:string,$newstr:string):string`
- 说明： 通过正则表达式替换所有符合规则的字符串（不区分大小写） 
- 参数： $str:string: 被查找的字符串。 $exp:string: 正则表达式，如：[a-z]+。 $newstr:string: 需要被替换的字符串。 
- 返回： 替换后的字符串

### `$vs.regexp.replaceFirst($str:string,$exp:string,$newstr:string):string`
- 说明： 通过正则表达式替换第一次出现的符合规则的字符串 
- 参数： $str:string: 被查找的字符串。 $exp:string: 正则表达式，如：[a-z]+。 $newstr:string: 需要被替换的字符串。 
- 返回： 替换后的字符串

### `$vs.regexp.replaceFirstIgnore($str:string,$exp:string,$newstr:string):string`
- 说明： 通过正则表达式替换第一次出现的符合规则的字符串（不区分大小写） 
- 参数： $str:string: 被查找的字符串。 $exp:string: 正则表达式，如：[a-z]+。 $newstr:string: 需要被替换的字符串。 
- 返回： 替换后的字符串

### `$vs.regexp.replaceRegExValue($str:string):string`
- 说明： 特殊字符串转译 
- 参数： $str:string: 需转译的字符串。 
- 返回： 转译后的字符串

## $vs.report - 报表导出文件对象(8 methods)

### `$vs.report.createPdfTextWaterMark($pdfPath:string,$text:string,$fontSize:Integer,$isFullTile:boolean,$startPageNo:int,$fontName:string):void`
- 说明： 为指定PDF文件添加文字水印 
- 参数： $pdfPath:string: 需要添加水印的PDF文件路径，如：/a0c/b3e/file.pdf，可以是本地临时文件路径、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 $text:string: 水印文字。 $fontSize:Integer: 文字大小，可缺省，默认：26。 $isFullTile:boolean: 水印是否平铺。true - 平铺（默认）； false - 每页一个水印，居中。 $startPageNo:int: 开始页数，从1开始，如：要跳过第一页，则设置为 2。 $fontName:string: 字体，默认：STSong-Light，中文字体必须在服务器操作系统上存在，否则中心不会显示。 
- 返回： 无

### `$vs.report.createPictureImageWaterMark($imagePath:string,$iconPath:string,$x:int,$y:int):void`
- 说明： 为指定图片添加图标水印 
- 参数： $imagePath:string: 需要添加水印的图片路径，如：/a0c/b3e/image.png，可以是本地临时文件路径、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 $iconPath:string: 水印图标路径，如：/a0c/b3e/image.png，可以是本地临时文件路径、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 $x:int: 水印图片左上角横坐标，单位像素，可缺省，默认：10。 $y:int: 水印图片左上角纵坐标，单位像素，可缺省，默认：10。 
- 返回： 无

### `$vs.report.createPictureTextWaterMark($imagePath:string,$text:string,$x:int,$y:int,$color:string,$fontSize:int,$fontName:string,$a:int):void`
- 说明： 为指定图片添加文字水印 
- 参数： $imagePath:string: 需要添加水印的图片路径，如：/a0c/b3e/image.png，可以是本地临时文件路径、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 $text:string: 水印文字。 $x:int: 文字横坐标，单位像素，可缺省，默认：10。 $y:int: 文字纵坐标，单位像素，可缺省，默认：10。 $color:string: 文字颜色，使用HTML颜色表达式（16进制字符串），如：ffffff表示白色，可缺省，默认：黑色。 $fontSize:int: 文字大小（不可小于6像素），可缺省，默认：14。 $fontName:string: 字体名称，如：宋体，可缺省，默认：操作系统默认字体。 $a:int: 文字透明度，值范围[1-255]，1近乎透明；255完全不透明，可缺省，默认：255。 
- 返回： 无

### `$vs.report.exportDataToExcel($datas:List<Map<String, Object>>,$titles:List<Map<String, Object>>):string`
- 说明： 导出数据到Excel临时文件 
- 参数： $datas:List >: 数据列表。 $titles:List>: 标题列表Map -> {width:100,fieldId:"BILL_CODE",format:"#,##0.00",align:"left",dataType:"VARCHAR",label:"单据号码"}。 
- 返回： excel临时文件，用完后，请删除此文件

### `$vs.report.exportToExcel($reportId:string,$params:Map):string`
- 说明： 导出报表数据为EXCEL 
- 参数： $reportId:string: 报表编码。 $params:Map: 报表查询条件。 
- 返回： 返回文件在本地（应用服务器）上的保存路径，这个路径是临时路径，请调用文件服务API`$vs.file.xxx`上传到文件服务器，否则过期文件会被清理

### `$vs.report.exportToPDF($reportId:string,$params:Map):string`
- 说明： 导出报表数据为PDF 
- 参数： $reportId:string: 报表编码。 $params:Map: 报表查询条件。 
- 返回： 返回文件在本地（应用服务器）上的保存路径，这个路径是临时路径，请调用文件服务API`$vs.file.xxx`上传到文件服务器，否则过期文件会被清理

### `$vs.report.mergePdfFile($files:List<String>):string`
- 说明： 合并指定文件为单一PDF文件 
- 参数： $files:List: 需要合并的文件列表，至少要2个以上的文件，文件类型支持PDF和DOCX；文件存储方式支持：本地临时文件路径、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 
- 返回： PDF临时文件，用完后，请删除此文件

### `$vs.report.wordToPdf($wordFilePath:string):string`
- 说明： word转pdf 
- 参数： $wordFilePath:string: word文件路径，可以是本地临时文件路径、本地文件路径、文件服务器上的共有路径、文件服务器上的私有路径。 
- 返回： 返回文件在本地（应用服务器）上的保存路径，这个路径是临时路径，请调用文件服务API`$vs.file.xxx`上传到文件服务器，否则过期文件会被清理

## $vs.request - http request 原生对象(23 methods)

### `$vs.request.getAttribute($name:string):object`
- 说明： 获取用户存放在request中的属性[原生方法] 
- 参数： $name:string: key值。 
- 返回： 用户存放的对象

### `$vs.request.getCharacterEncoding():string`
- 说明： 获取本次请求体的字符集[原生方法] 
- 参数： 无 
- 返回： 请求字符集

### `$vs.request.getContentLength():int`
- 说明： 获取本次请求体的长度[原生方法] 
- 参数： 无 
- 返回： 请求体长度

### `$vs.request.getContentType():string`
- 说明： 获取本次请求类型[原生方法] 
- 参数： 无 
- 返回： 请求类型

### `$vs.request.getContextPath():string`
- 说明： 获取请求路径信息[原生方法] 
- 参数： 无 
- 返回： --

### `$vs.request.getHeader($name:string):string`
- 说明： 获取请求头信息[原生方法] 
- 参数： $name:string: 键。 
- 返回： 请求头信息

### `$vs.request.getMethod():string`
- 说明： 获取请求头协议[原生方法] 
- 参数： 无 
- 返回： GET, POST, or PUT

### `$vs.request.getParameter($name:string):string`
- 说明： 获取本次请求参数[原生方法] 
- 参数： $name:string: 参数键值。 
- 返回： 请求参数

### `$vs.request.getPathInfo():string`
- 说明： 获取请求路径信息[原生方法] 
- 参数： 无 
- 返回： --

### `$vs.request.getPathTranslated():string`
- 说明： 获取请求路径信息[原生方法] 
- 参数： 无 
- 返回： --

### `$vs.request.getProtocol():string`
- 说明： 获取本次请求协议[原生方法] 
- 参数： 无 
- 返回： 请求协议，如：HTTP/1.1

### `$vs.request.getQueryString():string`
- 说明： 获取请求头参数[原生方法] 
- 参数： 无 
- 返回： 请求参数

### `$vs.request.getRemoteAddr():string`
- 说明： 获取本次请求远程地址（由于请求经过了代理，故此处不一定准确），要获取用户浏览器IP，请使用`$vs.http.getClientIp()`[原生方法] 
- 参数： 无 
- 返回： 客户端IP

### `$vs.request.getRemoteHost():string`
- 说明： 获取本次请求服务[原生方法] 
- 参数： 无 
- 返回： --

### `$vs.request.getRemoteUser():string`
- 说明： 获取请求用户（注意不是谷神用户，此方法一般不需要调用）[原生方法] 
- 参数： 无 
- 返回： --

### `$vs.request.getRequestURI():string`
- 说明： 获取请求地址[原生方法] 
- 参数： 无 
- 返回： 请求地址

### `$vs.request.getScheme():string`
- 说明： 获取本次请求协议（由于请求经过了代理，故此处不一定准确）[原生方法] 
- 参数： 无 
- 返回： 请求协议，如：http,https

### `$vs.request.getServerName():string`
- 说明： 获取本次请求服务名[原生方法] 
- 参数： 无 
- 返回： 服务名

### `$vs.request.getServerPort():string`
- 说明： 获取本次请求服务请求端口（由于请求经过了代理，故此处不一定准确），要获取本地http监听端口，使用`$vs.properties.getProperty("server.port")`[原生方法] 
- 参数： 无 
- 返回： 服务请求端口

### `$vs.request.getServletPath():string`
- 说明： 获取请求地址[原生方法] 
- 参数： 无 
- 返回： 请求地址

### `$vs.request.removeAttribute($name:string):void`
- 说明： 删除request用户对象[原生方法] 
- 参数： $name:string: 键。 
- 返回： 无

### `$vs.request.setAttribute($name:string,$value:object):void`
- 说明： 存放用户对象到request[原生方法] 
- 参数： $name:string: 键。 $value:object: 值。 
- 返回： 无

### `$vs.request.setCharacterEncoding($encoding:string):void`
- 说明： 设置本次请求体的字符集[原生方法] 
- 参数： $encoding:string: 字符集，如： utf-8。 
- 返回： 无

## $vs.response - http response 原生对象(5 methods)

### `$vs.response.addHeader($name:string,$value:string):void`
- 说明： 设置响应头（注意本方法采用追加模式【也就是会存在多个相同键的头】）[原生方法] 
- 参数： $name:string: 键。 $value:string: 值。 
- 返回： 无

### `$vs.response.getHeader($name:string):void`
- 说明： 获取响应头[原生方法] 
- 参数： $name:string: 键。 
- 返回： 无

### `$vs.response.sendRedirect($url:string):void`
- 说明： 重定向到目标地址[原生方法] 
- 参数： $url:string: 目标地址。 
- 返回： 无

### `$vs.response.setHeader($name:string,$value:string):void`
- 说明： 设置响应头（注意本方法采用覆盖模式）[原生方法] 
- 参数： $name:string: 键。 $value:string: 值。 
- 返回： 无

### `$vs.response.setStatus($status:int):void`
- 说明： 设置响应码[原生方法] 
- 参数： $status:int: 响应码，如： 404。 
- 返回： 无

## $vs.service - 插件服务调用对象(1 methods)

### `$vs.service.find($strServiceName:string):service`
- 说明： 查找插件包中的服务或组件 
- 参数： $strServiceName:string: 服务或组件Spring注册编码。 
- 返回： 服务或组件实例

## $vs.sqlTools - SQL条件对象(13 methods)

### `$vs.sqlTools.add($sqlBean:sqlBean,$strSubSql:string):void`
- 说明： 强制添加额外查询条件 
- 参数： $sqlBean:sqlBean: SQL查询对象。 $strSubSql:string: 自定义查询条件，如：AND (FIELD <>0 OR FIELD IS NULL)。 
- 返回： 无

### `$vs.sqlTools.and($sqlBean:sqlBean,$strField:string,$objData:object,$strOpt::string):void`
- 说明： 添加AND查询条件（等值） 
- 参数： $sqlBean:sqlBean: SQL查询对象。 $strField:string: 查询字段名称。 $objData:object: 条件值，任意格式。 $strOpt:string: 操作符，只接受：=、>、>=、<、<=、<>。 
- 返回： 无

### `$vs.sqlTools.and($sqlBean:sqlBean,$strField:string,$objData:object):void`
- 说明： 添加AND查询条件（等值） 
- 参数： $sqlBean:sqlBean: SQL查询对象。 $strField:string: 查询字段名称。 $objData:object: 条件值，任意格式。 
- 返回： 无

### `$vs.sqlTools.date($sqlBean:sqlBean,$strField:string,$strData:string,$strOpt:string):void`
- 说明： 添加日期查询条件，若`$strOpt`为`=`则判断从`00:00:00`到`23:59:59`内的数据 
- 参数： $sqlBean:sqlBean: SQL查询对象。 $strField:string: 查询字段名称。 $strData:string: 日期字符串（不含时间）。 $strOpt:string: 操作符，只接受：=、>、>=、<、<=、<>。 
- 返回： 无

### `$vs.sqlTools.date($sqlBean:sqlBean,$strField:string,$strData:string):void`
- 说明： 添加日期查询条件（等值），判断从`00:00:00`到`23:59:59`内的数据 
- 参数： $sqlBean:sqlBean: SQL查询对象。 $strField:string: 查询字段名称。 $strData:string: 日期字符串（不含时间）。 
- 返回： 无

### `$vs.sqlTools.dateBetween($sqlBean:sqlBean,$strField:string,$strStartDate:string,$strEndDate:string):void`
- 说明： 添加日期区间查询条件 
- 参数： $sqlBean:sqlBean: SQL查询对象。 $strField:string: 查询字段名称。 $strStartDate:string: 开始日期字符串（不含时间），允许为空，空则类似小于等于`$strEndDate`的数据。 $strEndDate:string: 结束日期字符串（不含时间，方法内自动添加`23:59:59`的时间标记），允许为空，空则类似大于等于`$strStartDate`的数据。 
- 返回： 无

### `$vs.sqlTools.in($sqlBean:sqlBean,$strField:string,$listValues:List<string>):void`
- 说明： 添加`AND IN`查询条件 
- 参数： $sqlBean:sqlBean: SQL查询对象。 $strField:string: 查询字段名称。 $listValues:List : IN值范围列表（List类型）。 
- 返回： 无

### `$vs.sqlTools.leftLike($sqlBean:sqlBean,$strField:string,$strData:string):void`
- 说明： 添加LIKE查询条件`like $strData%`， 如： `$vs.sqlTools.leftLike($sqlBean,"a.MAIN_CODE",$form.MAIN_CODE)` 
- 参数： $sqlBean:sqlBean: SQL查询对象。 $strField:string: 查询字段名称。 $strData:string: 条件值，`like $strData%`。 
- 返回： 无

### `$vs.sqlTools.like($sqlBean:sqlBean,$strField:string,$strData:string):void`
- 说明： 添加LIKE查询条件`like %$strData%`， 如： `$vs.sqlTools.like($sqlBean,"a.MAIN_CODE",$form.MAIN_CODE)` 
- 参数： $sqlBean:sqlBean: SQL查询对象。 $strField:string: 查询字段名称。 $strData:string: 条件值，`like %$strData%`。 
- 返回： 无

### `$vs.sqlTools.notIn($sqlBean:sqlBean,$strField:string,$listValues:List<string>):void`
- 说明： 添加`AND NOT IN`查询条件 
- 参数： $sqlBean:sqlBean: SQL查询对象。 $strField:string: 查询字段名称。 $listValues:List : IN值范围列表（List类型）。 
- 返回： 无

### `$vs.sqlTools.rightLike($sqlBean:sqlBean,$strField:string,$strData:string):void`
- 说明： 添加LIKE查询条件`like %$strData`， 如： `$vs.sqlTools.rightLike($sqlBean,"a.MAIN_CODE",$form.MAIN_CODE)` 
- 参数： $sqlBean:sqlBean: SQL查询对象。 $strField:string: 查询字段名称。 $strData:string: 条件值，`like %$strData`。 
- 返回： 无

### `$vs.sqlTools.strIn($sqlBean:sqlBean,$strField:string,$strValues:string):void`
- 说明： 添加`AND IN`查询条件 
- 参数： $sqlBean:sqlBean: SQL查询对象。 $strField:string: 查询字段名称。 $strValues:string: IN值范围字符串列表（多个以“,”分隔，不需要带上引号）。 
- 返回： 无

### `$vs.sqlTools.strNotIn($sqlBean:sqlBean,$strField:string,$strValues:string):void`
- 说明： 添加`AND NOT IN`查询条件 
- 参数： $sqlBean:sqlBean: SQL查询对象。 $strField:string: 查询字段名称。 $strValues:string: NOT IN值范围字符串列表（多个以“,”分隔，不需要带上引号）。 
- 返回： 无

## $vs.sqlHelper - SQL帮助类(20 methods)

### `$vs.sqlHelper.and($form:Map<string,?>,$strTableFieldId:string,$strDataFieldId:string):string`
- 说明： 添加AND查询条件（等值） 
- 用法： ``` #set($sql= $sql + $vs.sqlHelper.and($form,"CODE_FIELD","DATA_FIELD")) ``` 
- 参数： $form:Map: SQL查询对象。 $strTableFieldId:string: 查询字段名称。 $strDataFieldId:string: $form中对于的值字段名称，可缺省。 
- 返回： 返回AND的sql表达式，如果$form中$strDataFieldId对应的值为空，则返回空字符串

### `$vs.sqlHelper.and($form:Map<string,?>,$strTableFieldId:string):string`
- 说明： 添加AND查询条件（等值） 
- 用法： ``` #set($sql= $sql + $vs.sqlHelper.and($form,"CODE_FIELD")) ``` 
- 参数： $form:Map: SQL查询对象。 $strTableFieldId:string: 查询字段名称。 
- 返回： 返回AND的sql表达式，如果$form中$strTableFieldId对应的值为空，则返回空字符串

### `$vs.sqlHelper.andDate($form:Map<string,?>,$strTableFieldId:string,$strDataFieldId:string,$dateFmt:string):string`
- 说明： 添加日期查询条件 
- 参数： $form:Map: SQL查询对象。 $strTableFieldId:string: 查询字段名称。 $strDataFieldId:string: $form中对于的值字段名称，可缺省。 $dateFmt:string: 日期格式，可缺省。 
- 返回： 返回 `date` 的sql表达式，如果$form中$strDataFieldId对应的值为空，则返回空字符串

### `$vs.sqlHelper.andDate($form:Map<string,?>,$strTableFieldId:string,$strDataFieldId:string):string`
- 说明： 添加日期查询条件 
- 参数： $form:Map: SQL查询对象。 $strTableFieldId:string: 查询字段名称。 $strDataFieldId:string: $form中对于的值字段名称，可缺省。 
- 返回： 返回 `date` 的sql表达式，如果$form中$strDataFieldId对应的值为空，则返回空字符串

### `$vs.sqlHelper.andDate($form:Map<string,?>,$strTableFieldId:string):string`
- 说明： 添加日期查询条件 
- 参数： $form:Map: SQL查询对象。 $strTableFieldId:string: 查询字段名称。 
- 返回： 返回 `date` 的sql表达式，如果$form中$strDataFieldId对应的值为空，则返回空字符串

### `$vs.sqlHelper.andDateBetween($form:Map<string,?>,$strTableFieldId:string,$startDateField:string,$endDateField:string):string`
- 说明： 添加日期区间查询条件 
- 参数： $form:Map: SQL查询对象。 $strTableFieldId:string: 查询字段名称。 $startDateField:string: 开始日期查询字段名称。 $endDateField:string: 结束日期查询字段名称。 
- 返回： 返回 `date` 的sql表达式，如果$form中$strDataFieldId对应的值为空，则返回空字符串``

### `$vs.sqlHelper.andLike($form:Map<string,?>,$strTableFieldId:string,$strDataFieldId:string):string`
- 说明： 添加LIKE查询条件 
- 用法： ``` #set($sql= $sql + $vs.sqlHelper.andLike($form,"CODE_FIELD","DATA_FIELD")) ``` 
- 参数： $form:Map: SQL查询对象。 $strTableFieldId:string: 查询字段名称。 $strDataFieldId:string: $form中对于的值字段名称，可缺省。 
- 返回： 返回 `like` 的sql表达式，如果$form中$strDataFieldId对应的值为空，则返回空字符串

### `$vs.sqlHelper.andLike($form:Map<string,?>,$strTableFieldId:string):string`
- 说明： 添加LIKE查询条件 
- 用法： ``` #set($sql= $sql + $vs.sqlHelper.andLike($form,"CODE_FIELD")) ``` 
- 参数： $form:Map: SQL查询对象。 $strTableFieldId:string: 查询字段名称。 
- 返回： 返回 `like` 的sql表达式，如果$form中$strTableFieldId对应的值为空，则返回空字符串

### `$vs.sqlHelper.buildToNativeSql($sql:string,$dbType:int):string`
- 说明： 编译开发sql为原生sql字符串 
- 参数： $sql:string: SQL字符串。 $dbType:int: 数据库类型，参考： `$vs.dbTools.getDbType()`。 
- 返回： 返回编译后的sql（适配目标数据库的sql）

### `$vs.sqlHelper.buildToNativeSql($sql:string):string`
- 说明： 编译开发sql为原生sql字符串 
- 参数： $sql:string: SQL字符串。 
- 返回： 返回编译后的sql（适配目标数据库的sql）

### `$vs.sqlHelper.date($form:Map<string,?>,$strTableFieldId:string,$strDataFieldId:string,$dateFmt:string):string`
- 说明： 添加日期查询条件 
- 参数： $form:Map: SQL查询对象。 $strTableFieldId:string: 查询字段名称。 $strDataFieldId:string: $form中对于的值字段名称，可缺省。 $dateFmt:string: 日期格式，可缺省。 
- 返回： 返回 `date` 的sql表达式，如果$form中$strDataFieldId对应的值为空，则返回空字符串 `1=1`

### `$vs.sqlHelper.date($form:Map<string,?>,$strTableFieldId:string,$strDataFieldId:string):string`
- 说明： 添加日期查询条件 
- 参数： $form:Map: SQL查询对象。 $strTableFieldId:string: 查询字段名称。 $strDataFieldId:string: $form中对于的值字段名称，可缺省。 
- 返回： 返回 `date` 的sql表达式，如果$form中$strDataFieldId对应的值为空，则返回空字符串 `1=1`

### `$vs.sqlHelper.date($form:Map<string,?>,$strTableFieldId:string):string`
- 说明： 添加日期查询条件 
- 参数： $form:Map: SQL查询对象。 $strTableFieldId:string: 查询字段名称。 
- 返回： 返回 `date` 的sql表达式，如果$form中$strDataFieldId对应的值为空，则返回空字符串 `1=1`

### `$vs.sqlHelper.dateBetween($form:Map<string,?>,$strTableFieldId:string,$startDateField:string,$endDateField:string):string`
- 说明： 添加日期区间查询条件 
- 参数： $form:Map: SQL查询对象。 $strTableFieldId:string: 查询字段名称。 $startDateField:string: 开始日期查询字段名称。 $endDateField:string: 结束日期查询字段名称。 
- 返回： 返回 `date` 的sql表达式，如果$form中$strDataFieldId对应的值为空，则返回空字符串` 1=1 `

### `$vs.sqlHelper.like($form:Map<string,?>,$strTableFieldId:string,$strDataFieldId:string):string`
- 说明： 添加LIKE查询条件 
- 用法： ``` #set($sql= $sql + " and " + $vs.sqlHelper.like($form,"CODE_FIELD","DATA_FIELD")) ``` 
- 参数： $form:Map: SQL查询对象。 $strTableFieldId:string: 查询字段名称。 $strDataFieldId:string: $form中对于的值字段名称，可缺省。 
- 返回： 返回 `like` 的sql表达式，如果$form中$strDataFieldId对应的值为空，则返回空字符串 `1=1`

### `$vs.sqlHelper.like($form:Map<string,?>,$strTableFieldId:string):string`
- 说明： 添加LIKE查询条件 
- 用法： ``` #set($sql= $sql + " and " $vs.sqlHelper.like($form,"CODE_FIELD")) ``` 
- 参数： $form:Map: SQL查询对象。 $strTableFieldId:string: 查询字段名称。 
- 返回： 返回 `like` 的sql表达式，如果$form中$strTableFieldId对应的值为空，则返回空字符串 `1=1`

### `$vs.sqlHelper.listIn($list:List<string>,$strTableFieldId:string):string`
- 说明： 添加IN查询条件 
- 用法： ``` #set($sql= $sql + " and " + $vs.sqlHelper.listIn($list,"CODE_FIELD")) ``` 
- 参数： $list:List: IN数据列表。 $strTableFieldId:string: 查询字段名称。 
- 返回： 返回 IN 的sql表达式，如果$list为空，则返回字符串 ` 1=2 `

### `$vs.sqlHelper.listNotIn($list:List<string>,$strTableFieldId:string):string`
- 说明： 添加 NOT IN查询条件 
- 用法： ``` #set($sql= $sql + " and " + $vs.sqlHelper.listNotIn($list,"CODE_FIELD")) ``` 
- 参数： $list:List: SQL查询对象。 $strTableFieldId:string: 查询字段名称。 
- 返回： 返回 IN 的sql表达式，如果$list为空，则返回空字符串 ` 1=1 `

### `$vs.sqlHelper.strIn($strValues:string,$strTableFieldId:string):string`
- 说明： 添加IN查询条件 
- 用法： ``` #set($sql= $sql + " and " + $vs.sqlHelper.strIn($strValues,"CODE_FIELD")) ``` 
- 参数： $strValues:string: 以“,”分隔的字符串，如：`A123,B345`，元素不需要添加引号。 $strTableFieldId:string: 查询字段名称。 
- 返回： 返回 IN 的sql表达式，如果$strValues为空，则返回空字符串 ` 1=2 `

### `$vs.sqlHelper.strNotIn($strValues:string,$strTableFieldId:string):string`
- 说明： 添加IN查询条件 
- 用法： ``` #set($sql= $sql + " and " + $vs.sqlHelper.strNotIn($strValues,"CODE_FIELD")) ``` 
- 参数： $strValues:string: 以“,”分隔的字符串，如：`A123,B345`，元素不需要添加引号。 $strTableFieldId:string: 查询字段名称。 
- 返回： 返回 IN 的sql表达式，如果$strValues为空，则返回空字符串 ` 1=1 `

## $vs.thread - 异步线程队列对象(10 methods)

### `$vs.thread.get($key:string,$defvalue:object):void`
- 说明： 从线程变量池中拿出变量，若变量不存在，则返回默认值。 
- 参数： $key:string: 变量名称。 $defvalue:object: 变量默认值，可缺省。 
- 返回： 无

### `$vs.thread.get($key:string):void`
- 说明： 从线程变量池中拿出变量，若变量不存在，则返回`null`。 
- 参数： $key:string: 变量名称。 
- 返回： 无

### `$vs.thread.put($key:string,$value:object):void`
- 说明： 将变量放到当前线程变量池中，使得此变量在本次调用中所有代码均可访问（支持跨系统调用链漫游）。 
- 参数： $key:string: 变量名称。 $value:object: 变量值。 
- 返回： 无

### `$vs.thread.run($strProcName:string,$funName:string,$args:Object...):Object`
- 说明： 将一个任务放到异步线程队列等待执行 
- 参数： $strProcName:string: 过程脚本编码。 $funName:string: 过程脚本函数名称。 $args:Object...: 过程脚本函数参数，根据实际情况，这里可以是0-n个参数。 
- 返回： 无

### `$vs.thread.runFutureTask($strProcName:string,$funName:string,$args:Object...):FutureTaskResult`
- 说明： 将一个任务放到异步线程队列等待执行（不参与分布式事务） 
- 参数： $strProcName:string: 过程脚本编码。 $funName:string: 过程脚本函数名称。 $args:Object...: 过程脚本函数参数，根据实际情况，这里可以是0-n个参数。 
- 返回： 返回`FutureTask`对象，可以通过此对象获取线程的返回值

### `$vs.thread.runFutureTaskWithGlobalTrans($strProcName:string,$funName:string,$args:Object...):FutureTaskResult`
- 说明： 将一个任务放到异步线程队列等待执行（参与分布式事务） 
- 参数： $strProcName:string: 过程脚本编码。 $funName:string: 过程脚本函数名称。 $args:Object...: 过程脚本函数参数，根据实际情况，这里可以是0-n个参数。 
- 返回： 返回`FutureTask`对象，可以通过此对象获取线程的返回值

### `$vs.thread.runServiceComp($strCompId:string,$args:Object):Object`
- 说明： 将一个任务放到异步线程队列等待执行，执行服务组件（注意：不支持跨数据库)。 
- 参数： $strCompId:string: 过程脚本编码。 $args:Object: 过程脚本函数名称。 
- 返回： 无

### `$vs.thread.runServiceCompFutureTask($strCompId:string,$args:Object,$isTran:boolean):FutureTaskResult`
- 说明： 将一个任务放到异步线程队列等待执行，执行服务组件（注意：不支持跨数据库)。 
- 参数： $strCompId:string: 过程脚本编码。 $args:Object: 过程脚本函数名称。 $isTran:boolean: 是否参与分布式事务（默认：false）。 
- 返回： 返回`FutureTask`对象，可以通过此对象获取线程的返回值

### `$vs.thread.runServiceCompFutureTask($strCompId:string,$args:Object):FutureTaskResult`
- 说明： 将一个任务放到异步线程队列等待执行，执行服务组件（注意：不支持跨数据库)。 
- 参数： $strCompId:string: 过程脚本编码。 $args:Object: 过程脚本函数名称。 
- 返回： 返回`FutureTask`对象，可以通过此对象获取线程的返回值

### `$vs.thread.sleep($time:long):void`
- 说明： 暂停线程。 
- 参数： $time:long: 暂停时间（毫秒)。 
- 返回： 无

## $vs.user - 当前登录用户(13 in API tree; 11 top-level entries extracted)

### `$vs.user.CW_OPEN_ID - 当前登录用户企业微信openId（允许为空）`

### `$vs.user.DD_USER_ID - 当前登录用户钉钉openId（允许为空）`

### `$vs.user.EMAIL - 当前登录用户电子邮箱（允许为空）`

### `$vs.user.LAST_UP_PASS - 当前登录用户最后修改密码的时间（允许为空）`

### `$vs.user.LOGIN_ID - 当前登录用户登录ID（允许为空）`

### `$vs.user.MEMBER_CODE - 当前用户所属的会员企业代码`

### `$vs.user.MOBILE - 当前登录用户手机号`

### `$vs.user.USER_ID - 当前登录用户代码`

### `$vs.user.USER_NAME - 当前登录用户姓名`

### `$vs.user.USER_TYPE - 当前登录用户用户类型`
当前登录用户用户类型：10 - 操作员 20 - 管理员（会员用户） 30 - 管理员（后台用户）

### `$vs.user.WX_OPEN_ID - 当前登录用户微信openId（允许为空）`

## $vs.user.member - 会员信息类(2 methods)

### `$vs.user.member.MEMBER_CODE - 当前用户所属的会员企业代码`

### `$vs.user.member.MEMBER_NAME - 当前用户所属的会员企业名称`

## $vs.util - 公共工具类对象(88 methods)

### `$vs.util.bytesToString($buffer:byte[],$charset:string):string`
- 说明： 转换字节数组为字符串 
- 参数： $buffer:byte[]: 要转换的字节数组。 $charset:string: 可选，字符串的字符编码，默认UTF-8。 
- 返回： 转换后的字符串

### `$vs.util.bytesToString($buffer:byte[]):string`
- 说明： 转换字节数组为字符串 
- 参数： $buffer:byte[]: 要转换的字节数组。 
- 返回： 转换后的字符串

### `$vs.util.checkInput($obj:object,$tipMsg:string):void`
- 说明： 判断一个对象是否为空（参见：`$vs.util.isNull`），若为空，则抛出信息为`$tipMsg`的异常提示 
- 参数： $obj:object: 判断的对象。 $tipMsg:string: 提示给用户的信息。 
- 返回： 无

### `$vs.util.concat($str1:object,$str2...):string`
- 说明： 字符串拼接（此方法已过时，您可以直接做字符串相加操作） 
- 参数： $str1:string: 字符串。 $str2:...: 不定长字符串参数。 
- 返回： 拼接后`($str1 + $str2 + ...)`的字符串

### `$vs.util.endsWith($str:string,$sub:string,ignoreCase:boolean):boolean`
- 说明： 判断一个字符串是否以另外一个字符串为结尾 
- 参数： $str:string: 需要判断的字符串。 $sub:string: 结尾字符串。 $ignoreCase:boolean: 是否忽略大小写。 
- 返回： 是否以指定的字符串结尾

### `$vs.util.endsWith($str:string,$sub:string):boolean`
- 说明： 判断一个字符串是否以另外一个字符串为结尾 
- 参数： $str:string: 需要判断的字符串。 $sub:string: 结尾字符串。 
- 返回： 是否以指定的字符串结尾

### `$vs.util.equals($str1:string,$str2:string):boolean`
- 说明： 判断两个字符串内容是否相同（区分大小写） 
- 参数： $str1:string: 判断的对象。 $str2:string: 判断的对象。 
- 返回： true - 两个字符串内容相同; false - 两个字符串内容不相同

### `$vs.util.equalsIgnoreCase($str1:string,$str2:string):boolean`
- 说明： 判断两个字符串内容是否相同（不区分大小写） 
- 参数： $str1:string: 判断的对象。 $str2:string: 判断的对象。 
- 返回： true - 两个字符串内容相同; false - 两个字符串内容不相同

### `$vs.util.fill($intlen:int,$fillChar:string):string`
- 说明： 返回重复指定次数的字符串 
- 参数： $intlen:int: 需要重复的次数。 $fillChar:string: 需要重复的字符（string类型）。 
- 返回： 处理后的字符串

### `$vs.util.fillLeft($str:string,$fillChar:string,$intlen:int):string`
- 说明： 对字符串左侧添加新的字符使得原始字符串长度达到给定的长度 
- 参数： $str:string: 原始字符串。 $fillChar:string: 需要重复的字符（string类型）。 $intlen:int: 期望的长度，若原始字符串长度大于等于此值，则直接返回原始字符串。 
- 返回： 处理后的字符串

### `$vs.util.fillRight($str:string,$fillChar:string,$intlen:int):string`
- 说明： 对字符串右侧添加新的字符使得原始字符串长度达到给定的长度 
- 参数： $str:string: 原始字符串。 $fillChar:string: 需要重复的字符（string类型）。 $intlen:int: 期望的长度，若原始字符串长度大于等于此值，则直接返回原始字符串。 
- 返回： 处理后的字符串

### `$vs.util.fromJson($strJson:string):List<?>|Map<string,?>`
- 说明： 将JSON字符串转成对象 
- 参数： $strJson:string: 需要转对象的JSON字符串。 
- 返回： 对象（数组List或者Map）

### `$vs.util.getChar($char:int):string`
- 说明： int转换为ascll字符 
- 参数： $char:int: 0-127整形数字。 
- 返回： 无

### `$vs.util.getMapKeys($map:Map):List`
- 说明： 获取Map里所有键值 
- 参数： $map:Map: 需要处理的对象。 
- 返回： 键值列表

### `$vs.util.getMd5($str:string):string`
- 说明： 产生32位的MD5值（大写） 
- 参数： $str:string: 目标字符串。 
- 返回： 32位长度的16进制字符串（大写）

### `$vs.util.getPYIndexCode($strChinese:string):string`
- 说明： 获取汉字字符串的文字拼音首字母 
- 参数： $strChinese:string: 汉字字符串。 
- 返回： 汉字拼音首字母（大写）

### `$vs.util.getRandomNumber($max:int,$min:int):int`
- 说明： 获取随机数（介于($max-1)和$min间的数字） 
- 参数： $max:int: 最大数。 $min:int: 最小数。 
- 返回： （介于($max-1)和$min间的数字）

### `$vs.util.getRandomNumber($max:int):int`
- 说明： 获取随机数（介于($max-1)和0间的数字） 
- 参数： $max:int: 最大数。 
- 返回： （介于($max-1)和0间的数字）

### `$vs.util.getRandomStr($len:int):string`
- 说明： 获取随机数字符串 
- 参数： $len:int: 获取随机数字符串长度。 
- 返回： 指定位数的随机数字符串（非0开头）

### `$vs.util.getSystemId():string`
- 说明： 获取当前运行环境的系统编码 
- 参数： 无 
- 返回： 系统编码

### `$vs.util.GUID():string`
- 说明： 获取全球唯一码 
- 参数： 无 
- 返回： 返回32位长度的16进制字符串（小写）

### `$vs.util.ifNull($obj:object,$defaultValue:object):object`
- 说明： 判断一个对象是否为空（参见：`$vs.util.isNull`）并返回对应的值 
- 参数： $obj:object: 判断的对象。 $defaultValue:object: 默认值。 
- 返回： 当`$obj`为空，则返回`$defaultValue`；否则返回`$obj`

### `$vs.util.isBlankOne($obj1:object,$objn:...):boolean`
- 说明： 判断所提供的参数中，是否存在至少1个是`null`（或者空字符串）则返回`true` 
- 参数： $str:object: 判断参数，可多个。 
- 返回： 给定的参数是否存在`null`，如果参数是字符串，则空字符串也视为`null`

### `$vs.util.isContain($str:string,$sub:string):boolean`
- 说明： 判断一个字符串是否包含另一个字符串 
- 参数： $str:string: 需要判断的字符串。 $sub:string: 是否包含的字符串。 
- 返回： 是否包含指定的字符串

### `$vs.util.isList($v:object):boolean`
- 说明： 判断一个对象是否为List，若对象值为null，则返回false 
- 参数： $v:object: 需要判断的对象。 
- 返回： 是否为List，true - List false - 不是

### `$vs.util.isMap($v:object):boolean`
- 说明： 判断一个对象是否为Map，若对象值为null，则返回false 
- 参数： $v:object: 需要判断的对象。 
- 返回： 是否为Map，true - Map false - 不是

### `$vs.util.isNotNull($obj:object):boolean`
- 说明： 判断一个对象是否非空，若对象为字符串，则判断是否非空字符串（忽略空白字符） 
- 参数： $obj:object: 需要判断的对象。 
- 返回： `null`或者`空字符串`返回`false`；否则返回`true`

### `$vs.util.isNotZero($num:number):boolean`
- 说明： 判断数字是非为0（或者null） 
- 参数： $num:number: 需要判断的数字。 
- 返回： `0`或者`null`返回`false`；否则返回`true`

### `$vs.util.isNull($obj:object):boolean`
- 说明： 判断一个对象是否为空，若对象为字符串，则判断是否为空字符串（忽略空白字符） 
- 参数： $obj:object: 需要判断的对象。 
- 返回： `null`或者`空字符串`返回`true`；否则返回`false`

### `$vs.util.isNumeric($v:object):boolean`
- 说明： 判断一个对象是否为数字，若对象值为null，则返回false 
- 参数： $v:object: 需要判断的对象。 
- 返回： 是否为数字，true - 数字 false - 不是，注意：若为数字字符串，则返回true

### `$vs.util.isString($v:object):boolean`
- 说明： 判断一个对象是否为字符串，若对象值为null，则返回false 
- 参数： $v:object: 需要判断的对象。 
- 返回： 是否为字符串，true - 字符串 false - 不是

### `$vs.util.isZero($num:number):boolean`
- 说明： 判断数字是否为0（或者null） 
- 参数： $num:number: 需要判断的数字。 
- 返回： `0`或者`null`返回`true`；否则返回`false`

### `$vs.util.leftTrim($str:string):string`
- 说明： 去除左侧不可见字符 
- 参数： $str:string: 要去除的字符串。 
- 返回： 转换后的字符串

### `$vs.util.list2map($list:List<Map>,$fieldId:string):List`
- 说明： List 类型数据转为Map 
- 参数： $list:List: 需要转换的对象。 $fieldId:String: Map对象的主键，如：BILL_CODE。 
- 返回： 转换后的对象

### `$vs.util.listClone($list:List<?>):List<?>`
- 说明： List克隆 
- 参数： $list:List: 源对象（`List`）。 
- 返回： 新的`List`对象

### `$vs.util.listJoin($list<string>:list,$ch:string):string`
- 说明： 把字符串list转成指定分隔符的字符串 
- 参数： $list:list: 字符串数组。 $ch:string: 分隔符。 
- 返回： 拼接后`1,2,3,4,5`的字符串

### `$vs.util.map2list($map:Map):List`
- 说明： 把Map型对象转成List型 
- 参数： $map:Map: 需要转换的对象。 
- 返回： 转换后的对象

### `$vs.util.mapClone($src:Map<string,?>):Map<string,?>`
- 说明： 新建一个对象（`Map`）且将`$src`中的值复制一份到新的对象 
- 参数： $src:Map: 源对象（`Map`）。 
- 返回： 新的`Map`对象

### `$vs.util.mapCopy($src:Map<string,?>,$target:Map<string,?>):Map<string,?>`
- 说明： 将`$src`和`$target`中相同属性的值复制到`$target`中，若`$target`为空，则复制`$src`的所有属性（同）mapClone 
- 参数： $src:Map : 源对象（`Map`）。 $target:Map: 目标对象（`Map`）。 
- 返回： 新的`Map`对象

### `$vs.util.newHashSet():Set<?>`
- 说明： 创建一个对象不可重复的Set列表 
- 参数： 无 
- 返回： Set类型的变量

### `$vs.util.newHashSet($list:List<?>):Set<?>`
- 说明： 创建一个对象不可重复的Set列表 
- 参数： $list:List: 初始化数据（注意：里面的对象不可重复，否则会报异常）。 
- 返回： Set类型的变量

### `$vs.util.newLinkedHashMap():Map<string,?>`
- 说明： 创建一个有序Map类型的变量，一般用于接口或者对变量顺序有要求的场合 
- 参数： 无 
- 返回： Map类型的变量

### `$vs.util.newLinkedHashSet():Set<?>`
- 说明： 创建一个对象不可重复的有序的Set列表 
- 参数： 无 
- 返回： Set类型的变量

### `$vs.util.newLinkedHashSet($list:List<?>):Set<?>`
- 说明： 创建一个对象不可重复的有序的Set列表 
- 参数： $list:List: 初始化数据（注意：里面的对象不可重复，否则会报异常）。 
- 返回： Set类型的变量

### `$vs.util.newList():List<?>`
- 说明： 创建一个List类型的变量 
- 参数： 无 
- 返回： List类型的变量

### `$vs.util.newList($obj...):List<?>`
- 说明： 创建一个List类型的变量 
- 参数： $obj:...: 不定长对象参数。 
- 返回： List类型的变量

### `$vs.util.newMap():Map<string,?>`
- 说明： 创建一个Map类型的变量 
- 参数： 无 
- 返回： Map类型的变量

### `$vs.util.newMap($k:string,$v:object,$k:string,$v:object...):Map<string,?>`
- 说明： 创建一个Map类型的变量，并赋初始值 
- 参数： $k:string: 键。 $v:object: 值。 
- 返回： Map类型的变量

### `$vs.util.numberCompare($num1:number,$num2:number):int`
- 说明： 比较两个数字大小 
- 参数： $num1:number: 被比数。 $num2:number: 比数。 
- 返回： - 当`($num1 < $num2)`时返回`-1` - 当`($num1 = $num2)`时返回`0` - 当`($num1 > $num2)`时返回`1` - 当`$num1`或`$num2`有一个为`null`时返回`-2`

### `$vs.util.numberGUID():long`
- 说明： 获取数字全球唯一码 
- 参数： 无 
- 返回： 返回数字全球唯一编码

### `$vs.util.parseXml($xml:string,$charset:string):XmlNode`
- 说明： 解析XML字符串，用法见http://docs.guthon.com/docs/gdfaas/gdfaas-1d6lr5ttid3i8 
- 参数： $xml:string: 要解析的XML字符串。 $charset:string: 可选，XML字符串的字符编码，默认UTF-8。 
- 返回： 返回XML文档对象XmlNode，

### `$vs.util.parseXml($xml:string):XmlNode`
- 说明： 解析XML字符串，用法见http://docs.guthon.com/docs/gdfaas/gdfaas-1d6lr5ttid3i8 
- 参数： $xml:string: 要解析的XML字符串。 
- 返回： 返回XML文档对象XmlNode，

### `$vs.util.precise($num1:number,$num2:number,$stropt:string,$intScale:int):double`
- 说明： 数字‘+’、‘-’、‘*’、‘/’运算，功能同：`$vs.math.precise` 
- 参数： $num1:number: 被操作数，注意：若数值为`null`，则视为`0`。 $num2:number: 操作数，注意：若数值为`null`，则视为`0`。 $stropt:string: 运算符，须：‘+’、‘-’、‘*’、‘/’之一。 $intScale:int: 期望保留的小数位，仅‘*’、‘/’有效。 
- 返回： 运算后的数字

### `$vs.util.precise($num1:number,$num2:number,$stropt:string):double`
- 说明： 数字‘+’、‘-’、‘*’、‘/’运算，功能同：`$vs.math.precise` 
- 参数： $num1:number: 被操作数，注意：若数值为`null`，则视为`0`。 $num2:number: 操作数，注意：若数值为`null`，则视为`0`。 $stropt:string: 运算符，须：‘+’、‘-’、‘*’、‘/’之一。 
- 返回： 运算后的数字

### `$vs.util.replaceFirst($str:string,$tag:string,$new:string):string`
- 说明： 替换第一次出现的字符串（非正则） 
- 参数： $str:string: 被替换的字符串。 $tag:string: 需要替换的字符串。 $new:string: 替换字符。 
- 返回： 替换后的字符串

### `$vs.util.rightTrim($str:string):string`
- 说明： 去除右侧不可见字符 
- 参数： $str:string: 要去除的字符串。 
- 返回： 转换后的字符串

### `$vs.util.round($num:double,$intScale:int):double`
- 说明： 数字四舍五入 
- 参数： $num:double: 需要操作的数字。 $intScale:int: 保留小数位。 
- 返回： 处理后的数字

### `$vs.util.setToList($set):List<?>`
- 说明： Set列表转List 
- 参数： $set:Set: 数据。 
- 返回： 数组

### `$vs.util.sort($list:List<Map>,$fieldId:string,$order:string):void`
- 说明： 对列表进行排序 
- 参数： $list:List: 需要排序的列表。 $fieldId:string: 需要排序的列表元素Map的字段。 $order:string: 升序还是降序： ASC 升序（默认) DESC 降序。 
- 返回： 无

### `$vs.util.sort($list:List<Map>,$fieldId:string):void`
- 说明： 对列表进行排序（升序) 
- 参数： $list:List: 需要排序的列表。 $fieldId:string: 需要排序的列表元素Map的字段。 
- 返回： 无

### `$vs.util.sortList($list:List<Object>,$order:string):void`
- 说明： 对基础数据(number,string,date)列表进行排序 
- 参数： $list:List: 需要排序的列表，只能是(number,string,date)类型的数据列表。 $order:string: 升序还是降序： ASC 升序（默认) DESC 降序。 
- 返回： 无

### `$vs.util.sortList($list:List<Object>):void`
- 说明： 对基础数据(number,string,date)列表进行排序 
- 参数： $list:List: 需要排序的列表，只能是(number,string,date)类型的数据列表。 
- 返回： 无

### `$vs.util.split($str:string,$ch:string):List<string>`
- 说明： 根据给定的字符串分隔符，解析字符串 
- 参数： $str:string: 需要解析的字符串。 $ch:string: 字符串分隔符。 
- 返回： 解析后的字符串

### `$vs.util.startScriptRunTimeCount($tagName:string):void`
- 说明： 开启代码运行耗时统计（在代码段（或函数）第一行代码调用），统计本身也会消耗性能，生产环境慎用 
- 参数： $tagName:string: 任意字符串，会输出在日志文件中。 
- 返回： 无

### `$vs.util.startsWith($str:string,$sub:string,ignoreCase:boolean):boolean`
- 说明： 判断一个字符串是否以另外一个字符串为开头 
- 参数： $str:string: 需要判断的字符串。 $sub:string: 开头字符串。 $ignoreCase:boolean: 是否忽略大小写。 
- 返回： 是否以指定的字符串开头

### `$vs.util.startsWith($str:string,$sub:string):boolean`
- 说明： 判断一个字符串是否以另外一个字符串为开头 
- 参数： $str:string: 需要判断的字符串。 $sub:string: 开头字符串。 
- 返回： 是否以指定的字符串开头

### `$vs.util.strLeft($str:string,$len:int):string`
- 说明： 截取字符串左侧$len位长度的字符 
- 参数： $str:string: 要截取的字符串。 $len:int: 要截取的位数，必须大于0。 
- 返回： 截取后的字符串

### `$vs.util.strLen($str:string):int`
- 说明： 获取字符串长度（一个中文占1个长度) 
- 参数： $str:string: 要计算的字符串。 
- 返回： 字符串长度

### `$vs.util.strPos($str:string,$sub:string):int`
- 说明： 判断一个字符串在另外一个字符串中第一次出现的位置（从0开始) 
- 参数： $str:string: 需要判断的字符串。 $sub:string: 是否包含的字符串。 
- 返回： 指定的字符串位置

### `$vs.util.strPosLast($str:string,$sub:string):int`
- 说明： 判断一个字符串在另外一个字符串中最后一次出现的位置（从0开始) 
- 参数： $str:string: 需要判断的字符串。 $sub:string: 是否包含的字符串。 
- 返回： 指定的字符串位置

### `$vs.util.strReplace($str:string,$tag:string,$new:string):string`
- 说明： 替换所有出现的字符串（非正则） 
- 参数： $str:string: 被替换的字符串。 $tag:string: 需要替换的字符串。 $new:string: 替换字符。 
- 返回： 替换后的字符串

### `$vs.util.strReplaceAll($str:string,$tag:string,$new:string):string`
- 说明： 替换所有出现的字符串（支持正则） 
- 参数： $str:string: 被替换的字符串。 $tag:string: 需要替换的字符串。 $new:string: 被替换的字符串。 
- 返回： 替换后的字符串

### `$vs.util.strRight($str:string,$len:int):string`
- 说明： 截取字符串右侧$len位长度的字符 
- 参数： $str:string: 要截取的字符串。 $len:int: 要截取的位数，必须大于0。 
- 返回： 截取后的字符串

### `$vs.util.strToBytes($str:string,$charset:string):byte[]`
- 说明： 转换字符串为字节数组 
- 参数： $str:string: 要转换的字符串。 $charset:string: 可选，字符串的字符编码，默认UTF-8。 
- 返回： 字节数组

### `$vs.util.strToBytes($str:string):byte[]`
- 说明： 转换字符串为字节数组 
- 参数： $str:string: 要转换的字符串。 
- 返回： 字节数组

### `$vs.util.strToDouble($str:string):double`
- 说明： 字符串转小数 
- 参数： $str:string: 需要转换的字符串。 
- 返回： 转换后的数字

### `$vs.util.strToInt($str:string):int`
- 说明： 字符串转数字 
- 参数： $str:string: 需要转换的字符串。 
- 返回： 转换后的数字

### `$vs.util.strToLong($str:string):long`
- 说明： 字符串转long 
- 参数： $str:string: 需要转换的字符串。 
- 返回： 转换后的数字

### `$vs.util.strTrueLen($str:string):int`
- 说明： 获取字符串字节长度（一个中文占2个长度) 
- 参数： $str:string: 要计算的字符串。 
- 返回： 字符串长度

### `$vs.util.substring($str:string,$start:int,$end:int):string`
- 说明： 截取字符串 
- 参数： $str:string: 被截取的字符串。 $start:int: 开始位置（从0开始算起)。 $end:int: 结束位置（从0开始算起)。 
- 返回： 指定位置的字符串

### `$vs.util.substring($str:string,$start:int):string`
- 说明： 截取字符串，从$start到字符串末尾 
- 参数： $str:string: 被截取的字符串。 $start:int: 开始位置（从0开始算起)。 
- 返回： 指定位置的字符串

### `$vs.util.toCamelCase($str:string):string`
- 说明： 字段转驼峰，HELLO_word -> helloWord 
- 参数： $str:string: 需要转的字段。 
- 返回： 驼峰字段

### `$vs.util.toJson($object:object,$isSerializeNulls:boolean):string`
- 说明： 将对象转成JSON字符串 
- 参数： $object:object: 需要转JSON字符串的对象。 $isSerializeNulls:boolean: 是否序列化null值的字段（默认false）。 
- 返回： JSON字符串

### `$vs.util.toJson($object:object):string`
- 说明： 将对象转成JSON字符串 
- 参数： $object:object: 需要转JSON字符串的对象。 
- 返回： JSON字符串

### `$vs.util.toLowerCase($str:string):string`
- 说明： 转换字符串为小写字母 
- 参数： $str:string: 要转换的字符串。 
- 返回： 转换后的字符串

### `$vs.util.toUnderlineCase($str:string):string`
- 说明： 驼峰转字段，helloWord -> HELLO_WORD 
- 参数： $str:string: 需要转的字段。 
- 返回： 字段名称

### `$vs.util.toUpperCase($str:string):string`
- 说明： 转换字符串为大写字母 
- 参数： $str:string: 要转换的字符串。 
- 返回： 转换后的字符串

### `$vs.util.trim($str:string):string`
- 说明： 去掉字符串两边的空白字符（包括空格、tab、回车、换行等） 
- 参数： $str:string: 目标字符串。 
- 返回： 处理后的字符串

## $vs.workflow - 工作流对象(28 methods)

### `$vs.workflow.abstention($userId:string,$billcode:string,$billtypeCode:string,$comment:string,$addSignUserIds:List<String>,$addSignType:Integer,$carbonUserIds:List<String>):AuditNode`
- 说明： 审核弃权 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $comment:string: 审批意见。 $addSignUserIds:List: [可缺省]加签人编码。 $addSignType:Integer: [可缺省]加签人多个的情况下必填，审批类型（1-会签，2-或签）。 $carbonUserIds:Integer: [可缺省]抄送人id列表（审批回调时原值传给业务，一般用于业务回调处理时，发送消息通知给相关人员）。 
- 返回： 流程节点相关信息

### `$vs.workflow.abstention($userId:string,$billcode:string,$billtypeCode:string,$comment:string,$addSignUserIds:List<String>,$addSignType:Integer):AuditNode`
- 说明： 审核弃权 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $comment:string: 审批意见。 $addSignUserIds:List: [可缺省]加签人编码。 $addSignType:Integer: [可缺省]加签人多个的情况下必填，审批类型（1-会签，2-或签）。 
- 返回： 流程节点相关信息

### `$vs.workflow.abstention($userId:string,$billcode:string,$billtypeCode:string,$comment:string):AuditNode`
- 说明： 审核弃权 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $comment:string: 审批意见。 
- 返回： 流程节点相关信息

### `$vs.workflow.activate($userId:string,$billcode:string,$billtypeCode:string,$comment:string)`
- 说明： 激活实例（只能激活手动冻结、复审冻结） 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $comment:string: 审批意见。 
- 返回： 无

### `$vs.workflow.addApprover($userId:string,$billcode:string,$billtypeCode:string,$comment:string,$targetNodeId:string,$addUserIds:List<String>)`
- 说明： 添加审批人（仅限未审的节点，和加签不同，加签是在节点后面增加一个新节点） 
- 参数： $userId:string: 用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $comment:string: 备注。 $targetNodeId:string: 目标节点编码（通过调用 getInstanceInfo 方法获取到流程节点信息）。 $addUserIds:List: 添加人。 
- 返回： 无

### `$vs.workflow.addsign($userId:string,$billcode:string,$billtypeCode:string,$addSignUserId:String)`
- 说明： 加签（单人） 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $addSignUserId:String: 加签人编码。 
- 返回： 无

### `$vs.workflow.addsigns($userId:string,$billcode:string,$billtypeCode:string,$addSignUserIds:List<String>,$addSignType:Integer)`
- 说明： 加签（多人会签） 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $addSignUserIds:List: 加签人编码。 $addSignType:Integer: 加签人多个的情况下必填，审批类型（1-会签，2-或签）。 
- 返回： 无

### `$vs.workflow.approve($userId:string,$billcode:string,$billtypeCode:string,$comment:string,$addSignUserIds:List<String>,$addSignType:Integer,$carbonUserIds:List<String>):AuditNode`
- 说明： 审核同意当前单据 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $comment:string: 审批意见。 $addSignUserIds:List: [可缺省]加签人编码。 $addSignType:Integer: [可缺省]加签人多个的情况下必填，审批类型（1-会签，2-或签）。 $carbonUserIds:Integer: [可缺省]抄送人id列表（审批回调时原值传给业务，一般用于业务回调处理时，发送消息通知给相关人员）。 
- 返回： 流程节点相关信息

### `$vs.workflow.approve($userId:string,$billcode:string,$billtypeCode:string,$comment:string,$addSignUserIds:List<String>,$addSignType:Integer):AuditNode`
- 说明： 审核同意当前单据 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $comment:string: 审批意见。 $addSignUserIds:List: [可缺省]加签人编码。 $addSignType:Integer: [可缺省]加签人多个的情况下必填，审批类型（1-会签，2-或签）。 
- 返回： 流程节点相关信息

### `$vs.workflow.approve($userId:string,$billcode:string,$billtypeCode:string,$comment:string):AuditNode`
- 说明： 审核同意当前单据 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $comment:string: 审批意见。 
- 返回： 流程节点相关信息

### `$vs.workflow.assign($userId:string,$billcode:string,$billtypeCode:string,$comment:string,$targetNodeId:string,$assignId:string,$assignUserIds:List<String>)`
- 说明： 指派审批人（如果都指派了且流程被冻结，则自动激活流程，审批到下个未指派的节点则又被冻结） 
- 参数： $userId:string: 用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $comment:string: 备注。 $targetNodeId:string: 目标节点编码（通过调用 getInstanceInfo 方法获取到流程节点信息）。 $assignId:string: 待指派信息编码（通过调用 getUnassignList 方法获取到待指派信息）。 $assignUserIds:List: 指派人。 
- 返回： 无

### `$vs.workflow.changeMetaData($userId:string,$billcode:string,$billtypeCode:string,$data:Map<string,object>,$meta:Map<string,object>,$remark:string)`
- 说明： 变更流程数据 
- 参数： $userId:string: 操作人。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $data:Map : 业务数据，如：单据主表（用于流程计算时获取变量值，不保存，大小不限）。 $meta:Map: 元数据（参与变量取值，但是优先级小于$data），将会保存到数据，在回调时原值返回，大小要求：JSON序列化后的字符串大小要小于2000字节长度。 $remark:string: 备注。 
- 返回： 无

### `$vs.workflow.changeUserSign($userId:string,$billcode:string,$billtypeCode:string,$newUserId:String,$newUserName:string,$remark:string)`
- 说明： 换人审批 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $newUserId:String: 替换的人。 $newUserName:String: 替换的人姓名。 $remark:String: 备注。 
- 返回： 无

### `$vs.workflow.checkUserCanAudit($userId:string,$billcode:string,$billtypeCode:string):boolean`
- 说明： 判断用户当前节点是否需要审核当前单据 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 
- 返回： `true` - 是的 `false` - 不是

### `$vs.workflow.freeze($userId:string,$billcode:string,$billtypeCode:string,$comment:string)`
- 说明： 主动冻结实例 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $comment:string: 审批意见。 
- 返回： 无

### `$vs.workflow.getInstanceInfo($billcode:string,$billtypeCode:string):AuditInfo`
- 说明： 获取审批流相关信息 
- 参数： $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 
- 返回： 无

### `$vs.workflow.getUnassignList($billcode:string,$billtypeCode:string):List<AssignNode>`
- 说明： 获取待指派节点信息 
- 参数： $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 
- 返回： 无

### `$vs.workflow.invalid($userId:string,$billcode:string,$billtypeCode:string,$comment:string)`
- 说明： 作废（作废已审核通过的流程） 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $comment:string: 审批意见。 
- 返回： 无

### `$vs.workflow.reject($userId:string,$billcode:string,$billtypeCode:string,$comment:string,$targetNodeId:string,$addSignUserIds:List<String>,$addSignType:Integer):AuditNode`
- 说明： 审核拒绝当前单据 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $comment:string: 审批意见。 $targetNodeId:string: [可缺省]回退到目标节点编码（若流程设计时选择了驳回到指定节点，则本参数必填，可以通过调用 getInstanceInfo 方法获取到流程节点信息，并供用户选择）。 $addSignUserIds:List: [可缺省]加签人编码。 $addSignType:Integer: [可缺省]加签人多个的情况下必填，审批类型（1-会签，2-或签）。 
- 返回： 流程节点相关信息

### `$vs.workflow.reject($userId:string,$billcode:string,$billtypeCode:string,$comment:string,$targetNodeId:string):AuditNode`
- 说明： 审核拒绝当前单据 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $comment:string: 审批意见。 $targetNodeId:string: [可缺省]回退到目标节点编码（若流程设计时选择了驳回到指定节点，则本参数必填，可以通过调用 getInstanceInfo 方法获取到流程节点信息，并供用户选择）。 
- 返回： 流程节点相关信息

### `$vs.workflow.reject($userId:string,$billcode:string,$billtypeCode:string,$comment:string):AuditNode`
- 说明： 审核拒绝当前单据 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $comment:string: 审批意见。 
- 返回： 流程节点相关信息

### `$vs.workflow.submit($userId:string,$billcode:string,$billtypeCode:string,$processId:string,$data:Map<string,object>,$meta:Map<string,object>,$remark:string,$content:Map<String, Object>,$files:List<Map<String, Object>>,$nextUserIds:List<String>,$nextSignType:Integer,$systemId:string,$memberCode:string):string`
- 说明： 提交单据到审批工作流，并且指定下级审核人 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $processId:string: 流程模板编码。 $data:Map : 业务数据，如：单据主表（用于流程计算时获取变量值，不保存，大小不限）。 $meta:Map : 元数据（参与变量取值，但是优先级小于$data），将会保存到数据，在回调时原值返回，大小要求：JSON序列化后的字符串大小要小于2000字节长度。 $remark:string: 备注信息。 $content:Map : [可缺省]展示内容，不填不展示，有两种使用模式， 1、动态显示模式（会触发回调过程函数）：`{callback:'com.golden.xxx.callback.funName',files:'com.golden.xxx.callback.fileFunName'}`，获取内容函数[`funName`]参数为：`funName($instanceId, $billCode, $billType, $metaData):Map `，获取附件函数[`fileFunName`]参数为`fileFunName($instanceId, $billCode, $billType, $metaData):List >`，返回数据格式如：[{FILE_NAME:'XX钢厂质保书.docx',FILE_SIZE:'40.23KB',URL:'http://file.xxx.com/upload/xx/xx.docx'}]； 2、静态显示格式如：`{'采购合同主表':{'合同号':'HT202310101001','签订日期':'2023-10-10','采购方':'xxxxx'},'物资明细':[{'品名':'xxx','材质':'Q235','数量':12.34,'单价':5600.00},{...}]}`。 $files:List >: [可缺省]单据附件，不填不展示，格式如：[{FILE_NAME:"XX钢厂质保书.docx",FILE_SIZE:"40.23KB",URL:"http://file.xxx.com/upload/xx/xx.docx"}]。 $nextUserIds:List: [可缺省]指定下级审核人编码。 $nextSignType:Integer: [可缺省]下级审批人多个的情况下必填，审批类型（1-会签，2-或签）。 $systemId:string: [可缺省]单据所在的系统编码，默认：发起当前请求的系统编码。 $memberCode:string: [可缺省]所属往来单位（协同）代码，默认当前操作员所在的单位代码。 
- 返回： 流程实例编码

### `$vs.workflow.submit($userId:string,$billcode:string,$billtypeCode:string,$processId:string,$data:Map<string,object>,$meta:Map<string,object>,$remark:string,$content:Map<String, Object>,$files:List<Map<String, Object>>,$nextUserIds:List<String>,$nextSignType:Integer,$systemId:string):string`
- 说明： 提交单据到审批工作流，并且指定下级审核人 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $processId:string: 流程模板编码。 $data:Map : 业务数据，如：单据主表（用于流程计算时获取变量值，不保存，大小不限）。 $meta:Map : 元数据（参与变量取值，但是优先级小于$data），将会保存到数据，在回调时原值返回，大小要求：JSON序列化后的字符串大小要小于2000字节长度。 $remark:string: 备注信息。 $content:Map : [可缺省]展示内容，不填不展示，有两种使用模式， 1、动态显示模式（会触发回调过程函数）：`{callback:'com.golden.xxx.callback.funName',files:'com.golden.xxx.callback.fileFunName'}`，获取内容函数[`funName`]参数为：`funName($instanceId, $billCode, $billType, $metaData):Map `，获取附件函数[`fileFunName`]参数为`fileFunName($instanceId, $billCode, $billType, $metaData):List >`，返回数据格式如：[{FILE_NAME:'XX钢厂质保书.docx',FILE_SIZE:'40.23KB',URL:'http://file.xxx.com/upload/xx/xx.docx'}]； 2、静态显示格式如：`{'采购合同主表':{'合同号':'HT202310101001','签订日期':'2023-10-10','采购方':'xxxxx'},'物资明细':[{'品名':'xxx','材质':'Q235','数量':12.34,'单价':5600.00},{...}]}`。 $files:List >: [可缺省]单据附件，不填不展示，格式如：[{FILE_NAME:"XX钢厂质保书.docx",FILE_SIZE:"40.23KB",URL:"http://file.xxx.com/upload/xx/xx.docx"}]。 $nextUserIds:List: [可缺省]指定下级审核人编码。 $nextSignType:Integer: [可缺省]下级审批人多个的情况下必填，审批类型（1-会签，2-或签）。 $systemId:string: [可缺省]单据所在的系统编码，默认：发起当前请求的系统编码。 
- 返回： 流程实例编码

### `$vs.workflow.submit($userId:string,$billcode:string,$billtypeCode:string,$processId:string,$data:Map<string,object>,$meta:Map<string,object>,$remark:string,$content:Map<String, Object>,$files:List<Map<String, Object>>,$nextUserIds:List<String>,$nextSignType:Integer):string`
- 说明： 提交单据到审批工作流，并且指定下级审核人 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $processId:string: 流程模板编码。 $data:Map : 业务数据，如：单据主表（用于流程计算时获取变量值，不保存，大小不限）。 $meta:Map : 元数据（参与变量取值，但是优先级小于$data），将会保存到数据，在回调时原值返回，大小要求：JSON序列化后的字符串大小要小于2000字节长度。 $remark:string: 备注信息。 $content:Map : [可缺省]展示内容，不填不展示，有两种使用模式， 1、动态显示模式（会触发回调过程函数）：`{callback:'com.golden.xxx.callback.funName',files:'com.golden.xxx.callback.fileFunName'}`，获取内容函数[`funName`]参数为：`funName($instanceId, $billCode, $billType, $metaData):Map `，获取附件函数[`fileFunName`]参数为`fileFunName($instanceId, $billCode, $billType, $metaData):List >`，返回数据格式如：[{FILE_NAME:'XX钢厂质保书.docx',FILE_SIZE:'40.23KB',URL:'http://file.xxx.com/upload/xx/xx.docx'}]； 2、静态显示格式如：`{'采购合同主表':{'合同号':'HT202310101001','签订日期':'2023-10-10','采购方':'xxxxx'},'物资明细':[{'品名':'xxx','材质':'Q235','数量':12.34,'单价':5600.00},{...}]}`。 $files:List >: [可缺省]单据附件，不填不展示，格式如：[{FILE_NAME:"XX钢厂质保书.docx",FILE_SIZE:"40.23KB",URL:"http://file.xxx.com/upload/xx/xx.docx"}]。 $nextUserIds:List: [可缺省]指定下级审核人编码。 $nextSignType:Integer: [可缺省]下级审批人多个的情况下必填，审批类型（1-会签，2-或签）。 
- 返回： 流程实例编码

### `$vs.workflow.submit($userId:string,$billcode:string,$billtypeCode:string,$processId:string,$data:Map<string,object>,$meta:Map<string,object>,$remark:string,$content:Map<String, Object>,$files:List<Map<String, Object>>):string`
- 说明： 提交单据到审批工作流，并且指定下级审核人 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $processId:string: 流程模板编码。 $data:Map : 业务数据，如：单据主表（用于流程计算时获取变量值，不保存，大小不限）。 $meta:Map : 元数据（参与变量取值，但是优先级小于$data），将会保存到数据，在回调时原值返回，大小要求：JSON序列化后的字符串大小要小于2000字节长度。 $remark:string: 备注信息。 $content:Map : [可缺省]展示内容，不填不展示，有两种使用模式， 1、动态显示模式（会触发回调过程函数）：`{callback:'com.golden.xxx.callback.funName',files:'com.golden.xxx.callback.fileFunName'}`，获取内容函数[`funName`]参数为：`funName($instanceId, $billCode, $billType, $metaData):Map `，获取附件函数[`fileFunName`]参数为`fileFunName($instanceId, $billCode, $billType, $metaData):List >`，返回数据格式如：[{FILE_NAME:'XX钢厂质保书.docx',FILE_SIZE:'40.23KB',URL:'http://file.xxx.com/upload/xx/xx.docx'}]； 2、静态显示格式如：`{'采购合同主表':{'合同号':'HT202310101001','签订日期':'2023-10-10','采购方':'xxxxx'},'物资明细':[{'品名':'xxx','材质':'Q235','数量':12.34,'单价':5600.00},{...}]}`。 $files:List>: [可缺省]单据附件，不填不展示，格式如：[{FILE_NAME:"XX钢厂质保书.docx",FILE_SIZE:"40.23KB",URL:"http://file.xxx.com/upload/xx/xx.docx"}]。 
- 返回： 流程实例编码

### `$vs.workflow.submit($userId:string,$billcode:string,$billtypeCode:string,$processId:string,$data:Map<string,object>,$meta:Map<string,object>,$remark:string):string`
- 说明： 提交单据到审批工作流，并且指定下级审核人 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $processId:string: 流程模板编码。 $data:Map : 业务数据，如：单据主表（用于流程计算时获取变量值，不保存，大小不限）。 $meta:Map: 元数据（参与变量取值，但是优先级小于$data），将会保存到数据，在回调时原值返回，大小要求：JSON序列化后的字符串大小要小于2000字节长度。 $remark:string: 备注信息。 
- 返回： 流程实例编码

### `$vs.workflow.submitCancel($userId:string,$billcode:string,$billtypeCode:string,$reason:string)`
- 说明： 取消提交 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $reason:string: 取消原因。 
- 返回： 无

### `$vs.workflow.terminate($userId:string,$billcode:string,$billtypeCode:string,$comment:string)`
- 说明： 强制中止审批流程 
- 参数： $userId:string: 提交人用户ID。 $billcode:string: 单据号码。 $billtypeCode:string: 标识单据类型的字符串，用于区分不同的单据，建议传值单据类型编码。 $comment:string: 审批意见。 
- 返回： 无
