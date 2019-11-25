## cherry-pick

+ (1)git log --oneline -n
  
  找到最近自己分支的提交记录，n表示提交的次数

  ```git
  c87a6cdd yyy
  4029a62e bugfix: xxx
  ```
  
+ (2)git checkout test

  切换到目标分支test

+ (3)git cherry-pick c87a6cdd

+ (4)git 提交三连
  - git add -A

  - git commit -m "提交内容"

  - git push origin test  即可
