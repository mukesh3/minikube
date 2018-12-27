* list alias ```$ alias```  </br>
* temporary alias ```$ alias wr=”cd /var/www/html”``` </br>
* To add alias permanently, add in .bashrc or .bash_aliases </br>
```
$ vim ~/.bashrc
#My custom aliases
alias kc="kubectl”
$ source ~/.bashrc
```
* remove alias ```$ unalias alias_name```</br>
* remove all alias ```$ unalias -a [remove all alias]```

* For setting autocompletion for alias(here kc is the alias), run below command post setting alias:</br>
```echo "source <(kubectl completion bash|sed s/kubectl/kc/g)">>.bashrc```
