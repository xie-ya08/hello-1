层次分析法

%先获取判断矩阵
disp("请输入判断矩阵A")
A=input('A=');
[n,n]=size(A);%%得知矩阵A的大小

%求权重
%方法一 算术平均法求权重
%先将A矩阵按列求和
Sum_A=sum(A);
SUM_A=repmat(Sum_A,n,1);
Stand_A=A./SUM_A;
disp('算术平均法求权重的结果为：');
w1=sum(Stand_A,2)./n;%,2表示按行求和
disp(w1)

%方法二 特征值法求权重
[V,D]=eig(A);
Max_eig=max(max(D));%先按列求最大值，得到行向量，在从这个向量里面求最大值
[r,c]=find(D==Max_eig,1);%find函数是返回与Max_eig元素对应的前1的索引，即返回出相关位置
disp("特征值法求权重的结果为：");
w2=V(:,c)./sum(V(:,c));%%得到权重

disp("两种算法的平均值是：");
disp((w1+w2)./2);

%%做一致性检验CI=（最大特征值-n）/（n-1）
CI=(Max_eig-n)/(n-1);
%RI有误差,通过查表知道
RI=[0 0.0001 0.52 0.89 1.12 1.2 1.36 1.41]
CR=CI/RI(n);
disp('最大特征值是：');
disp(Max_eig);
disp('一致性指标CI=');disp(CI);
disp('一致性比例CR=');disp(CR);
if CR<0.10
    disp('CR<0.10,该判断矩阵A的一致性可以接受');
else
    disp('注意，CR>=0.10，该判断矩阵需要进行修改');
end

