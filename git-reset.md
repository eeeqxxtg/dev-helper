## git reset几种使用
+ git add 后退 ：
  ```git
    git reset HEAD
  ```

+ git commit 后退 ：
  ```git
    git reset HEAD^
  ```

+ git pull 后退 ：
  ```git
    git reflog
    
    8909d63d HEAD@{0}: ccc
    837b7690 HEAD@{1}: bbb
    837b7690 HEAD@{2}: aaa
    
    git reset --hard HEAD@{n}
  ```
  
