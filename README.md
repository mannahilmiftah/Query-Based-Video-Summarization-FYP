# Query-Based-Video-Summarization-FYP

## Problem Statement
The goal of this project is to create an end-to-end deep learning solution for a query based video summarization, where the system automatically generates concise yet informative summaries of input videos pertaining to the query provided by the user. The summarization process should capture the most important scenes, actions, events, and content from the video while maintaining coherence and avoiding redundancy and
fulfilling all the aspects of user provided context.

## Dataset
Ego4D is a large-scale, multi-modal dataset for egocentric (first-person) video understanding. It consists of over 3,000 hours of video recordings from 700 unique individuals, capturing daily activities like cooking, cleaning, and socializing. The dataset includes:
1. 3,000+ hours of egocentric video.
2. 40,000+ annotated episodes (short video clips).
3. 12,000+ hours of audio narration.
4. 2.5 million+ annotated objects, actions, and events.
The Ego4D dataset has been limited to the use case of cleaning and laundry videos for this project. Total 44 videos of varying length (3 to 30 minutes) were downloaded and used for training the captioning model.
The data contains the description of frames, frame number and time stamp along with the video.

## Methodology
The process of video summarization entails two primary tasks: image captioning and retrieving frames similar to a user query. For this purpose, the following steps were performed:
1. A given video (30 FPS) is broken down into its constituent frames.
2. All those frames were selected for training whose descriptions were given in the dataset.
3. These frames are saved as numpy arrays and PIL Images.
4. A hugging face dataset is created which contains frames and their respective descriptions.
5. A combination of two large pretrained models (ViT and GPT-2) is finetuned over this custom dataset.
6. For each video, a description is generated every 15th frame (2 frames’ descriptions generated per second).
7. The set of these generated descriptions along with their respective frame numbers are made into documents of LlamaIndex.
8. These nodes are stored into VectorStoreIndex which acts as a retriever.
9. The retriever is then queried with the user query, and it outputs top 60 frames similar to the user query.
10. The overlapping frames are eliminated to avoid repetition of frames in a summary.
11. For every similar frame preceding and succeeding 4-second segments are selected alongside them to maintain coherence within the summary.
12. The generated summaries are evaluated against human generated ground truth. The evaluation metrics used are recall and F1-score.

## Video Summaries (Output)
https://drive.google.com/drive/folders/1eZ6foFICWWHc17HG7CyWajTthZsbqtEk?usp=drive_link

## Dataset
https://drive.google.com/drive/folders/1evcIC95NbJWVBRFLEFjg7ooLpM0LDcze?usp=drive_link
