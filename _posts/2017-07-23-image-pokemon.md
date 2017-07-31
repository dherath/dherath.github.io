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

#### 2) OR operation

![or-image-example](https://raw.githubusercontent.com/dherath/WebsiteMaterial/master/2017/post_3_boolean_algebra_pokemon/theory_examples/or.png){:height="200px"}

The **OR**  operation combines two binary images such that value 1s of both images show up in the final output.  Thats the reason the combination of both the white circles are present in the above output image.

#### 3) AND operation

![and-image-example](https://raw.githubusercontent.com/dherath/WebsiteMaterial/master/2017/post_3_boolean_algebra_pokemon/theory_examples/and.png){:height="180px"}

The **AND**  operation functions in a similar fashion as described in the table above. In this example unlike in the **OR** case, only the intersection of the two circles are shown in the output. Here the output only shows a high value(1) when both images represent a high value for the same (x,y) coordinate respectively.

### <a name="ref1">Combining game sprites</a>

From here on, I'll be explaining the main steps in combining image sprites. I've used the software platform **`Matlab`** for this demonstration. Also note that in the code examples I've used a function, the reason being the steps I explain below need to be operated three times iteratively for all red, blue and green channels of a given image. Instead of repeating the same code, I figured using functions would make my life more easier. `If you have no idea about the Matlab image processing toolbox click` **[here](https://in.mathworks.com/help/images/getting-started-with-image-processing-toolbox.html){:target="blank"}** `and if you need a refresher on Matlab functions click `**[here](https://in.mathworks.com/help/matlab/matlab_prog/create-functions-in-files.html){:taget="blank"} :)**. **_<a href="#ref2">(Click here to go directly to the CODE)</a>_**

##### Step 1 : Converting RGB(Color) images to Binary images

The first step is to convert our input images to a binary format so that we can use logical operations. Initially we separate the three channels of red, green and blue and afterwards convert them to purely black and white. In **`matlab`** we can do this using a function called `im2bw()`. The images below show the output for this step.

![binary-images](https://raw.githubusercontent.com/dherath/WebsiteMaterial/master/2017/post_3_boolean_algebra_pokemon/step1.png)

##### Step 2 : Create an inverted mask of the binary background image

The second step is to create a temporary image or mask which is an inverted output of the binary background image.

![inverted-binary-background](https://raw.githubusercontent.com/dherath/WebsiteMaterial/bc226401273ab062b18245a6b9adcf4ab002de4f/2017/post_3_boolean_algebra_pokemon/step2.png){:height="200px"}

##### Step 3 : Create temporary Mask 1

In this step a temporary mask is created using the two output images from steps 1 & 2. The **AND** operations is used on the `inverted-background image and the binary-character` image in order to get a mask with a certain property. If you look closely at the output image, all the pixels describing the character are black _(value 0)_ where as the rest of the background is the same. Which means any operation done on this mask would only affect the background and the character portion of the image will remain unchanged.

![Mask-1](https://raw.githubusercontent.com/dherath/WebsiteMaterial/bc226401273ab062b18245a6b9adcf4ab002de4f/2017/post_3_boolean_algebra_pokemon/step3.png)

##### Step 4 : Create temporary Mask 2

To get the second temporary mask, the **NOT** operation is used on the Mask image obtained in the previous step. Here the output image is such that all the background pixels remain in its binary state where as the character portion becomes value 1 or _white_. Therefore any operation done to the image will only affect the character and the background will be unaffected.

![Mask-2](https://raw.githubusercontent.com/dherath/WebsiteMaterial/bc226401273ab062b18245a6b9adcf4ab002de4f/2017/post_3_boolean_algebra_pokemon/step4.png){:height="200px"}

##### Step 5 : Process Masks with original images

By now we have two separate masks which give the opportunity to manipulate color intensities of the character and the background separately. However these masks are binary, meaning the values are either 1 or 0. The pixel intensities for original images for each channel(red, green or blue) vary between 0 and 255. In order to get this range into the obtained masks, each mask is `point-wise multiplied` by the respective input images.

**_So what's this point-wise multiplication?_** Earlier I explained that images are like a 2D-grid, and they are stored in matlab as a 2-D matrix. Usually in matrix multiplication, a row is multiplied by a column of another matrix and all the individual values are summed together to obtain a value of one cell in a new matrix. **`However, in point-wise multiplication each cell indexed some (x,y) of matrix A is multiplied by another cell of index (x,y) of some matrix B to obtain the answer.`** Here there is no summation or rowise/columnwise multiplication.

![processed-images](https://raw.githubusercontent.com/dherath/WebsiteMaterial/bc226401273ab062b18245a6b9adcf4ab002de4f/2017/post_3_boolean_algebra_pokemon/step5.png)

If you look closely at the output images. The character image has the original character in the image in addition to a binary representation of the background. In the background output image, the background pixels have the same intensity values as per the input image where as the character section is binary.  Basically, the only step left to take is combine these two separate output images into one single image.

##### Step 6 : Combine the character image and background image

This step is all about combining the separate outputs into one. There are a couple of ways to go about this step, in my case I opted to go by selecting the maximum pixel intensity for each (x,y) coordinate of both the output images and creating a new image with this maximum value. My rational for this method was that the intensity distribution for every pixel would be definitely between 0 and 255, thus by selecting the maximum at each point I'd minimize the probability of selecting a stray 0 (black) pixel.

![combined-image](https://raw.githubusercontent.com/dherath/WebsiteMaterial/bc226401273ab062b18245a6b9adcf4ab002de4f/2017/post_3_boolean_algebra_pokemon/step6.png)

And there you go!!! :) This is the combined image for the red channel from separate sprites for a game character and a specific background.

##### Step 7 : Combine separate channels (R,G,B) into a color(RGB) image

The final step is all about iterating the above steps from 1-6 for each color channel and combining them together in order to create a color image. This step is crucial for a color image, because the output from step 6 only shows a distribution of intensity values for a given image, The only reason we see the differences in shades of gray is because we map those intensity values to some color scale. Therefore, to combine the separate channels a new image is created of type unit8 and the outputs from step 6  combined into it.

![final](https://raw.githubusercontent.com/dherath/WebsiteMaterial/bc226401273ab062b18245a6b9adcf4ab002de4f/2017/post_3_boolean_algebra_pokemon/step7.png)

### <a name="ref2">Code</a>

##### The main program

``` matlab
clc;
clear;
man = imread('silver.png'); % loading images
back = imread('background.png');

man_r=man(:,:,1); % separate input character image to r,g,b channels
man_g=man(:,:,2);
man_b=man(:,:,3);

back_r = back(:,:,1);% separate input background image to r,g,b channels
back_g = back(:,:,2);
back_b = back(:,:,3);

temp_r = combine_image(man_r,back_r); % process using function()
temp_g = combine_image(man_g,back_g);
temp_b = combine_image(man_b,back_b);

final_image = uint8(zeros(size(man)));
final_image(:,:,1)= temp_r; % step 7 -combine output images to a single color image
final_image(:,:,2)= temp_g;
final_image(:,:,3)= temp_b;

figure;
imshow(final_image);

```

##### The Function - combine_image()
``` matlab
function temp = combine_image(man,back)
    man_b= im2bw(man,0.99); %  step 1
    back_b = im2bw(back);
    not_back = not(back_b); % step 2
    com = and(man_b,not_back); % step 3 - Mask 1
    com1 = not(com); % step 4 - Mask 2
    with_man = com1.*double(man); % step 5
    with_tree = com.*double(back);
    sz= size(com);
    for i = 1:sz(1,1) % step 6
        for j=1:sz(1,2)
            temp(i,j)=max(with_man(i,j),with_tree(i,j));
        end
    end
    temp = uint8(temp);
end
```
I know this post was a bit long, but this is a cool example of some basic image processing techniques. If you want to learn more click [here](http://onlinelibrary.wiley.com/book/10.1002/9780470689776){:target="blank"} for a reference to a great book.

###### So until next time.
#### Cheers !!
