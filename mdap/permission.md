## 美特好权限设计

### 展示已有权限的门店JS
```
   checkbox.on('change', function(e){
      var mendian = {};
      _.each($('ibox-md'), function(e){
         var checked_length = $(e).find('input[type=checkbox][name="permissions[]"]
                              [data-system="mendian"]').length;
         if(checked_length){
            mendian[md_id] = md_name;
         }
      });
      $('#selected-mendian').html('');
      _.each(mendian, function(e){
         $('#selected-mendian').append('<a href="#">'+ e +'</>');
      });
   });
```

### 门店permission数据组织形式及伪代码：
```
   门店部分可以采用更好的组织方式（根据其parent来区分）：
   [
      XXX门店 => [
         0 => Permission(XXX门店),
         XXX导师团 => [
            0 => Permission(XXX导师团),
            XXX团队 => [
               0 => Permission(XXX团队),
               XXX部门 => Permission(XXX部门),
               YYY部门 => Permission(YYY部门),
               ...
            ],
            ...
         ],
         ...
      ]
   ]
   $r = [];
   $pp = $p->parent.split('-');
   if($p->parent == ''){
      if($p->name in $r){
         $r[$p->name][0] = $p;
      }else{
         $r[$p->name] = [0 => $p];
      }
   }else if($pp.length == 1){
      if($pp[0] in $r){
         if($p->name in $r[$pp[0]]){
            $r[$pp[0]][$p->name][0] = $p;
         }else{
            $r[$pp[0]] = [$p->name => [0 => $p]];
         }
      }else{
         $r[$pp[0]] =  [$p->name => [0 => $p]];
      }
   }else if($pp.length == 2){
      if($pp[0] in $r){
         if($pp[1] in $r[$pp[0]]){
            if($p->name in $r[$pp[1]]){
               $r[$pp[0]][$pp[1]][$p->name][0] = $p;
            }else{
               $r[$pp[0]][$pp[1]][$p->name] = [0 => $p];
            }
         }else{
            $r[$pp[0]][$pp[1]] = [$p->name => [0 => $p]];
         }
      }else{
         $r[$pp[0]] =  [$pp[1] => [$p->name => [0 => $p]];
      }
   }else if($pp.length == 3){
      if($pp[0] in $r){
         if($pp[1] in $r[$pp[0]]){
            if($pp[2] in $r[$pp[0]][$pp[1]]){
               $r[$pp[0]][$pp[1]][$pp[2]][$p->name] = $p;
            }else{
               $r[$pp[0]][$pp[1]][$pp[2]] = [$p->name => $p];
            }
         }else{
            $r[$pp[0]][$pp[1]] = [$pp[2] => [$p->name => $p]];
         }
      }else{
         $r[$pp[0]] = [$pp[1] => [$pp[2] => [$p->name => $p]]];
      }
   }
```
