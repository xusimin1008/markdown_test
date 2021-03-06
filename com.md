### datartery-amazon-v3 command
```php
<?php

namespace App\Console\Commands;

use App;
use Log;
use DB;
use Illuminate\Console\Command;
use Carbon\Carbon;

class ApplyUsSimpleProductTasks extends Command
{
    /**
     * The name and signature of the console command.
     *
     * @var string
     */
    protected $signature = 'apply:us-simple-product';

    /**
     * The console command description.
     *
     * @var string
     */
    protected $description = 'Apply Us Simple Product Tasks';

    /**
     * Create a new command instance.
     *
     * @return void
     */
    public function __construct()
    {
        parent::__construct();
    }

    /**
     * Execute the console command.
     *
     * @return mixed
     */
    public function handle()
    {
        // Log::info('Run Us Simple Product Tasks...');
        $this->comment('Run Us Simple Product Tasks...');

        $tableName = 'us_simple_product';
        $table = DB::table($tableName);
        // $table->dateTime('last_snapped_at');
        $simpleProducts = $table->where('last_snapped_at', '<', Carbon::now())
                                ->orWhereNull
                                               ->orderBy('last_snapped_at')
                                               ->get();

        $this->comment('Simple Product Count: '. count($simpleProducts));

        return;

        $worker = 'crawler-celery';
        $taskName = 'dispatcher.tasks.us_simple_product.crawl_us_simple_product';
        $celery = App::make($worker);

        foreach ($simpleProducts as $simpleProduct) {
            $kwargs = [
                'product_id' => $simpleProduct->id,
            ];

            $celery->taskAsyncApply($taskName, $kwargs);

            $lastSnappedAt = NULL;
            if (!$simpleProduct->last_snapped_at || $simpleProduct->last_snapped_at == '1970-01-01 00:00:00') {
                $lastSnappedAt = Carbon::now()->addDays(1);
            } else {
                $lastSnappedAt = Carbon::parse($simpleProduct->last_snapped_at)->addDays(1);
            }

            DB::table($tableName)->where('id', $simpleProduct->id)
                                 ->update(['last_snapped_at' => $lastSnappedAt]);

            break;

        }
    }
}

```

### 数据积累
> 股票

> 豆瓣电影top 250

```python
import path
def hello():
  pass
```

```
sudo service nginx restart
sudo service php5-fpm restart
```
### 创建laravel项目时，端口映射
```shell
主机环境下
$ cd /etc
$ subl hosts
$ cd ~/.homestead 
$ subl Homestead.yaml
$ vagrant provision (vagrant目录下)
```

### 青云对象存储使用相关
```python
>>> import qingcloud.qingstor
#建立连接
>>> conn = qingcloud.qingstor.connect(
        'pek3a.qingstor.com',
        'access key id',
        'secret access key'
    ) 
    
# 创建存储空间    
>>> bucket = conn.create_bucket('mybucket') 

# 创建对象（创建完对象后需要进行send_file，才会建立对应的对象）
>>> key = bucket.new_key('myobject')
>>> with open('/tmp/myfile') as f:
>>>     key.send_file(f)

# 删除对象
>>> bucket.delete_key('myobject')

使用bucket进行检索
def list(self, prefix=None, delimiter=None, marker=None, limit=None):
```

### javascript 相关
```
in --- 键在对象中 或 索引在数组中
&& --- 
```


### elasticsearch 相关
```
sudo service elasticsearch start （启动服务）
```

### tmux 相关(一切以Ctrl + B开始)
```
% 左右分屏
" 上下分屏
```

### sublime 相关
```
Command + , 打开设置
```

### 克隆代码库
1. git clone 主代码库链接
2. git checkout -b develop origin/develop
3. 添加remotes:
	1. 添加origin: 自己的fork代码库链接
	2. 添加main: 主库的代码库链接

### npm
1. npm install vue-resource --save

### 查看谷歌扩展的代码
```
cd Library/Application\ Support/Google/Chrome/Default/Extensions
在谷歌扩展程序中 开启 开发者模式 得到扩展id
到上面的目录找到id对应的目录，里面即为源码
```
### amazon爬虫
```
存储路径（对象存储）：Amz{region(Us, Cn, Uk)}/{year}/{month}/{date}/{asin}.{format(html, xml)}.gz

抓取来源：按各品类去抓取和用户自定义添加
-- 用户添加的商品等到下一次抓取周期才进行

抓取时间间隔：固定（假设每3，5或者7天抓取一次商品排行榜和商品快照）
-- 现在的抓取时间间隔只能保证是我们想要的间隔，但并不能保证在我们想要的时间内，即如果出现这样的异常作何处理？

面对不同结构的页面，应该把所有情况都尝试一遍，比如，detail = ''
if (!detail) { ... }
if (!detail) { ... }
...

```

### amazon category 研究
```
Clothing下的Women的Shorts的node_id为：1048186, 在Men下的node_id 为：1045560
说明 -- 具有相同名称的子品类在不同较大品类下中的node_id也是不同的。
---
在四个排行榜下的品类展示都是一样的，除了movers and shakers只展示最高品类，
所以要想抓取所有的品类，只需抓取某一个，如best sellers下的品类。
```
存储结构
```
id, dept_code, parent_id, node_id, name,
best_sellers_url, crawled_best_sellers_at,
hot_new_releases_url, crawled_hot_new_releases_at
movers_and_shakers_url, crawled_movers_and_shakers_at
most_wished_for_url, crawled_most_wished_for_at
most_gifted_url, crawled_most_gifted_at
```

### vue router相关
```
把路由映射到各个组件
嵌套路由可以进行嵌套组件
如果一个子路径和一个父路径有相同的字段，则子路径的值会覆盖父路径的值
动态片段 /user/:username 显示可从$router.params.username得到
全匹配片段（动态片段贪心版） /user/*any 可以匹配/user/a/b/c 显示可从$router.params.any得到
```

### vue相关
```
v-cloak 不显示元素知道编译完成
v-text 显示元素内容 <span v-text="msg"></span> == <span>{{msg}}</span> （不过后者在元素未编译完成时会显示{{msg}}，建议使用前者）

```
### pg数据库语句
```
update products set review_url = replace(review_url, 'helpful', 'recent&pageNumber=1'); (替换字符串)
```

###laravel学习
```
php composer.phar dumpautoload  (数据库重建时，某些表出现错误)
```

### tornado学习
> 想了解框架和学习一下消息推送

***

### Cron正则表达式检查
```
<?php
$cron = "*/5 * * * *";
$result = preg_match(
	"/(\*|[0-5]?[0-9]|\*\/[0-9]+)\s+"
	."(\*|1?[0-9]|2[0-3]|\*\/[0-9]+)\s+"
	."(\*|[1-2]?[0-9]|3[0-1]|\*\/[0-9]+)\s+"
	."(\*|[0-9]|1[0-2]|\*\/[0-9]+|jan|feb|mar|apr|may|jun|jul|aug|sep|oct|nov|dec)\s+"
	."(\*\/[0-9]+|\*|[0-7]|sun|mon|tue|wed|thu|fri|sat)\s*/i", $cron, $matches); （不支持逗号）
	
$pattern = '^((?:[1-9]?\d|\*)\s*(?:(?:[\/-][1-9]?\d)|(?:,[1-9]?\d)+)?\s*){5}$'; (完整可用的)
```
***

### 清空redis的某个数据库
```
  $ redis-cli 
  > select [db_num]
  > flushdb
```
