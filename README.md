# UDA_FinalProject_Hu_Code

## Introduction

This is the codebase for the 4th and Final Coursework for Unstructured Data Analysis (UDA).

Here we look at the semi-supervised approach on unlabelled financial news data, to fine-tune BERT models for binary sentiment classification (positive/negative).

## Dependencies - Before you get started

Please run the code by installing the requirements by running

```
pip install -r requirements.txt
```

## Project structure

This repo contains 6 notebooks that you can run the replicate the full data pipeline process, with two parts as seen below. If you want to replicate the complete workflow, you need run all 6 notebooks in order from 1 to 6.

### a. Data Labelling workflow (notebook 1 to 3):
- 1.EDA_All_data.ipynb: aggregates all disparate json files containing news articles from Webz.io dataset together, and select the relevant sources for analysis
- 2.OpenAI_API_Prompt_Engineering_Test.ipynb: tests prompts for labelling unlabelled news data
- 3.OpenAI_Automatic_Data_labelling.ipynb: runs batch jobs to label unlabelled news data

The folders news_data_all (stores raw webz.io files) -> processed_data (takes combined news files from notebook 1's output files) -> labelled_data (stores notebook 3's labelled news data from OpenAI in batches) -> test (includes human annotated data comparing 200 samples labelled by GPT-4 with human annotations)

N.B. in this repo only the output from notebook 3's openAI data labelling is stored in the respective folder (`labelled_data`), if you want to replicate the complete the data workflow from scratch, follow the instructions in "Running everything from the Data Labelling Workflow" section.

### b. Data Analysis Workflow (notebook 4 to 6)
- 4.Unsupervised_Analysis_topic_modelling.ipynb: Performs Latent Semanatic Analysis (LSA) and Latent Dirichlet Allocation (LDA) to assess the information content of our news articles
- 5_Supervised_Analysis_BERT_Training.ipynb: Performing fine-tuning of the base BERT model using Logistic Regression (with TF-IDF representation) as a benchmark, and comparing performing using validation and test sets
- 6_Supervised_Analysis_FinBERT_Training.ipynb: Performing fine-tuning of the FinBERT model using Logistic Regression (with TF-IDF representation) as a benchmark. Here, we compare the performance of the Logistic Regression, fine tuned base BERT model and fine tuned FinBERT models together to evaluate their relative performance on the validation and test sets.

Please note that the folder `combined_data_output` **contains the training, validation, and test sets** of financial news articles that is used for data analysis, the key part of this analysis report.

Please note if you want to just run the data analysis workflow and skip the need to the data labelling workflow, I've uploaded the data in the appropriate folders to allow you to do so.

**You can in fact start running the code from notebook 4 to 6 to start the data analysis using unsupervised methods, and fine-tuning BERT using the labelled dataset from BERT, using the train, validation and test sets in the `combined_data_output` folder**

#### Running everything from the Data Labelling Workflow

To start the data pipeline, please first take download the complete free financial news data from the news aggregator Webz.io [data description](https://staging.webz.io/free-datasets/financial-news-articles/), [data link](https://staging.webz.io/free-datasets-thank-you/?Required_Dataset=financial-news-articles). Please click on the data link to download zip file of news. Here there will be 3 folders containing news for each  month between July and October 2015. Unzip the all such that you have jsons of news article for each folder (3 folders in total). Copy these folders into the `news_data_all` folder.

You will also need the openAI API key. Setup your own OpenAI API key using the [OpenAI API documentation](https://platform.openai.com/docs/overview) using your own OpenAI account and top up your API account with Credit appropriately. You will need to spend roughly $22 to label the unlabelled data.

Once you have have the API key, please save the API in the `.env` folder replacing the `ADD_OWN_OPENAI_KEY` in `OPENAI_API_KEY=ADD_OWN_OPENAI_KEY` line of the `.env` file.

**I declare that the below is of my own work, and I have worked on this assignment independently. Please see the cell below for package dependencies, uncomment to install the package dependencies**

Please note that the size of the data folders combined (news_data_all, processed_data, test, labelled_data, combined_data_output) is less than 100mb, and the dataset I use for the analysis (data analysis workflow above) in the combined_data_output folder is therefore much less than 100mb. Therefore my dataset for analysis fits the 100mb limit as required. 
