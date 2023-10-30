# `lf` + `fzf`

[lf](https://github.com/gokcehan/lf) command to change directory using [fzf](https://github.com/junegunn/fzf)

```
cmd fzfdirs ${{

    D=`find -L . -mindepth 1 \\( -path '*/\\.*' -o -fstype 'sysfs' -o -fstype 'devfs' -o -fstype 'devtmpfs' -o -fstype 'proc' \\) -prune -o -type d -print -o -type l -print 2> /dev/null | cut -b3- | fzf -m --preview 'ls -ah {}'`
    if [[ $D == '' ]]; then
        lf -remote "send $id echo fzf aborted."
    else
        lf -remote "send $id cd $D"
    fi
}}

map <c-t> fzfdirs
```

<img src="demo.gif">
