# timelib

PHP & MongoDB 的时间解析库的 CGO wrapper. 主要为了移植 `strtotime` 函数.

## strtotime 文档

https://www.php.net/manual/en/function.strtotime.php
https://www.php.net/manual/en/datetime.formats.php
https://github.com/goghcrow/strtotime

## strtotime 示例

```golang
package timelib

import (
	"testing"
	"time"
)

func Test_Strtotime_Example(t *testing.T) {
	times := []string{
		"now",
		"yesterday",
		"today",
		"tomorrow",
		"noon",
		"midnight",

		"yesterday 08:15pm",
		"yesterday noon",
		"yesterday midnight",
		"tomorrow 18:00",
		"tomorrow moon",

		"+1 week 2 days 4 hours 2 seconds",

		"saturday this week",

		"next year",
		"next month",

		"last day",
		"last wed",

		"this week",
		"next week",
		"last week",
		"previous week",

		"monday",
		"mon",
		"tuesday",
		"tue",
		"wednesday",
		"wed",
		"thursday",
		"thu",
		"friday",
		"fri",
		"saturday",
		"sat",
		"sunday",
		"sun",

		"first day",
		"first day next month",
		"first day of next month",
		"last day next month",
		"last day of next month",
		"last day of april",

		"third Monday December 2020",
		"second Friday Nov 2022",
		"+3 week Thursday Nov 2020",
		"last wednesday of march 2020",

		"2020W30",

		"2020W101T05:00+0",

		"10/22/1990",
		"10/22",
		"01/01",

		"Sun 2020-01-01",
		"Mon 2020-01-02",

		"19970523091528",
		"20001231185859",
		"20800410101010",

		"Fri 2020-01-06",

		"2020-06-25 14:18:48.543728 America/New_York",

		"2020-10-22 13:00:00 Asia/Shanghai",
		"2022-01-01 13:00:00 UTC",
		"2020-01-01 00:00:00 Europe/Rome",

		"2020-11-26T18:51:44+01:00",
		"Thursday, 26-Nov-2020 18:51:44 CET",
		"2020-11-26T18:51:44+0100",
		"Thu, 26 Nov 20 18:51:44 +0100",
		"Thursday, 26-Nov-20 18:51:44 CET",
		"Thu, 26 Nov 2020 18:51:44 +0100",

		"May 18th 2020 5:05pm",
		"2005-8-12",
		"Sat 26th Nov 2020 18:18",
		"26th Nov",
		"Dec. 4th, 2020",
		"December 4th, 2020",
		"Sun, 13 Nov 2020 22:56:10 -0800 (PST)",
		"May 18th 5:05pm",
	}

	for _, it := range times {
		t.Log(time.Unix(Strtotime(it), 0))
	}
}
```

## 平台支持

已经提供了 darwin_amd64、darwin_arm64、linux_amd64 的静态链接，如果需要在其他平台使用，自行编译 timelib 并添加 cgo 链接配置

```go
// strtotime.go

package timelib
/*
#include <stdlib.h>
#include "lib/timelib.h"
#include "strtotime.h"
#cgo darwin,arm64 LDFLAGS: -L./lib -ltimelib_darwin_arm64
#cgo darwin,amd64 LDFLAGS: -L./lib -ltimelib_darwin_amd64
#cgo linux,amd64 LDFLAGS: -L./lib -ltimelib_linux_amd64
*/
import "C"

// ...
```