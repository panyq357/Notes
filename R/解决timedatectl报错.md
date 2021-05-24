# 解决 timedatectl 报错

在 WSL2 的 R 中载入 tidyverse 是，会看到这样的报错。

```
> library(tidyverse)
System has not been booted with systemd as init system (PID 1). Can't operate.
Failed to create bus connection: Host is down
── Attaching packages ────────────────────────────────────────── tidyverse 1.3.0 ──
✓ ggplot2 3.3.3     ✓ purrr   0.3.4
✓ tibble  3.1.0     ✓ dplyr   1.0.5
✓ tidyr   1.1.3     ✓ stringr 1.4.0
✓ readr   1.4.0     ✓ forcats 0.5.1
── Conflicts ───────────────────────────────────────────── tidyverse_conflicts() ──
x dplyr::filter() masks stats::filter()
x dplyr::lag()    masks stats::lag()
Warning message:
In system("timedatectl", intern = TRUE) :
  running command 'timedatectl' had status 1
```

解决方法为终端中执行以下内容。

```bash
echo 'TZ="China/Beijing"' > ~/.Renviron
```

然后就不会报错了。

参考：<https://community.rstudio.com/t/timedatectl-had-status-1/72060/5>