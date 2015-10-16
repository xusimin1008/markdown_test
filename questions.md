## Datartisan ##

1. Analysis是什么时候和Source建立联系的
  通过定时任务来建立联系
2. 对analysis的调用是在哪里
  目测是在celery里
3. 如何对analysis进行定时任务
  1. 遍历所有的project
  2. 对任务执行时间前24小时内有语料更新的项目执行语料分析的定时任务
  3. 把所有需要执行的analysis task罗列出来，分别调用并生产对应的Task
4. 关于如何组织analysis目录
  我觉得可以把celery的配置写成单独文件
  可以把每个celery的task或某一类的task写成单独文件，放到tasks的包里面

  ```
  - analysis
    - celery.py
    - tasks
      - xxx.py
      - zzz.py
    - test
      - test1.py
      - test2.py
    - config.py
    - requirement.txt
  ```
  
这样会使各个task比较独立，方便查看和修改。
尽量把文件分包分类，避免平铺带来的不便。
对于项目的组织，以前也只是尽量遵循规范，自己本身也没考虑太多，以上仅是个人想法。

