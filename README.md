# **Brainhack-TIL-2022**

## **Introduction**
My team and I participated in the Brainhack TIL 2022 hackathon organized by DSTA. The hackathon was an AI focused with two tasks:
1. CV Task to identify fallen people in still images.
2. NLP Task to classify a short audio clip into 5 categories.

We ended up 18th place overall for the qualifiers and was unable to get into the finals. This was our workflow during the hackathon, as well as improvements and lessons learnt from other competitors.

This README provides a overview of our process and learning points. The actual code can be found in the Python Notebooks.
___

## **NLP**
For the NLP portion, the training data set contained 3500 labelled short audio clips of varying lengths. The labels were Neutral, Anger, Happy, Sad, Fear. A big help for our process was from an [article by Ketan Doshi](https://towardsdatascience.com/audio-deep-learning-made-simple-sound-classification-step-by-step-cebc936bbe5) on Medium.

A brief breakdown of our process is as follows:

1. Import audio clips with Librosa library and standardise length to be 5 seconds.
2. Convert all audio clips to stereo with the same sampling rate. 
3. Apply data augmentation via the form of white noise, shifting the entire audio slightly, stretching the audio.
4. Convert augmented and non-augmented audio clips into MFCC (Mel Frequency Cepstrum Coefficient).
5. Perform a stratified train test split and run training data through ResNet18 and validate.


Mel Spectrogram          |  MFCC
:-------------------------:|:-------------------------:
| ![](images%5Cangry_0fb05c8a26.png)| ![](images%5Cangry_0ae2776d1c.png)

We initially converted and processed the images in the form of Mel Spectrograms but realised that an MFCC representation would better capture the nuances of human speech and would likely be better.

For the model choice, we tried a basic CNN and a pre-trained ResNet18. We experienced slightly better results with ResNet18 and ended up going with it in the end. At this point of time, the choice of models was based on the training results. We had issues trying other pre-trained models due to inexperience.

After applying the data augmentations, we had a total of 14000 training images (3500 * 4). Due to time constraints, we were unable to run all the images through ResNet18 and manage to run about half of them through. 

![](images%5CNLP%20Score.PNG)

On our validation set, we achieved a accuracy of approx 0.52. During the finals, the accuracy dropped to approx 0.29.

## **Learning Points**

After the hackathon ended, we got advice from other participants that did better (0.78 acc) and learnt a bit more from their workflow.
> 1. Using transformers instead of converting to MFCC to directly extract features from the audio clips. 
> 2. Not applying execessive data augmentation like stretching as they may affect emotional accuracy.
> 3. Using [Wav2Vec2-XLSR-53](https://huggingface.co/facebook/wav2vec2-large-xlsr-53) as a pre-trained model.

While our results for the NLP task were not great, going through this project was a very informative experience that will help in future projects.

___

## **CV**