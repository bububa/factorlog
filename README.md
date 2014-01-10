FactorLog
=========

FactorLog is a logging infrastructure for Go that provides numerous logging functions for whatever your style may be. It could easily be a replacement for Go's log in the standard library (though it doesn't support functions such as `SetFlags()`).

Documentation here: [http://godoc.org/github.com/kdar/factorlog](http://godoc.org/github.com/kdar/factorlog)

## Features

- Various log severities: TRACE, DEBUG, INFO, WARN, ERROR, CRITICAL, STACK, FATAL, PANIC
- Formattable logger.
- Designed with speed in mind.
- Many logging functions to fit your style of logging. (Trace, Tracef, Traceln, etc...)
- Settable verbosity like [glog](https://github.com/golang/glog)
- Used in a production system so it will get some love.

## Motivation

There are many good logging libraries out there but none of them worked the way I wanted them to. For example, some libraries have an API like `log.Info()`, but behind the scenes it's using fmt.Sprintf. What this means is I couldn't do things like `log.Info(err)`. I would instead have to do `log.Info("%s", err.Error())`. This kept biting me as I was coding. In FactorLog, `log.Info` behaves exactly like `fmt.Sprint`. `log.Infof` uses `fmt.Sprintf` and `log.Infoln` uses `fmt.Sprintln`.

I really like [glog](https://github.com/golang/glog), but I don't like that it takes over your command line arguments. I may implement more of its features into FactorLog.

I also didn't want a library that read options from a configuration file. You could easily handle that yourself if you wanted to. FactorLog doesn't include any code for logging to different backends (files, syslog, etc...). The reason for this is I was structuring this after [http://12factor.net/](http://12factor.net/). There are many programs out there that can parse your log output from stdout/stderr and redirect it to the appropriate place. However, FactorLog doesn't prevent you from writing this code yourself.

## Example

You can use the API provided by the package itself just like Go's log does:

```
package main

import (
  log "github.com/kdar/factorlog"
)

func main() {
  log.Println("Hello there!")
}
```

Or, you can make your own log from `FactorLog`:

```
package main

import (
  "github.com/kdar/factorlog"
  "os"
)

func main() {
  log := factorlog.New(os.Stdout, "%D %T %f:%s %M")
  log.Println("Hello there!")
}
```

## Documentation

[http://godoc.org/github.com/kdar/factorlog](http://godoc.org/github.com/kdar/factorlog)