### Migration过程 ###
1. 创建Model: php artisan make:model User
2. 创建迁移脚本: php artisan make:migration create_users_table
3. 往上步的create_users_table里面添加User定义的字段
4. 执行: composer dump-autoload
5. 执行: php artisan migrate (--seed)

### 查看当前laravel的版本 ###
到composer.lock里面查看

### Laravel代码发生项目库启动错误 ###
1. 使用国内数据源: composer config -g repositories.packagist composer http://packagist.phpcomposer.com
2. rm -Rf vendor/ (删除项目库)
3. php composer.phar update -vvv

### Git使用 ###
在git上fork一份代码库（里面包含已存在的分支）

git clone url （克隆远端代码库的master分支）

git checkout -b develop origin/master

git add －A caterory/ （添加指定目录的全部文件，同时删除已删除的文件）

git commit

到github上进行pull request(注意分支的对应，main的develop应该对应origin的develop)

### 安装gensim ###
1. 先安装其依赖 NumPy and Scipy
	1. 安装Numpy: 由于之前安装Pandas时顺带安装了，如果独立安装，需再找一下。
	2. 安装[Sccipy](https://github.com/scipy/scipy/blob/master/INSTALL.rst.txt#id8):
	sudo apt-get install python python-dev libatlas-base-dev gcc gfortran g++
2. 运行: pip install -U gensim

### 关联规则 ###
_以下D代表一个数据集合_

1. 数据离散化 => 找出高频项目组 ＝> 产生关联规则，
2. 找出高频项目组: 对D中的所有元素进行组合，需要满足指定支持度
3. 产生关联规则:  对各种组合进行计算，验证是否满足给定的支持度和可信度，
4. 假设要计算 X->Y 是否在D中的存在关联规则，
5. 关联规则在D中的支持度(support)是D中事务同时包含X、Y的百分比，即概率，
6. 置信度(confidence)是D中事务已经包含X的情况下，包含Y的百分比，即条件概率，
7. 如果满足最小支持度阈值和最小置信度阈值，则认为是有关联的。

### Laravel debugger学习 ###
1. 安装
	1. 在项目目录下执行: composer require barryvdh/laravel-debugbar
	2. 到config/app.php文件中, providers配置下添加Barryvdh\Debugbar\ServiceProvider::class,
		aliases配置下'Debugbar' => Barryvdh\Debugbar\Facade::class,
	3. php artisan vendor:publish
	4. 如有必要可进行缓存和配置缓存清除:
		1. php artisan cache:clear 
		2. php artisan config:clear
2. 使用：
	1. 可以在View中或Controller写入调试代码，比如:
	<?php Debugbar::info(‘Debug'); ?>
	就可以在浏览器端看到调试条了。
	
### Laravel 测试 ###
_由于想用laravel自带的phpunit命令进行测试，出现了权限问题，所以换用另一种方式_
1. wget https://phar.phpunit.de/phpunit.phar (在项目目录下执行)
2. php phpunit.phar

### 可以使用国内的pip源 ###
pip install --trusted-host pypi.mirrors.ustc.edu.cn -i http://pypi.mirrors.ustc.edu.cn/simple/ {包名}

### mysql学习 ###
1. 查看某个表的索引: SHOW INDEX FROM yourtable;

### 全局注意事项 ###
1. 注意切换到_**指定版本和环境**_下, 比方在虚拟环境下我的virtualenv在/home/vagrant/python中
2. 在Linux下 . 和 source 的作用相同 


### celery and flower ###
1. 在指定环境下安装celery: pip install celery
2. 在制定环境下安装flower: pip install flower
3. 编写相关的celery任务，相关操作可查看：[First Steps with Celery](http://celery.readthedocs.org/en/latest/getting-started/first-steps-with-celery.html)
3. 启动celery和flower: 
	1. celery -A proj worker --loglevel=info
	2. celery flower -A proj --port=5555
4. 查看flower的相关调用： [flower REST API](http://nbviewer.ipython.org/github/mher/flower/blob/master/docs/api.ipynb)
5. 任务查看: 访问http://1localhost:5555/
6. 注意事项: (如果用虚拟环境配置的，则localhost对应多地址是虚拟地址，比如：192.168.10.10)

### Mac下启动redis ###
redis-server /usr/local/etc/redis.conf
(homestead下默认有安装redis)

### virtualenv学习 ###
具体使用都可查看［Virtual Environments］(http://docs.python-guide.org/en/latest/dev/virtualenvs/)

## vagrant操作事项：##
1. Vagrant启动（_到Homestead目录下运行_)： vagrant ssh
2. 查看状态： vagrant status
3. 创建项目时需要重启环境：vagrant provision

## 创建新的larvel项目 ##
1. 使用命令：laravel new project_name
	或者（推荐）composer create-project laravel/laravel test-laravel-5-project --prefer-dist 
2. 修改homestead的site map （在.homestead下的Homestead.yaml(cd ~/.homestead)）
3. 修改host里面的主机映射（在/etc下的hosts）
