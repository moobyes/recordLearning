# git 批量删除分支

批量删除本地分支

git branch -a | grep -v -E 'master|develop' | xargs git branch -D

批量删除远程分支

git branch -r| grep -v -E 'master|develop' | sed 's/origin\///g' | xargs -I {} git push origin :{}

如果有些分支无法删除，是因为远程分支的缓存问题，可以使用git remote prune

批量删除本地tag

git tag | xargs -I {} git tag -d {}

批量删除远程tag

git tag | xargs -I {} git push origin :refs/tags/{}
it show-ref --tag | awk '/(.*)(\s+)(.*)$/ {print ":" $2}' | xargs git push origin

用到命令说明

grep -v -E 排除master 和 develop

-v 排除

-E 使用正则表达式

xargs 将前面的值作为参数传入 git branch -D 后面

-I {} 使用占位符 来构造 后面的命令





git branch -a | grep -v -E 'tang' | xargs git branch -D