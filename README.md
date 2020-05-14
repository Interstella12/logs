# logs
写的一个go日志库，支持文件和控制台输出，支持打印日志的文件行和文件名称，支持多颜色显示，支持多级日志分级，支持按时间 分割日志，支持按大小分割日志

# 先来看看例子
```go
package main

import (
	"github.com/xuexihuang/logs"
)
func main() {
	log := logs.NewLogger()
	log.SetLogger(logs.AdapterFile,`{"filename":"project.log","level":7,"maxlines":0,"maxsize":0,"daily":true,"maxdays":10,"color":true}`)
	log.EnableFuncCallDepth(true)//是否打印日志发生的行和文件名
	log.SetLogFuncCallDepth(2)//

	log.Error("this is a error message %s %d ","发生错误，错误码是:",12)
}
```
# 参数说明

filename 保存的文件名
maxlines 每个文件保存的最大行数，默认值 1000000
maxsize 每个文件保存的最大尺寸，默认值是 1 << 28, //256 MB
daily 是否按照每天 logrotate，默认是 true
maxdays 文件最多保存多少天，默认保存 7 天
rotate 是否开启 logrotate，默认是 true
level 日志保存的时候的级别，默认是 Trace 级别
perm 日志文件权限

# 日志级别

LevelEmergency
LevelAlert
LevelCritical
LevelError
LevelWarning
LevelNotice
LevelInformational
LevelDebug
级别依次降低，默认全部打印，但是一般我们在部署环境，可以通过设置级别设置日志级别：
beego.SetLevel(beego.LevelInformational)


