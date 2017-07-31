---
layout: post
title: "Combining video-game sprites using logical operations"
comments: false
description: "post 3"
keywords: "image processing, logic, operations, AND, NOT, OR, example"
---
![front-image](https://raw.githubusercontent.com/dherath/WebsiteMaterial/master/2017/post_3_boolean_algebra_pokemon/images/front_matter.png)

Today I'm going to explain how different video-game sprites(_or any image_) can be combined together like whats shown above using logical operations like **AND, OR, NOT** in the realm of `Image Processing`. This is an extremely interesting area I got to sample during my undergrad days, and I thought of making my second post from a memorable part of it. For the demonstrations I thought of  using sprites from one of my all time favourte pokemon games, [pokemon silver](https://bulbapedia.bulbagarden.net/wiki/Pok%C3%A9mon_Gold_and_Silver_Versions){: target="blank"} from Generation 2 which I played first :).

### Some Basics(<a href="#ref1">Skip</a> if you're not new to Image Processing)

First of all a brief introduction to images. I'm sure you all know something about different types of screen resolutions like HD, 488p and so on. The difference between these types of resolutions are the number of **pixels** in a given view. Think of an image as a 2D grid of small squares where each square represents a dot of color, and higher the resolution the larger the number of squares in a picture. These squares are called **_pixels_**. In a digital image a pixel stores some kind of numeric value, where each numeric value represents some color. `For example in grayscale images the value 0 represents black and 255 white and all integers between are shades of gray.`

 We all know that the three primary colors are **red, blue and green**. Likewise color images (RGB) could be represented as a combination of three channels or sub-images for red, blue and green as shown below. Each of these sub-images are represented in [grayscale](https://en.wikipedia.org/wiki/Grayscale){: target="blank"}. In fact these sub-images don't really have a color per-say, rather some intensity vale[0-255] which is shown in shades of gray.

![rgb_seperated](https://raw.githubusercontent.com/dherath/WebsiteMaterial/master/2017/post_3_boolean_algebra_pokemon/images/rgb_seperated.png)

Now if you look closely at the character image it's mostly red, therefore the red-channel has values closer to 255 which is why that channel looks brighter as opposed to the blue-channel which is very dark. Similarly for the background, the green-channel is th brightest image because the original background shows a forest.

#### Logical operations in Image Processing

The basic logical operations in image processing are the same as in arithmetic **`AND, NOT and OR`**.

![truth-table](https://upload.wikimedia.org/wikipedia/commons/4/4a/Truth_table_for_AND%2C_OR%2C_and_NOT.png){: width="400px"}

For logical operations to work on images, the images need to be of a specific type called `binary`. As the name suggests the pixels of these images could only have two values **1(for white) or 0(for black)**. So basically these are the main operations I'll be using to combine the pokemon game sprites. The images below illustrate the outcome of logical operations on binary images.

#### 1) NOT operation

![not-image-example](https://raw.githubusercontent.com/dherath/WebsiteMaterial/master/2017/post_3_boolean_algebra_pokemon/theory_examples/not_image.png){:height="200px"}

The **NOT** operation inverts a given input value(0 to 1 & vice-versa), its the same principle for images where instead of one single point or location entire regions get inverted depending on their pixel values; so a black area become white or a white area becomes black respectively.

#### 2) AND operation

#### 3) OR operation

### <a name="ref1">Combining game sprites</a>

From here on, I'll be explaining the main steps in combining image sprites. I've used the software platform **`Matlab`** for this demonstration. Also note that in the code examples I've used a function, the reason being the steps I explain below need to be operated three times iteratively for all red, blue and green channels of a given image. Instead of repeating the same code, I figured using functions would make my life more easier. `If you have no idea about the Matlab image processing toolbox click` **[here](https://in.mathworks.com/help/images/getting-started-with-image-processing-toolbox.html){:target="blank"}** `and if you need a refresher on Matlab functions click `**[here](https://in.mathworks.com/help/matlab/matlab_prog/create-functions-in-files.html){:taget="blank"} :)**.

##### Step 1 : Converting RGB(Color) images to Binary images

The first step is to convert our input images to a binary format so that we can use logical operations. Initially we separate the three channels of red, green and blue and afterwards convert them to purely black and white. In **`matlab`** we can do this using a function called `im2bw()`. The images below show the output for this step.

![binary-images](https://raw.githubusercontent.com/dherath/WebsiteMaterial/master/2017/post_3_boolean_algebra_pokemon/step1.png)

##### Step 2 : Create an inverted mask of the binary background image

The second step is to create a temporary image or mask which is an inverted output of the binary background image.

![inverted-binary-background]()

##### Step 3 : Create temporary Mask 1

##### Step 4 : Create temporary Mask 2

##### Step 5 : Process Masks with original images

##### Step 6 : Combine the character image and background image

##### Step 7 : Combine separate channels (R,G,B) into a color(RGB) image

 What you need to remember is that at unlike in a standard arithmetic problem, when it comes to images the output of these operations will also be images.




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
