# hanachin/rhg
Dockerfile for reading ruby hacking guide.

## How to run

``` ruby
$ docker pull hanachin/rhg
$ docker run -i -t hanachin/rhg ruby -v
ruby 1.7.3 (2002-09-11) [x86_64-linux]
$ docker run -i -t hanachin/rhg /bin/bash
root@f977c78b7c10:/ruby-rhg# ruby -v
ruby 1.7.3 (2002-09-11) [x86_64-linux]
```
