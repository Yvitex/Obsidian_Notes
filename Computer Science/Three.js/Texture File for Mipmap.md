---
aliases: [how to choose the texture format for Three.js Texturing]
---
# Texture
 There are 3 main important factors to consider
 - The weight
 - The size
 - The data
 - 
There are 2 common kinds of texture file to consider
- Jpg - lossly compression but lighter
- Png - lossless compression but heavier

If we want an accurate [[Three.js Textures]] values then we use png, if not, use jpg. We could compress images using this website called [TinyPng](https://tinypng.com/). If you have jpg or png files you need to compress, use that website. 

Remember that the smaller the size or weight of the texture, the higher its performance is to the [[GPU]]. [[Mipmapping]] will increase the number of pixels which is why it is not advisable to use LinearFilter extensively and use NearestFilter instead in [[Magnification Filter]] or [[Minification Filter]] and disable [[Mipmapping]]. Textures are indeed stored in the [[GPU]] and they have limited space. Therefore it is a common sense that we provide small sized files as much as possible. 

Because sometimes we really need [[Mipmapping]], and this method will divide the original pixel by half until it became 1 by 1, we need to provide files that are in power of 2 size such as
- 512 x 512
- 1024 x 1024
- 512 x 2048

If we need to have transparency, then we must use 2 jpg files for [[Color Texture]] and [[Alpha Texture]] for faster load, or else we could use a single png file with color + transparency included. This has less images to send to the [[GPU]]

In case for [[Normal Texture]], we always need a png file because it needs to be accurate. and png is lossless compression. 

We could combine data using red green and blue channels. 

Website for downloading texture
- [3dTextures.me](https://3dtextures.me/)
- [Arrowtextures](https://www.arroway-textures.ch/)
- [Others](https://www.creativebloq.com/3d-tips/find-high-res-textures-1232646)

Or create your own in photoshop or [substance designer](https://www.substance3d.com/)

