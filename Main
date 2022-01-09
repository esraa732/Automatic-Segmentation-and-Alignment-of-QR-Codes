
##I = imread("1.1.bmp");
##I = imread("2.1.bmp");
##I = imread("3.1.bmp");
##I = imread("3.3.bmp");
##I = imread("4.1.bmp");
I = imread("4.4.bmp");
##I = imread("5.1.bmp");
##I = imread("5.2.bmp");
##I = imread("5.3.bmp");
##I = imread("6.1.bmp");
##I = imread("6.2.bmp");
##I = imread("7.1.bmp");
F=1;
R=0;
I_=I;
VV=[];
Show = 1;
[H W L]=size(I);

Temp = sort((I(:)));

MIN = sum(Temp(1:15))/15;

I=rgb2gray(I);

I = medfilt2(I, [3 3]);

I=I-MIN;

if Show==1
figure('Name','med filter - min '),imshow(I);
end

Sampel=20;

for i = 1 : (H/Sampel)
for j = 1 : (W/Sampel)

i1=i*Sampel;
j1=j*Sampel;

x=I(i1-Sampel+1:i1,j1-Sampel+1:j1);

min_=min(x(:));

x=sort(x(:));

c=Sampel*Sampel;

range = sum(x(c-14:c))/15 - sum(x(1:15))/15;

Threshold=min_+range/1.5;

if range>50

Z=I(i1-Sampel+1:i1,j1-Sampel+1:j1)>Threshold;

I(i1-Sampel+1:i1,j1-Sampel+1:j1)=Z*255;

end

end

end


I=im2bw(I,0.5);

if Show==1
figure('Name','Variable Thresholding'),imshow(I);

figure('Name','Detect Corners'),imshow(I_);
hold on;
end


All_Conected = bwconncomp(I);
numPixels = cellfun(@numel,All_Conected.PixelIdxList);
N=size(numPixels,2);


x=[];
y=[];


for i=1:N

if numPixels(i)>50 

[X,Y] = ind2sub(size(I),All_Conected.PixelIdxList{i});


minx=min(X);
miny=min(Y);

maxx=max(X);
maxy=max(Y);

H=maxx-minx;
W=maxy-miny;

Z=I(minx:maxx,miny:maxy);



D1 = square(W,H);

D2=CentreBlackSqure(Z,W,H);

if D1==1 && D2==1 

[v ,D3]=CentricBlackBorder(I,Z,minx,maxx,miny,maxy,W,H);

if D3==1


if Show==1
plot(round((maxy+miny)/2),round((maxx+minx)/2),'r-o')
end

V=v;

VV=[VV ; V];

x=[x;round((maxy+miny)/2)];

y=[y;round((maxx+minx)/2)];

end

end
end
end

QRs=size(x,1);

if size(x,1)<3

F=0;

elseif size(x,1)==3

R=Alignment(x,y,I_,V,Show);

else

for i=1:QRs

miny=100000;
flag=0;

for j=1:QRs

if i~=j  && x(i)~=-1 && x(j)~=-1

p1=[x(i);y(i)];
p2=[x(j);y(j)];
s1 = sqrt(((p2(1)-p1(1))^2+(p2(2)-p1(2))^2));

for ij=1:QRs
if ij~=i  &&  ij~=j && x(ij)~=-1

p3=[x(ij);y(ij)];

s2 = sqrt(((p3(1)-p1(1))^2+(p3(2)-p1(2))^2));

s3 = sqrt(((p3(1)-p2(1))^2+(p3(2)-p2(2))^2));


if abs(s1-s2)<40 && abs((s1^2+s2^2)-s3^2)<1200

if s1<miny

P=[p1' ; p2'  ; p3' ];

miny=s1;

I=i;
J=j;
IJ=ij;
flag=1;

end

end

end

end

end

end

if flag==1

R=Alignment(P(:,1),P(:,2),I_,VV(I),Show);

x(I)=-1;
x(J)=-1;
x(IJ)=-1;

end

end

end
