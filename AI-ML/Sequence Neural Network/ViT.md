## Idea
![[ViT.png]]
- Traditionally, [[Transformer]]-based architecture is used for NLP tasks
- **ViT** brings Transformer to Computer Vision by using its **Encoder** to **generate embedding** for **images**
## Image Patching & Embedding
![[image patching vit.png]]
- An input image is divided into **patches**
- The original paper used the **size 16x16** for each **patch**
- These **patches** are equivalent with **words** in NLP
- These patches are **flattened** and fed into a neural network to generate the **image embedding** of each **patch**
- It also has [[Transformer#Positional Embedding|Positional Embedding]] layer to retain the information about the order of each patch in the image
## The Rest
- The **image embedding** vector is then fed to the usual Encoders stack to extract the features of the image
- The features can be used for CNN tasks
## ViT VS CNN
- **ViT** works better than **CNN** when we have **huge data** (millions)
	- This is because ViT can learn the images *holistically* by understanding the context from each patches
	- CNN learns *hierarchically* by extracting features one by one
- When the data is **relatively small**, **CNN** usually works better