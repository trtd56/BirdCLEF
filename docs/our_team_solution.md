Our Solution

# X place solution

[It](https://www.kaggle.com/c/birdclef-2021/discussion/233454) said bagging works good in this competition.
We thought so too from us experiment, so our strategy is training various model and they ensemble.

## teyo  part

## toda part

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


## shinmura part
I mainly developed post-processing (And [hand labeing](https://www.kaggle.com/c/birdclef-2021/discussion/239911)).  

Our post-processing improved LB significantly (**LB 0.65 -> 0.70** jump up).  
Our post-processing is 7 ideas.

### 1.Threshold Optimization
In sound event detection, threshold optimization seem to be big impact. So I want to do threshold optimization, but there is domain shift in this competition. The normal way (Using train_short_audio) was impossible.

So I focused on the "nocall" of train_soundscape.


### 2.prediction 

### 3.Delete head and tails

### 4.Focus site 
Similar to toda part, I made a list of birds that frequently appear in each site.  
 (SSWlist, CORlist, COLlist, SNElist) Each list contains about 50 species of birds.
 
In inference time, I delete prediction for bird species not included in the list for each site.
```
prediction[targetlist==False] = 0
```

This technique reduce false positive.

### 5.Bonus time at each species
In train_soundscape, the same bird is always singing throughout a clip (e.g. runwar, sonspa).

So, birds that appear more in prediction are more likely to be singing more (a lot of false negative). Therefore, I lowered the threshold for birds that appear a lot in prediction. It is bonus time!

```
def bonus_time(prediction, thresh): #prediction(120,397)=0 or 1, thresh(397)
    prediction_count = np.sum(prediction, axis=0)
    for i in range(len(prediction_count)):#397
        if prediction_sount[i] > 20: # over 20 times appear
            thresh[i] = thresh[i] - 0.1
    return thresh
```

This technique reduce false negative.

### 6.Threshold down at special species
In train_soundscape, certain birds appeared more frequently(e.g. runwar, reevir1). 

It is highly likely that these bird will appear frequently in the test audio. So I lowered the threshold for these birds (=special species).

Special species are
+ runwar
+ reevir1
+ sonspa
+ grycat
+ eawpew

### 7.Threshold down at SNE special species
Above special species is SSW and COR species. In test audio, there are also "COL" and "SNE".
