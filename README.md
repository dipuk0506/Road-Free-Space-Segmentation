# Road Lane Segmentation
 - Convolution Neural Network for segmentation of the road lane.
 - Models : [SegNet](https://arxiv.org/abs/1511.00561), [U-Net](https://arxiv.org/abs/1505.04597), [LinkNet](https://arxiv.org/abs/1707.03718), [PSPNet](https://arxiv.org/pdf/1612.01105.pdf)

## Load Dataset
```python
def make_dataset(image_list, mask_list, img_size=(360,480)):
    images = []
    masks = []
    
    for img, mask in zip(image_list, mask_list):
         images.append(cv2.resize(cv2.imread(img), img_size))
         masks.append(binarylab(cv2.resize(cv2.imread(mask), img_size)))
        
    images = np.array(images)
    masks = np.array(masks)
    
    return images, masks
```

## Build Model
```python
class_weighting= [0.2595, 0.1826, 4.5640, 0.1417, 0.9051, 0.3826, 9.6446, 1.8418, 0.6823, 6.2478, 7.3614, 1.0974]
```
```python
model_checkpoint = ModelCheckpoint('model-epoch-{epoch:02d}-val_loss-{val_loss:.2f}.hdf5', monitor='val_loss', save_best_only=True)
model_earlystopping = EarlyStopping(monitor='val_loss')
```
### SegNet
    _________________________________________________________________
    Layer (type)                 Output Shape              Param #   
    =================================================================
    input_2 (InputLayer)         (None, 360, 480, 3)       0         
    _________________________________________________________________
    conv2d_21 (Conv2D)           (None, 360, 480, 64)      1792      
    _________________________________________________________________
    batch_normalization_21 (Batc (None, 360, 480, 64)      256       
    _________________________________________________________________
    activation_21 (Activation)   (None, 360, 480, 64)      0         
    _________________________________________________________________
    conv2d_22 (Conv2D)           (None, 360, 480, 64)      36928     
    _________________________________________________________________
    batch_normalization_22 (Batc (None, 360, 480, 64)      256       
    _________________________________________________________________
    activation_22 (Activation)   (None, 360, 480, 64)      0         
    _________________________________________________________________
    max_pooling2d_4 (MaxPooling2 (None, 180, 240, 64)      0         
    _________________________________________________________________
    conv2d_23 (Conv2D)           (None, 180, 240, 128)     73856     
    _________________________________________________________________
    batch_normalization_23 (Batc (None, 180, 240, 128)     512       
    _________________________________________________________________
    activation_23 (Activation)   (None, 180, 240, 128)     0         
    _________________________________________________________________
    conv2d_24 (Conv2D)           (None, 180, 240, 128)     147584    
    _________________________________________________________________
    batch_normalization_24 (Batc (None, 180, 240, 128)     512       
    _________________________________________________________________
    activation_24 (Activation)   (None, 180, 240, 128)     0         
    _________________________________________________________________
    max_pooling2d_5 (MaxPooling2 (None, 90, 120, 128)      0         
    _________________________________________________________________
    conv2d_25 (Conv2D)           (None, 90, 120, 256)      295168    
    _________________________________________________________________
    batch_normalization_25 (Batc (None, 90, 120, 256)      1024      
    _________________________________________________________________
    activation_25 (Activation)   (None, 90, 120, 256)      0         
    _________________________________________________________________
    conv2d_26 (Conv2D)           (None, 90, 120, 256)      590080    
    _________________________________________________________________
    batch_normalization_26 (Batc (None, 90, 120, 256)      1024      
    _________________________________________________________________
    activation_26 (Activation)   (None, 90, 120, 256)      0         
    _________________________________________________________________
    conv2d_27 (Conv2D)           (None, 90, 120, 256)      590080    
    _________________________________________________________________
    batch_normalization_27 (Batc (None, 90, 120, 256)      1024      
    _________________________________________________________________
    activation_27 (Activation)   (None, 90, 120, 256)      0         
    _________________________________________________________________
    max_pooling2d_6 (MaxPooling2 (None, 45, 60, 256)       0         
    _________________________________________________________________
    conv2d_28 (Conv2D)           (None, 45, 60, 512)       1180160   
    _________________________________________________________________
    batch_normalization_28 (Batc (None, 45, 60, 512)       2048      
    _________________________________________________________________
    activation_28 (Activation)   (None, 45, 60, 512)       0         
    _________________________________________________________________
    conv2d_29 (Conv2D)           (None, 45, 60, 512)       2359808   
    _________________________________________________________________
    batch_normalization_29 (Batc (None, 45, 60, 512)       2048      
    _________________________________________________________________
    activation_29 (Activation)   (None, 45, 60, 512)       0         
    _________________________________________________________________
    conv2d_30 (Conv2D)           (None, 45, 60, 512)       2359808   
    _________________________________________________________________
    batch_normalization_30 (Batc (None, 45, 60, 512)       2048      
    _________________________________________________________________
    activation_30 (Activation)   (None, 45, 60, 512)       0         
    _________________________________________________________________
    conv2d_31 (Conv2D)           (None, 45, 60, 512)       2359808   
    _________________________________________________________________
    batch_normalization_31 (Batc (None, 45, 60, 512)       2048      
    _________________________________________________________________
    activation_31 (Activation)   (None, 45, 60, 512)       0         
    _________________________________________________________________
    conv2d_32 (Conv2D)           (None, 45, 60, 512)       2359808   
    _________________________________________________________________
    batch_normalization_32 (Batc (None, 45, 60, 512)       2048      
    _________________________________________________________________
    activation_32 (Activation)   (None, 45, 60, 512)       0         
    _________________________________________________________________
    conv2d_33 (Conv2D)           (None, 45, 60, 512)       2359808   
    _________________________________________________________________
    batch_normalization_33 (Batc (None, 45, 60, 512)       2048      
    _________________________________________________________________
    activation_33 (Activation)   (None, 45, 60, 512)       0         
    _________________________________________________________________
    up_sampling2d_4 (UpSampling2 (None, 90, 120, 512)      0         
    _________________________________________________________________
    conv2d_34 (Conv2D)           (None, 90, 120, 256)      1179904   
    _________________________________________________________________
    batch_normalization_34 (Batc (None, 90, 120, 256)      1024      
    _________________________________________________________________
    activation_34 (Activation)   (None, 90, 120, 256)      0         
    _________________________________________________________________
    conv2d_35 (Conv2D)           (None, 90, 120, 256)      590080    
    _________________________________________________________________
    batch_normalization_35 (Batc (None, 90, 120, 256)      1024      
    _________________________________________________________________
    activation_35 (Activation)   (None, 90, 120, 256)      0         
    _________________________________________________________________
    conv2d_36 (Conv2D)           (None, 90, 120, 256)      590080    
    _________________________________________________________________
    batch_normalization_36 (Batc (None, 90, 120, 256)      1024      
    _________________________________________________________________
    activation_36 (Activation)   (None, 90, 120, 256)      0         
    _________________________________________________________________
    up_sampling2d_5 (UpSampling2 (None, 180, 240, 256)     0         
    _________________________________________________________________
    conv2d_37 (Conv2D)           (None, 180, 240, 128)     295040    
    _________________________________________________________________
    batch_normalization_37 (Batc (None, 180, 240, 128)     512       
    _________________________________________________________________
    activation_37 (Activation)   (None, 180, 240, 128)     0         
    _________________________________________________________________
    conv2d_38 (Conv2D)           (None, 180, 240, 128)     147584    
    _________________________________________________________________
    batch_normalization_38 (Batc (None, 180, 240, 128)     512       
    _________________________________________________________________
    activation_38 (Activation)   (None, 180, 240, 128)     0         
    _________________________________________________________________
    up_sampling2d_6 (UpSampling2 (None, 360, 480, 128)     0         
    _________________________________________________________________
    conv2d_39 (Conv2D)           (None, 360, 480, 64)      73792     
    _________________________________________________________________
    batch_normalization_39 (Batc (None, 360, 480, 64)      256       
    _________________________________________________________________
    activation_39 (Activation)   (None, 360, 480, 64)      0         
    _________________________________________________________________
    conv2d_40 (Conv2D)           (None, 360, 480, 64)      36928     
    _________________________________________________________________
    batch_normalization_40 (Batc (None, 360, 480, 64)      256       
    _________________________________________________________________
    activation_40 (Activation)   (None, 360, 480, 64)      0         
    _________________________________________________________________
    output (Conv2D)              (None, 360, 480, 12)      780       
    =================================================================
    Total params: 17,650,380
    Trainable params: 17,639,628
    Non-trainable params: 10,752
    _________________________________________________________________

### result 
![png](output_28_0.png)
![png](output_32_0.png)

### U-Net

## References
 - https://github.com/preddy5/segnet/blob/master/Segnet.ipynb
 - https://gist.github.com/melgor/0e43cadf742fe3336148ab64dd63138f
 - https://github.com/mathildor/TF-SegNet/blob/master/AirNet/layers.py
