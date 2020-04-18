# ASUS TM-AC1900 Arbitrary Command Execution Vulnerability [post-auth :<]

## Root cause
* This is a workaround for [CVE-2018-9285](https://www.cvedetails.com/cve/CVE-2018-9285/). But instead of using characters like backtick and semi-colon since those characters get filtered, the supplied metasploit module leverages the newline character (\x0a) since that character does not get filtered.
* I also only have a TM-AC1900 with me right now, so the supplied metasploit module may work on other ASUS routers.

## Getting code exec

* Achieving code execution took some time since the character `"/"` and the string `"http://"` are filtered. By messing around I found that the supplied `wget` does not require the `"http://"` handler which was a relief. It's also possible to change the current working directory with `cd` and execute shell scripts without an absolute path via `sh script_to_be_executed`.

## Debug Tools

* The supplied binaries within the `debug_tools` will give you the ability to debug applications (`gdb` and `strace`). A dense build of `busybox` is also supplied.
* It also feels like ASUS tried to lock down this device since the ability to launch `telnet` or `ssh` was removed a while ago. >:|

# Mitigations

## Change your default username and password!

* Navigate to `http://cellspot.router`
* Click `Administration`
* Change the values for `Router Login Name`, `New Password`, `Retype New Password`, and click `Apply`.

## Video
[![asciicast](https://asciinema.org/a/2b3jpZErAuq2XTlrPPXMzeZaD.svg)](https://asciinema.org/a/2b3jpZErAuq2XTlrPPXMzeZaD)

[[b1ack0wl]](https://twitter.com/b1ack0wl)