Welcome to the savtable wiki!

savTable is a codeigniter library to generate table list with less effort.
savTable automatically create insert, edit and delete functionality.
Other features:
Paging (back,next and numeric link)
Order by column (sort table by ascending and descending order)

**Installation**

Place the following files at corresponding location of your project.

libraries/savtable.php 
controllers/Table_p.php 

Done!

controllers/Welcome.php and views/table_list.php are optional, it contain demo code.


To generate table list in views:

		// load library
		$this->load->library('savtable');
		// call table_list function by passing mysql table name as first parameter.
		$data['table_list'] = $this->savtable->table_list('mysql_table_name_here');
		// $data['table_list'] variable contain the result, which you can print at view page.
		$this->load->view('table_list',$data);


For more information check demo files.



Advance configuration:

In second parameter you can pass an array with more attributes.
example 1) 


		$attr=array(
		"column"=>array('bid','first_name','last_name'),
		"limit"=>"0",
		"nor"=>"30",
		"where"=>"last_name='sandhu'",
		"order_by"=>"ASC",
		"order_col"=>"bid"
		);
		$data['table_list'] = $this->savtable->table_list('basic',$attr);

		
here first value of array contain the columns you want to publish in table.
second & thrid value contain the limit and number of rows per page.	
fourth value contain where condition.
fifth & sixth value contain order by statement.

it will return following query:

		select bid,first_name,last_name from basic order by bid DESC limit 0,30





example 2) - Join


		$attr=array(
		'column'=>array('basic.bid','basic.first_name','basic.last_name','user_group.group_name'),
		'join'=>array(
						array('user_group','basic.gid=user_group.gid')
					),
		);
		$data['table_list'] = $this->savtable->table_list('basic',$attr);

		
here first value of array contain the columns you want to publish in table.
second value contain the multidimensional array to join the base table.		

it will return following query:

		select basic.bid,basic.first_name,basic.last_name,user_group.group_name from basic join user_group on basic.gid=user_group.gid order by bid DESC limit 0,30



example 3) - multiple where conditions


		$attr=array(
		"column"=>array('bid','first_name','last_name'),
		"limit"=>"10",
		"where"=>array(
						"last_name='sandhu'",
						"bid='1'",
						),
		"order_by"=>"ASC",
		"order_col"=>"bid"
		);
		$data['table_list'] = $this->savtable->table_list('basic',$attr);

here first value of array contain the columns you want to publish in table.
second value contain the limit.	
third value contain the array of where condition.
fourth & fifth value contain order by statement.


example 4) - custom query


		$attr=array(
				"query"=>"select * from basic"
				);
		$data['table_list'] = $this->savtable->table_list('basic',$attr);



Add css class name into table


		$attr=array(
				'table_class_name'=>'my_table'
				);
		$data['table_list'] = $this->savtable->table_list('basic',$attr);




