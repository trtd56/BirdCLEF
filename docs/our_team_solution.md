Our Solution

# X place solution

## teyo  part

## shinmura part

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