# XTU oj

## 作业0x05-数组1



### 1、1169——最大子列和

http://202.197.224.59/exam/index.php/problem/exam_read/id/1169/exam_id/441

在线处理

```c
#include<stdio.h>
#define MAX_N 100000
int arr[MAX_N+1];
int main()
{
    int n,m;
    while(scanf("%d %d",&n,&m)!=EOF&&(n!=0)&&(m!=0)){
        int max=0,sum=0;
        for(int i=0;i<n;i++){
            scanf("%d",&arr[i]);
            sum+=arr[i];
            if(i>=m) sum-=arr[i-m];
            if(sum>max) max=sum;
        }
        printf("%d\n",max);
    }
    return 0;
}
```

### 2、1175——Change

http://202.197.224.59/exam/index.php/problem/exam_read/id/1175/exam_id/441

```c
#include<stdio.h>
#define MAX_N 50
int a[MAX_N+1],b[MAX_N+1],flag[MAX_N+1];
int main()
{
    int n;
    while(scanf("%d",&n)!=EOF&&(n!=0)){
        for(int i=0;i<n;i++){
            scanf("%d",&a[i]);
        }
        for(int i=0;i<n;i++){
            scanf("%d",&b[i]);
        }
        for(int i=0;i<n;i++){
            if(b[i]>a[i])
                flag[i]=1;
            else if(b[i]==a[i])
                flag[i]=0;
            else
                flag[i]=-1;
            }
        int t1=0,t2=0,t3=0;
        for(int i=0;i<n;i++){
            if(flag[i]==1) t1++;
            else if(flag[i]==-1) t3++;
        }
        t2=n-t1-t3;
        printf("%d %d %d\n",t1,t2,t3);
    }
    return 0;
}
```

### 3、1260——Completed String

http://202.197.224.59/exam/index.php/problem/exam_read/id/1260/exam_id/441

```c
#include<stdio.h>
#include<string.h>
#include<ctype.h>
#define MAX_N 1000
char str[MAX_N+1];
int main()
{
    char ch;
    while(~scanf("%s",str)){
        int arr[26]={0};
        for(int i=0;i<26;i++) arr[i]=0;
        int  len=strlen(str);
        for(int i=0;i<len;i++){
            ch=tolower(str[i]);
            str[i]=ch;
             arr[str[i]-'a']=1;
        }
        int ans=0;
        for(int i=0;i<26;i++){
            if(arr[i]==1) ans++;
        }
       
        if(ans==26)puts("Yes");
        else puts("No");
    }
    return 0;
}
```

### 4、1166——逆序数（小数据）

http://202.197.224.59/exam/index.php/problem/exam_read/id/1166/exam_id/441

```c
#include<stdio.h>
#define MAX_N 100000
int arr[MAX_N+1];
int main()
{
    int n;
    while(~scanf("%d",&n)&&(n!=0)){
        for(int i=0;i<n;i++){
            scanf("%d",&arr[i]);
        }
        int count=0;
        for(int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                if(arr[i]>arr[j])count++;
                else continue;
            }
        }
        printf("%d\n",count);
    }
    return 0;
}
```

### 5、1331——密码

http://202.197.224.59/exam/index.php/problem/read/id/1331

这种包含关系，想着用递归，但是我只能想出边界条件，然后看大佬(Jay_is_chou)的解题过程感觉和数学归纳法很像，去查了一下，发现原来三者之间有关系，关系大致是这样的，递推是数学归纳法的原理，递推也是递归的原理，利用数学归纳法可以写出递归函数。

```c
#include<stdio.h>
__int64 b[50][5];
__int64 ans;
void solve()
{
    b[1][1]=b[1][2]=b[1][3]=b[1][4]=1;
    for(int i=2;i<=45;i++){
        b[i][1]=b[i-1][2]+b[i-1][3];
        b[i][2]=b[i-1][1]+b[i-1][3]+b[i-1][4];
        b[i][3]=b[i-1][1]+b[i-1][2]+b[i-1][4];
        b[i][4]=b[i-1][2]+b[i-1][3];
    }
}
int main(){
    solve();
    int n;
    scanf("%d",&n);
    while(n--){
        int a;
        scanf("%d",&a);
        ans=b[a][1]+b[a][2]+b[a][3]+b[a][4];
        printf("%I64d\n",ans);
    }
}
```

