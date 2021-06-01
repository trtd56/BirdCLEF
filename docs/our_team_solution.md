Our Solution

# X place solution

[It](https://www.kaggle.com/c/birdclef-2021/discussion/233454) said bagging works good in this competition.
We thought so too from us experiment, so our strategy is training various model and they ensemble.

## teyo  part

my aproach is cnn classifier model

### Data Preparation

I cut out 5 seconds of audio from train short audio.
The training data was converted to logmel using torchlibrosa, and then increased to 3 channels.
I used delta to increase channels, referring to past competitions. There was not much difference from simple repeat.

Reference [Cornell Birdcall Identification 4-th place solutinon](https://www.kaggle.com/vladimirsydor/4-th-place-solution-inference-and-training-tips)

### model

rexnet_200

The rexnet 200 was unusually strong:)
I keep track of the f-1 for the train sound scape data and use the best f-1 weight.

for ensemble [densenet161, efficientnetv2_s, resnext50_32x4]

not worked efficientnetb0-4,resnest50d

### data augmentation

+ NoiseInjection
+ PinkNoise
+ RandomVolume
+ SpecAugmentation (do in model)
+ [Modified Mixup](https://www.kaggle.com/c/birdsong-recognition/discussion/183199)
  + increase 0.02 in public LB

### other settings

+ split
  + StratifiedKFold
    + mainly 5 fold
+ Scheduler
  + CosineAnnealingWarmRestarts
  + 30 epochs
  + lr=1e-4
  + min_lr=1e-6
+ optimizer
  + Adam
+ criterion
  + BCEWithLogitsLoss

## shinmura part
I mainly developed post-processing (And [hand labeing](https://www.kaggle.com/c/birdclef-2021/discussion/239911)).  

Our post-processing improved LB very well (**LB 0.65 -> 0.70** jump up).  
Our post-processing is 7 ideas. But it's too long to write here.

If you want to know our post-processing, please comment me.
Then I will build another thread.

## toda part

**※ My model has not used in our team final submission, so this part is "I try, but it was not working".**

I have used the ResNet18 based SED model.
My ingenuity points are there three:

### 1. add background noise 

In order to make the audio of the training data as close as possible to the test data, I used the data of ESC50 to add noise to the training data. The selected audio are listed below.

airplane, rain, water_drops, crackling fire, engine, insects, crickets, frog, wind

I also adjusted Gain to give variation to the volume of the bird's voice, but this did not work.

### 2. make model each site

Birds that are observed differ depending on the area, and it is expected that some birds, such as migratory birds, will be observed only for a specific period. I decided to make a specialized model.

Specifically, the radius was within 1000 km from the observation point of the test data, and the period was narrowed down with a buffer of one month before and after the target period (for example, January to August for SSW).

After narrowing down, we sorted by rating of each audio file and extracted the first 5 seconds of the top 300.

The dataset is here:
- SSW: https://www.kaggle.com/takamichitoda/birdclef-ssw-max300
- SNE: https://www.kaggle.com/takamichitoda/birdclef-sne-max300
- COR: https://www.kaggle.com/takamichitoda/birdclef-cor-max300
- COL: https://www.kaggle.com/takamichitoda/birdclef-col-max300

### 3. generate nocall data

I add nocall data that made from other site.
The method making nocall datasets is reversed the method making datasets each site.
I extracted audio that is more than 1000km away from each site and is not in the target period.

nocall data is here: https://www.kaggle.com/takamichitoda/birdclef-nocall-each-site
