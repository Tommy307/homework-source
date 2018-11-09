##Top-down介绍  
建立一个新的asm文件 
然后在asm里面第一需要建立的是整个asm的基准，后续不断的插入空的prt文件， 
把需要的prt空文件建完以后，根据顶层的基准创建第一个prt的feature，完善第一个prt以后 
后面的零件可以根据第一个prt，也可以根据顶层的基准来完成feature的创建。以此类推，直到完成整个asm的建立。   

##洗衣机算法设计（伪代码）  

START  
water_in_switch(open)  
REPEAT  
get_water_volume()  
UNTIL water_volumw==setting_water_volume   
water_in_switch(close)  
  
REPEAT  
motor_run(left)  
motor_run(right)  
UNTIL time_counter()==setting_time  
halt(returncode)  
  

water_out_switch(open)
REPEAT  
get_water_volume()  
UNTIL water_volumw==0  
water_out_switch(close) 
IF halt(returncode)  RETURN success  
ELSE return failure  
ENDIF  

END 
