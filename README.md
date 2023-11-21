# 1. Run Experiments
## Part 1: Setting up Environment
### Part 1a: Dependencies
Note: It is highly recommended to use a Google Colab environment to run this code. To run locally, there may need to be some more additional steps required to get this functional such as getting packages that Colab has pre-installed or issues with file paths.

Note: Make sure the version that the version of Python being is used is 3.6+.

To get dependencies to run the code, there are two options:

> Option 1: Clone Repository from GitHub

```
git clone https://github.com/ShreChinno/negation-and-nlu.git 
```
This is a forked repository of the original author's code. I have made changes to it for the paper. This repository contains the necessary datasets and dependencies to run the code. If there is a need to change the datasets, please refer to Part 2. With this, all that is needed is the notebook file.

> Option 2: Use code provided in Zip File

The code provided has the same code that comes from the GitHub Repository. However, because the original authors had a specific procedure in mind for the ConanDoyle-Neg Dataset, two necessary directories have to be downloaded to regain full functionality.

Download the two directories from the following link:

```https://drive.google.com/drive/folders/1BM3V9aQqGk_4RLLBKehReYtq_ckdH2Gs?usp=sharing```

You may need to unzip them. Google Drive may change the names of the directories, so please rename them to their respective names as they are in Google Drive. Once they have been unzipped. Put these directories in ```<path to negation-and-nlu repository>/negation-and-nlu/cue-detector/```

Follow these next steps:

```
pip install --upgrade pip
pip install torch torchvision
pip install -U spacy
python -m spacy download en_core_web_sm
pip install transformers
pip install datasets
pip install git+https://github.com/kmkurn/pytorch-crf
```
This will install the important packages for the code. As noted before, this is assuming the code is running on a Google Colab environment. There may be a need to install more packages depending on the environment being used.

```
cd <path to negation-and-nlu repository>/negation-and-nlu/cue-detector/model/pre-trained/roberta_base
wget https://huggingface.co/roberta-base/resolve/main/config.json
wget https://huggingface.co/roberta-base/resolve/main/merges.txt
wget https://huggingface.co/roberta-base/resolve/main/pytorch_model.bin
wget https://huggingface.co/roberta-base/resolve/main/tokenizer.json
wget https://huggingface.co/roberta-base/resolve/main/vocab.json
cd ../../../
```
This will download the model being used in this paper: ```RoBERTa```. Please make sure to change the path as necessary.

### Part 1b: Change Paths
Some of the code relies on paths to specific files and dependencies. Most of these have been defined within the ```negation-and-nlu/cue-detector/config/train.json``` and ```negation-and-nlu/cue-detector/config/predict.json```. If there is an error that arises due to an invalid path, it is likely due to what has been defined in these two files. Please use the following format to change the path

```
<path to negation-and-nlu repository>/<path to specified resource> 
```

This error may arise in the code itself. Please follow the above note to change paths in the code to resolve the issue. 

### Part 1c: Modify Datsets

> If using Option 1:

The datasets and model being used for this paper have already been put into the repository to be used by the code, so you may skip this. If there is a need to change the datasets, I have provided mechanisms to change them. Within the notebook, in ```Part 2: Prepare Data```, there is a boolean under each dataset that determines if the data should be reduced. Please modify this code to make use of different variations of the same dataset.

> If using Option 2:

Running the ```Part 2: Prepare Data``` is mandatory. You may also make changes to the datasets just like with Option 1 if wanted, but it is not necessary as I have already set it up to what I ran my experiments with.

## Part 2: Run Code

If using the notebook, please run the the following cells in this order:
1. All cells in ```Part 1: Setting Up Environment``` 
2. All cells in ```Part 2: Prepare Data```
3. All cells in ```Import Packages for Training and Evaluation```
4. All cells in ```Part 3: Train Model```
5. All cells in ```Part 4: Evaluate Model``` 
6. All cells in ```Part 5: Extension: Correlation Negation Cue Detection in Datasets to Determine Sentiment```

If not using the notebook, please run the steps in ```Part 1: Setting Up Environment``` in a shell, then run the rest of the code as python files.

# References

The borrowed code comes from ```https://github.com/mosharafhossain/negation-and-nlu```. This is the repository that contains the code of the original authors. I have forked this repo, and I have modified to work with my code.

The code that was borrowed and changed were the ```train.py``` and ```evaluate.py``` files. I have removed dead code that was not necessary to run these experiments. I also added some code to the ```evaluate.py``` file to evaluate a series of datasets instead of one dataset at a time. I aggreagated the file paths within two lists. I then added a for loop that would use these lists in order to carry out its evaluation phase. As long as the dataset is compatitable, and it is within the ```negation-and-nlu/cue-detector/datasets``` directory, it should run its analysis on it.

As for code I have written, the code for ```Part 2: Prepare Data``` and ```Part 5: Extension: Correlation Negation Cue Detection in Datasets to Determine Sentiment``` was my own. I wrote them to work in tangent with the code I borrowed from the original authors. The original code did not contain any datasets to run evaluation on, so I had to grab them from HuggingFace. I also wrote the code to run my extension idea which was not done by the original work.


# Datasets

All datasets have been provided in the repository. These are the URLs to where I have retrieved the datasets from. ConanDoyle-Neg was provided by the original authors which was likely modified. For this reason, a special link has provided for this.

ConanDoyle-Neg - Annotated Negation from Sir Arthur Conan Doyle's Stories.

> This data comes from the original authors from the GitHub Repo ```https://github.com/mosharafhossain/negation-and-nlu``` within the ```outputs``` and ```data``` directors in ```negation-and-nlu/cue-detector```. They can be downloaded from a Google Drive link: ```https://drive.google.com/drive/folders/1BM3V9aQqGk_4RLLBKehReYtq_ckdH2Gs?usp=sharing```.

CommonSenseQA - Contains Common Sense Questions.

> Retrived from ```https://huggingface.co/datasets/commonsense_qa```

COPA - Contains a Premise, Question, and options to choose from.

> Retrived from ```https://huggingface.co/datasets/pkavumba/balanced-copa```

QQP - Textual Similarity and Paraphrasing Dataset. Uses pairs of questions and have the model determine if they are paraphrases.

> Retrived from ```https://huggingface.co/datasets/glue/viewer/qqp```

STS-B - Textual Similarity and Paraphrasing Dataset. Uses pairs of text and have the model determine if they are semantically similar.

> Retrived from ```https://huggingface.co/datasets/glue/viewer/stsb```

QNLI - Inference Dataset. Model decides if text is a reasonable answer for a question.

> Retrived from ```https://huggingface.co/datasets/glue/viewer/qnli```

WiC - Word Sense Dismbiguation Dataset. Model decides if two words are used with the same intention (meaning).

> Retrived from ```https://huggingface.co/datasets/super_glue/viewer/wic```

WSC - Coreference Resolution Dataset. Model decides if pronoun and noun are co-refrential (both refer to the same object).

> Retrived from ```https://huggingface.co/datasets/super_glue/viewer/wsc```

SST-2 - Sentiment Analysis Dataset. Model decides the sentiment (positive or negative) of the text.

> Retrived from ```https://huggingface.co/datasets/sst2```

Sentiment140 - Sentiment Analysis Dataset. Collection of Tweets that have varying sentiment.

> Retrived from ```https://huggingface.co/datasets/sentiment140```