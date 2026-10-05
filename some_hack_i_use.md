# a simple tool to run command

add #->command anywhere and it will give you index to invoke it

````zsh
#!/bin/zsh
#->./gradlew test
#->./gradlew :server:run
#->./gradlew :app:desktopApp:run
#->./build-all-artifacts.sh
#->./clean.sh
#->./safe-zip
#->kotlin dist/server/server-1.0.0.jar
#->sudo pacman -U dist/desktop/bin-*-x86_64.pkg.tar.zst
cd "$( dirname -- "${"${(%):-%N}"#"./"}")"
if [[ "$1" == "-i" ]] ; then
eval "$(grep "^ *# *-> *" "${"${(%):-%N}"##*/}" | fzf | sed -e 's/^# *-> *//g' )"
elif (( $# > 0 )) ; then
for index in "$@" ; do
    cmd="$(grep "^ *# *-> _" "${"${(%):-%N}"##_/}" | head -n "$index" | tail -n1 | sed -e 's/^# *-> *//g')"
    echo "$cmd"
eval "$cmd"
  done
else
  grep "^ *# *-> *" "${"${(%):-%N}"##*/}" | sed -e 's/^# *-> *//g' | awk 'BEGIN{ count = 0 }{ count = count + 1 ; print count ":" $0 }'
fi```

````
