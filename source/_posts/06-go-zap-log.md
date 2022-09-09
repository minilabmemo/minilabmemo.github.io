---
title: "[Go 07] 使用 zap 框架印出 log"
tags:
  - golang
categories:
  - Tech.
  - back-end
  - golang
date: 2020-05-18T23:51:23+08:00
---

本章內容：

- 實作使用高性能 zap log 框架
- 擁有 log level 配置 (常用 debug/warn/info/error)與程式碼位置
- 可以選擇印出在 console 或是文件（要外掛 lumberjack 去分割）
- zap 有 suger 函式可以增加易用性，但犧牲效能

<!--more-->

> 雖然目前還未有高性能之需求，網路上也有很多不同的ＬＯＧ框架可以選擇，有興趣可以看這篇[在 Github 中 stars 数最多的 Go 日志库集合](https://my.oschina.net/u/168737/blog/1536117 "在Github中stars数最多的Go日志库集合")，看了各框架說明介紹，這個框架實作上看來蠻容易的，今天就還試試看．

直接上實作完之程式碼

```
package logger

import (
	"mywork/demo/internal/config"
	"os"
	"strings"
	"time"
	"go.uber.org/zap"
	"go.uber.org/zap/zapcore"
	"gopkg.in/natefinch/lumberjack.v2"
)


var ZapLogger *zap.Logger
var SugarLogger *zap.SugaredLogger

func InitLogger() {

	logWriter := []zapcore.WriteSyncer{zapcore.AddSync(os.Stdout)}

	if config.Configuration.Logger.File != "" {
		hook := setFileWriter(config.Configuration.Logger.File)
		logWriter = append(logWriter, hook)
	}
	encoderConfig := setEncoder()

	level := getLogLevel(config.Configuration.Logger.Level)

	core := zapcore.NewCore(encoderConfig,
		zapcore.NewMultiWriteSyncer(logWriter...),
		level)

	ZapLogger = zap.New(core, zap.AddCaller()) //印出log的位置
	// ZapLogger.Debug("POK")                     // ZapLogger sample
	ZapLogger.Info("ZapLogger",
		zap.String("String", "ohoh"),
		zap.Int("Int", 3),
		zap.Duration("backoff", time.Second),
	)
	SugarLogger = ZapLogger.Sugar()
	//SugarLogger.Infof("Success! statusCode = %s for URL %s", "OK", "OK")  // SugarLogger sample

}

func setEncoder() zapcore.Encoder {
	encoderConfig := zap.NewProductionEncoderConfig()
	encoderConfig.EncodeTime = zapcore.ISO8601TimeEncoder
	encoderConfig.EncodeLevel = zapcore.CapitalLevelEncoder
	return zapcore.NewConsoleEncoder(encoderConfig)
}

func setFileWriter(filePath string) zapcore.WriteSyncer {
	lumberJackLogger := &lumberjack.Logger{
		Filename:   filePath,
		MaxSize:    1,
		MaxBackups: 5,
		MaxAge:     30,
		Compress:   false,
	}
	return zapcore.AddSync(lumberJackLogger)
}

func getLogLevel(lv string) zapcore.Level {
	lv = strings.ToLower(lv)
	if level, ok := levelMap[lv]; ok {
		return level
	}
	return zapcore.InfoLevel
}

var levelMap = map[string]zapcore.Level{
	"debug":  zapcore.DebugLevel,
	"info":   zapcore.InfoLevel,
	"warn":   zapcore.WarnLevel,
	"error":  zapcore.ErrorLevel,
}



```

LOG 輸出範例

- zap.Logger 輸出需針對 Type 去輸入，使用跟印出看起來都比較麻煩一點
- zap.SugaredLogger 就像是語法糖

```
2021-01-31T11:46:00.954+0800    INFO    log/log.go:27   ZapLogger       {"String": "ohoh", "Int": 3, "backoff": 1}
2021-01-31T11:46:01.012+0800    INFO    http_server/httpserver.go:35    Listening on port: 56888
```
