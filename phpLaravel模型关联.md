###模型关联
* ####模型1对1  
	* <h5>有Phone模型和Use模型  比如User有一个外键user_id在phone模型上，通过默认外键获取到Phone对象可以使用下面的方式
	
	* $this->hasOne('App\Phone') （根据User对象中的id字段，查看Phone模型上的user_id字段）
	
	* 如果不是要通过默认的外键来获取Phone对象，可以在hasOne的第二个参数里面填写其他字段名
	
	* $this->hasOne('App\Phone', 'foreign_key')（根据User对象中的id字段，查看Phone模型上的foreign_key字段来获取Phone模型）
	
	* 如果不想通过User模型中的id字段来查看Phone模型，可以通过传入hasone的第三个参数
	
	* $this->hasOne('App\Phone', 'foreign_key', 'local_key')（根据User模型中的local_key字段来查看Phone模型中的foreign_key字段来获取Phone）</h5>
	
* #### 定义反向关联
	* <h5> 例如 根据Phone模型来获取User模型 
	
	* 使用 $this->belongsTo('App\User') ps:根据默认外键获取到User对象 也就是通过Phone模型的user_id字段查询User模型的id字段
	
	* 如果Phone不是想通过默认外键user_id来获取User 需要使用其他的字段来获取，可以传入belongsTo的第二个参数
	
	* $this->belongsTo('App\User', 'foreign_key') ps:Phone模型根据foreign_key字段来查询User模型中的id字段来获取User模型
	
	* 如果Phone不想通过外键来查询User模型中的id字段 可以传入belongsTo的第三个参数
	
	* $this->belongsTo('App\User', 'foreign_key', 'other_key') ps:Phone模型对象根据外键foreign_key来查询User模型中的other_key字段来获取User对象</h5>