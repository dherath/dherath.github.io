---
layout: post
title: "Combining video-game sprites using logical operations"
comments: false
description: "post 3"
keywords: "image processing, logic, operations, AND, NOT, OR, example"
---
![front-image](https://raw.githubusercontent.com/dherath/WebsiteMaterial/master/2017/post_3_boolean_algebra_pokemon/images/front_matter.png)

![RGB](https://raw.githubusercontent.com/dherath/WebsiteMaterial/master/2017/post_3_boolean_algebra_pokemon/images/rgb_seperated.png)


``` matlab
function temp = combine_image(man,back)
    man_b= im2bw(man,0.99); % a comment
    back_b = im2bw(back);
    not_back = not(back_b);
    com = and(man_b,not_back);
    com1 = not(com);
    with_man = com1.*double(man);
    with_tree = com.*double(back);
    sz= size(com);
    for i = 1:sz(1,1)
        for j=1:sz(1,2)
            temp(i,j)=max(with_man(i,j),with_tree(i,j));
        end
    end
    temp = uint8(temp);
end
```
``` matlab
clc;
clear;
man = imread('silver.png');
back = imread('background.png');

man_r=man(:,:,1);
man_g=man(:,:,2);
man_b=man(:,:,3);

back_r = back(:,:,1);
back_g = back(:,:,2);
back_b = back(:,:,3);

temp_r = combine_image(man_r,back_r);
temp_g = combine_image(man_g,back_g);
temp_b = combine_image(man_b,back_b);

final_image = uint8(zeros(size(man)));
final_image(:,:,1)= temp_r;
final_image(:,:,2)= temp_g;
final_image(:,:,3)= temp_b;

figure;
imshow(final_image);

```
