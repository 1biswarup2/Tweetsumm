[Contact Us for accessing the TweetSum Dataset](mailto:benjams@il.ibm.com)

# TweetSumm

A dataset focused on summarization of dialogs, which represents the rich domain of Twitter customer care conversations 

Tweetsumm comprises of 1,100 dialogs reconstructed from Tweets that appear in the [Kaggle Customer Support On Twitter](www.kaggle.com/thoughtvector/customer-support-on-twitter) dataset each accompanied by 3 extractive and 3 abstractive summaries generated by human annotators.


If you use this dataset in your work, please cite our paper:

@inproceedings{,
    title = "....",
    
}

## TweetSumm format

TweetSumm is released with a partition in Train/Test/Valid files.
Each file is in [JSON Lines format](https://jsonlines.org/).

A TweetSum entry (line) has the following format:
- **conversation_id** : a unique identifier of the dialog
- **tweet_ids_sentence_offset** : a list of 
    -  **tweet_id** : corresponding to Twitter Id in [Kaggle Customer Support On Twitter](www.kaggle.com/thoughtvector/customer-support-on-twitter) dataset
    -  **sentence offsets** : the offsets of the sentences splitting we used.
- **annotations** : a list of summaries generated by the human annotators - each entry contains :
    - **extractive** : a list of sentences selected from the initial dialog. The sentences are in the format **tweet_id**, **sentence offsets**
    - **abstractive** : a list of one or two sentences.


## TweetSumm processing

The script `tweet_summ_processor` allows to transform the TweetSumm entries to readable strings for further processing.

The `TweetSumProcessor` class requires one parameter : the path to the `twcs file` of [Kaggle Customer Support On Twitter](www.kaggle.com/thoughtvector/customer-support-on-twitter). This file can be download [here](https://www.kaggle.com/thoughtvector/customer-support-on-twitter/download).

The `TweetSumProcessor` has one method : `get_dialog_with_summaries` which gets a list of TweetSumm entries (lines in the TweetSumm files) and returns a list of corresponding `DialogWithSummaries` objects. These objects allow to access to the readable conversation associated with their readable human generated summaries.

**Code sample:**
```
    processor = TweetSumProcessor(TWCS_FILE_PATH)
    with open(TWEET_SUMM_FILE_PATH) as f:
        dialog_with_summaries = processor.get_dialog_with_summaries(f.readlines())
        for dialog_with_summary in dialog_with_summaries:
            json_format = dialog_with_summary.get_json()
            string_format = str(dialog_with_summary)
            ...
```   

## TweetSumm entry sample

```
{
  "conversation_id": "bbde6d8ec7c39c4551da1ff6024f997b",
  "tweet_ids_sentence_offset": [
    {
      "tweet_id": 2263653,
      "sentence_offsets": [
        "[0, 80]",
        "[82, 95]"
      ]
    },
    {
      "tweet_id": 2263651,
      "sentence_offsets": [
        "[0, 43]",
        "[44, 68]",
        "[69, 134]"
      ]
    },
    {
      "tweet_id": 2263652,
      "sentence_offsets": [
        "[0, 57]"
      ]
    },
    {
      "tweet_id": 2263654,
      "sentence_offsets": [
        "[0, 14]",
        "[15, 114]"
      ]
    },
    {
      "tweet_id": 2263655,
      "sentence_offsets": [
        "[0, 24]",
        "[25, 76]"
      ]
    },
    {
      "tweet_id": 2263656,
      "sentence_offsets": [
        "[0, 42]",
        "[43, 132]"
      ]
    },
    {
      "tweet_id": 2263657,
      "sentence_offsets": [
        "[0, 67]",
        "[68, 118]",
        "[119, 163]",
        "[164, 177]"
      ]
    },
    {
      "tweet_id": 2263658,
      "sentence_offsets": [
        "[0, 16]",
        "[17, 45]",
        "[46, 108]",
        "[109, 110]"
      ]
    }
  ],
  "annotations": [
    {
      "extractive": [
        {
          "tweet_id": 2263653,
          "sentence_offset": "[0, 80]"
        },
        {
          "tweet_id": 2263654,
          "sentence_offset": "[15, 114]"
        },
        {
          "tweet_id": 2263656,
          "sentence_offset": "[43, 132]"
        },
        {
          "tweet_id": 2263658,
          "sentence_offset": "[46, 108]"
        }
      ],
      "abstractive": [
        "Customer is complaining that the watchlist is not updated with new episodes from past two days.",
        "Agent informed that the team is working hard to investigate to show new episodes on page."
      ]
    },
    {
      "extractive": [
        {
          "tweet_id": 2263653,
          "sentence_offset": "[0, 80]"
        },
        {
          "tweet_id": 2263651,
          "sentence_offset": "[69, 134]"
        },
        {
          "tweet_id": 2263654,
          "sentence_offset": "[15, 114]"
        },
        {
          "tweet_id": 2263655,
          "sentence_offset": "[25, 76]"
        },
        {
          "tweet_id": 2263656,
          "sentence_offset": "[43, 132]"
        }
      ],
      "abstractive": [
        "Customer is complaining that my watch list is not updating with the new episodes.",
        "Agent updated to recommend checking the show page for these shows as the new eps will be there."
      ]
    },
    {
      "extractive": [
        {
          "tweet_id": 2263653,
          "sentence_offset": "[0, 80]"
        },
        {
          "tweet_id": 2263651,
          "sentence_offset": "[69, 134]"
        },
        {
          "tweet_id": 2263654,
          "sentence_offset": "[15, 114]"
        },
        {
          "tweet_id": 2263656,
          "sentence_offset": "[43, 132]"
        },
        {
          "tweet_id": 2263657,
          "sentence_offset": "[0, 67]"
        }
      ],
      "abstractive": [
        "Customer is complaining that he is not getting the updated watch list with new episodes for some shows.",
        "Agent assures that their team is working on it to resolve the issue and requests to navigate manually in the meantime."
      ]
    }
  ]
}
```

## License
Dataset released under the CDLA-Sharing license https://cdla.io/sharing-1-0/

## Disclaimer
IBM is not responsible for the content of the data, nor for any claim related to the data (including claims related to alleged intellectual property or privacy breach).
