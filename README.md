# IAT481A2
Speech Emotion Recognition Dataset Analysis
  
*worked on code together with Sienna Wu*  


*CompletedA2 and ReadMe are my submissions*

For my assignment, I chose to have RAVDESS, EmoDB, and merged data. This is simply for my own convenience and ease of mind when I work with separated data and merged data. I think being able to see the two datasets separately and then seeing the merged result allows me to understand how each dataset impacts insights like the standard deviation of features, gender ratios, and emotion ratios. 

## Category Mismatches

In order to avoid errors and category mismatches (regarding emotions), I first had to make sure both RAVDESS and EmoDB had the same number and the same emotions as each other. Since EmoDB originally had 7 and RAVDESS had 8, I simply wrote down the emotions present in both datasets and eliminated the ones that did not overlap. Consequently, this meant that there were only 6 emotions left (anger, disgust, fear, happy, neutral, and sad). Luckily, the emotions coded in these datasets were small so I was able to do it manually. If it were larger I think I would have to write a bit more code checking similar emotions and deleting the ones that were not.

## Gender Balance 
### RAVDESS 
![chrome_LD4UKsrgxl](https://github.com/merfurfu/IAT481A2/assets/55826426/19a7fe8d-6f20-4164-abbf-fd7a7e0199d7)
This will be a common theme throughout my report, but I find that RAVDESS has very equal and balanced data instances. I can see this here with exactly equal split between male and female. 

### EmoDB
![chrome_77Q6jIFxWN](https://github.com/merfurfu/IAT481A2/assets/55826426/0fb01b1c-bf50-4e83-b4f8-4882ad30f574)
For the EmoDB dataset, I think I might have coded something wrong? The description of the data has 5 male and 5 female voices, but the plot shows that there are more female voices. 

### Merged
![chrome_NIvEj4fgtl](https://github.com/merfurfu/IAT481A2/assets/55826426/9a67eab9-c0ee-4919-8e06-566b4710a3bf)
In the merged dataset, the plot is similar to EmoDB's gender balance since RAVDESS has an even split between genders. Hopefully, the amount of data would decrease any large variances in data points. 

## Emotional Balance
### RAVDESS  

![chrome_3CWCRgS3Cj](https://github.com/merfurfu/IAT481A2/assets/55826426/e8400470-2a85-4e04-b6a8-304f47c0e0cc)
For the RAVDESS dataset, you can see that the original 8 emotions (anger, calm, disgust, fear, happy, neutral, surprised, and sad), they are all split evenly aside from neutral (which makes sense since neutral does not have intensity). The even split among all emotions would mean that RAVDESS would be a great model to train data on. 


### EmoDB

![chrome_EU5HEwxBqC](https://github.com/merfurfu/IAT481A2/assets/55826426/086d7f80-4b9e-4ebb-a29f-6328c3909a8a)
For the EmoDB dataset, you can see there is a clear difference in the frequency of emotions (anger, boredom, disgust, fear, happy, neutral, and sad). It appears that anger appears the most, with disgust appearing the least. The other categories appear with around the same frequency. An interesting observation is that neutral appears with around the same frequency as boredom. 

### Merged
![chrome_Z37abUvlLy](https://github.com/merfurfu/IAT481A2/assets/55826426/8d14ee40-b3e9-40cc-bcdf-fcbfcdfd6ec1)
In the cleaned and merged dataset with only common emotions, the dataset changes from how we saw it in RAVDESS. It follows the shape of the EmoDB, which is not surprising at all since RAVDESS is almost completely even among all emotion categories (aside from neutral). 

## Feature Analysis 
### RAVDESS
![chrome_eBnCQHTJb8](https://github.com/merfurfu/IAT481A2/assets/55826426/838b5360-4cc3-4e29-b770-13e2b8475f41)
![chrome_ztlTUo4zsN](https://github.com/merfurfu/IAT481A2/assets/55826426/c335e23c-607b-47c5-9989-35bebf3e596e)
When extracting our features, you can see that RAVDESS data has a similar standard deviation between chromagram and spectrogram features, however, when you look at MFCC features, the standard deviation jumps to 98.494. This is not great and means that we should move onto scaling our data. 

### EmoDB 
![chrome_M0krP3f8sV](https://github.com/merfurfu/IAT481A2/assets/55826426/1f3bc18b-26fa-4bf3-a3d0-aa0de5c1d706)
![chrome_E5kjoJ3ILA](https://github.com/merfurfu/IAT481A2/assets/55826426/c8a4c68d-4a93-416d-9171-55fa82c65fb3)
In EmoDB we can see that spectrogram and MFCC features have standard deviations not similar but also not close together. It looks reasonable between chromagram, spectrogram, and MFCC, however, it can always be scaled. 

### Merged 
![chrome_Xpbc83K6MR](https://github.com/merfurfu/IAT481A2/assets/55826426/6e6f405f-2b8a-4cf3-8c29-adacf523eeee)
![chrome_ktQz1TwhKL](https://github.com/merfurfu/IAT481A2/assets/55826426/5791c89c-2678-4536-b2ce-70e9c5967de3)
The features extraction for the merged dataset shows a similar pattern to the RAVDESS dataset, with chromogram and spectrogram with sds in a similar range and MFCC with a standard deviation much much higher than the two (86.164 vs 0.094 and 9.730). This dataset 100% needs to be scaled. 


### Scaling/Min Maxing

![chrome_PcsWAu80I0](https://github.com/merfurfu/IAT481A2/assets/55826426/bf7b22db-6714-44bc-a2d2-36400f4a35e1)
![chrome_bHb4kh6fja](https://github.com/merfurfu/IAT481A2/assets/55826426/ceee1c3a-58a6-4456-9221-d0ac96d07033)
![chrome_MS4QVReULz](https://github.com/merfurfu/IAT481A2/assets/55826426/ddcd650d-ea0a-4e32-bfb8-0e14972ce392)

After scaling, we can see that the standard deviations for all three datasets are similar to one another with no drastic outliers. Of course, the most drastic change is the sd for MFCC of the merged dataset, going from 86.164 to 0.175. This shows us that scaling is the correct response and allows for us to use these scaled datasets for future modelling. 

## Overall Thoughts & Analysis

### Data Preprocessing
The most difficult part (to me) of this assignment was extracting and cleaning data. From the tutorial code, I sort of knew what to do which was to use load_data() to extract emotion data. This was fairly straightforward for both RAVDESS and EmoDB. However, I ran into difficulties with extracting gender. I eventually hardcoded a dict listing all the numbers from 1-24 and the male and female of each number. I think that there would be a more straightforward way of passing the extracted value ("0X") as an int and then using an if-else statement to see if the int is divisible by 2 to determine gender. For EmoDB, since there were just 10 and no particular rhyme or reason (I could find) to the gender and number assignment, I also just hard coded it. 

### Merging Datasets
While merging datasets, I had an idea of using either .vstack() or .hstack() since .hstack() was used previously. After going to office hours, Maryiam gave us a hint that it needs to be merged vertically, so I knew I wanted to use .vstack(). However, after using .vstack() it gave me an error and I tried .concatenate() instead. .concatenate() worked wonderfully, and so I used that to merge emotions (emotions, emotionsberlin), gender (genderRAV, genderEmo), and features (features, features). 

### Errors
The errors I mostly ran into were about mismatched indexes (when trying to merge), missing parameters or invalid operations (deleting emotions from datasets), and key errors (when trying to extract gender from EmoDB). 
![chrome_KrSIUW9gMJ](https://github.com/merfurfu/IAT481A2/assets/55826426/90993b93-71b6-46c9-990c-b7b8616c4ff4)
I spent a little too long trying to work out why my code returned only "10.wav" before realizing that I needed to code an additional step before that stripping the ".wav" from file_name, and then splitting it to find gender. When trying to delete non common emotions, I tried to delete from emotion_list in the barplot code chunks, before Maryiam suggested I just look directly at the code. I still ran into a few more errors mostly on how to write it, but eventually np.delete() while passing the list and emotion name yielded best results. 


I learned a lot about populating arrays through functions, writing my own functions, and splitting strings. I think my favourite part of this assignment was running load_data and seeing all the emotions be translated from numbers (but as a string) into actual written emotions (and same with gender). It was satisfying having this code work out after a lot of trial and error. 

## Citations 

Livingstone SR, Russo FA (2018) The Ryerson Audio-Visual Database of Emotional Speech and Song (RAVDESS): A dynamic, multimodal set of facial and vocal expressions in North American English. PLoS ONE 13(5): e0196391. https://doi.org/10.1371/journal.pone.0196391.

Sendlmeier, W et al. (2020) EmoDB dataset, 
https://www.kaggle.com/datasets/piyushagni5/berlin-database-of-emotional-speech-emodb/data 

Used code from tutorial:
Zahoor, M (2023), Week-2_Data_Preprocessing, https://github.com/IAT-ExploringAI-2024/Week-2_Data_Preprocessing
