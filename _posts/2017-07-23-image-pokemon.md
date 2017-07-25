---
layout: post
title: "Combining video-game sprites using logical operations"
comments: false
description: "post 3"
keywords: "image processing, logic, operations, AND, NOT, OR, example"
---
![front-image](https://raw.githubusercontent.com/dherath/WebsiteMaterial/master/2017/post_3_boolean_algebra_pokemon/images/front_matter.png)

Today I'm going to explain how different video-game sprites(_or any image_) can be combined together like whats shown above using logical operations like **AND, OR, NOT** in the realm of `Image Processing`. This is an extremely interesting area I got to sample during my undergrad days, and I thought of making my second post from a memorable part of it. For the demonstrations I thought of  using sprites from one of my all time favourte pokemon games, [pokemon silver](https://bulbapedia.bulbagarden.net/wiki/Pok%C3%A9mon_Gold_and_Silver_Versions){: target="blank"} from Generation 2 which I played first :).

### Some Basics ( Skip if you're not new to Image Processing)

First of all a brief introduction to images. I'm sure you all know something about different types of screen resolutions like HD, 488p and so on. The difference between these types of resolutions are the number of **pixels** in a given view. Think of an image as a 2D grid of small squares where each square represents a dot of color, and higher the resolution the larger the number of squares in a picture. These squares are called **_pixels_**. In a digital image a pixel stores some kind of numeric value, where each numeric value represents some color. `For example in grayscale images the value 0 represents black and 255 white and all integers between are shades of gray.`

 We all know that the three primary colors are **red, blue and green**. Likewise color images (RGB) could be represented as a combination of three channels or sub-images for red, blue and green as shown below. Each of these sub-images are represented in [grayscale](https://en.wikipedia.org/wiki/Grayscale){: target="blank"}. In fact these sub-images don't really have a color per-say, rather some intensity vale[0-255] which is shown in shades of gray.

![rgb_seperated](https://raw.githubusercontent.com/dherath/WebsiteMaterial/master/2017/post_3_boolean_algebra_pokemon/images/rgb_seperated.png)

Now if you look closely at the character image it's mostly red, therefore the red-channel has values closer to 255 which is why that channel looks brighter as opposed to the blue-channel which is very dark. Similarly for the background, the green-channel is th brightest image because the original background shows a forest.

#### Logical operations in Image Processing

The basic logical operations in image processing are the same as in arithmetic **`AND, NOT and OR`**.

![truth-table](https://upload.wikimedia.org/wikipedia/commons/4/4a/Truth_table_for_AND%2C_OR%2C_and_NOT.png){: width="300px"}

For logical operations to work on images, the images need to be of a specific type called `binary`. As the name suggests the pixels of these images could only have two values **1(for white) or 0(for black)**.


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
