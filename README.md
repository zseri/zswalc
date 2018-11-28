# zswalc

Zscheile Web Application Light Chat is an highly insecure,
unreliable, experimental fastcgi-based chatting app,
which utilizes javascript to update the chat view.

## expected paths on webserver
```
/zswebapp with at least the content of the corresponding subdirectory in this repo.
```

## expected environment variables
```
ZSWA_DATADIR="/path/to/chat/files" # should be an existing directory
```

## lighttpd example
```
###############################################################################
# zswebapp.conf
# include'd by lighttpd.conf.
###############################################################################

fastcgi.server += (
  "/chat/" => (
    "localhost" => (
      "socket"    =>  "/run/lighttpd/fastcgi-zschat-" + PID + ".socket",
      "bin-path"  =>  "/usr/src/zswebapp-build/zsfcgi",
      "check-local" => "disable",
      "max-procs" => 1,
      "kill-signal" => 10,
      "bin-environment" => (
        "ZSWA_DATADIR" => "/srv/zschat/main"
      )
    )
  ),
)

alias.url += (
  "/zswebapp" => "/usr/share/zswebapp"
)

# vim: set ft=conf foldmethod=marker et :
```
