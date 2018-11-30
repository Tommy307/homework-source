##*附带软件的风潮  
大家应该都有遇到下载一个软件的时候被莫名其妙的安装上了其它自己并不需要的软件。  
这是一款软件在利用大家一般很少会检查安装表的习惯。   
![](https://raw.githubusercontent.com/zlsteven/homework-source/gh-pages/images/屏幕截图(36).png)    

从上图可以看出，很多时候软件会把强装软件的征求同意的条款放在很不起眼的地方，同时自动为用户打上勾，这样即使用户发起投诉，软件公司也有借口了。  
  
##*一些排序算法   
#*1>快速排序算法  
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
void swap(int s[],int a,int b){  

    int temp=s[a];  

    s[a]=s[b];  
     
    s[b]=temp;  

}  

void qsort(int s[],int left,int right){  

    if(right-1==left) return;  

    swap(s,left,(left+right)/2);   

    int mid=left;  

    for(int i=left+1;i<=right;++i){  

        if(s[i]<left) swap(s,i,++mid);   

    }  

    swap(s,left,mid);  

    qsort(s,left,mid-1);  

    qsort(s,mid+1,right);  

}  
    
#*2>嵌套循环算法  
用两个循环按顺序依次将带比较元素中的最小元素转移到带比较序列的最前端，从而达到从小到大排序的目的。  
伪码：  
int l=length(s[])
FOR i=0 i<l-1 DO:  
    FOR j=i+! j<l DO:  
    IF(s[i]>s[j]) s_swap(i,j)
    END IF
    END FOR  
END FOR  
  
程序：  
#include<stdio.h>  

void swap(int s[],int i,int j){  

    int temp=s[i];  

    s[i]=s[j];  

    s[j]=temp;  

}  

void qsort(int s[],int l){  

    for(int i=0;i<l-1;++i){  

        for(int j=i+1;j<l;++j){  

            if(s[i]>s[j]) swap(s,i,j);  

        }  

    }  

}  


  

