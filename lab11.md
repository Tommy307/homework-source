##附带软件的风潮  
大家应该都有遇到下载一个软件的时候被莫名其妙的安装上了其它自己并不需要的软件。  
这是一款软件在利用大家一般很少会检查安装表的习惯。   
![](https://raw.githubusercontent.com/zlsteven/homework-source/gh-pages/images/屏幕截图(36).png)    

从上图可以看出，很多时候软件会把强装软件的征求同意的条款放在很不起眼的地方，同时自动为用户打上勾，这样即使用户发起投诉，软件公司也有借口了。  
  
##一些排序算法   
1>快速排序算法  
选取数组的中间元素，然后对除这个元素外的所有元素进行排序，比这个元素大<记作A+>的则不进行操作，比这个元素小<记作A+>的就向左与距它最远的A+swap，并记住已测试过的区段的A+与A-的分界点，最终将“中间元素”插入到中间点，之后运用递归对中间元素左右两边的小数组进行排序，当数组元素少于两个时停止递归。  
伪码：  
qsort(left right s[]):  
IF right-l==left END  
  

int mid=(left+right)/2;  
s_swap(left,mid)  
mid=left  

FOR:i=left+1;i<=right DO:
IF s[i]<s[left] mid++ s_awap(i,++mid)
END IF  
s_swap(left,mid)  
END FOR  
qsort(left mid-1)
qsort(mid+1,right)
END
程序：  
void swap(int a,int b){
    int temp=a;
    a=b;
    b=temp;
}
void qsort(int s[],int left,int right){

}

  

