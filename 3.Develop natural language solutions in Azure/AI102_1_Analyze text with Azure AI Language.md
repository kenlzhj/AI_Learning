[Analyze text with Azure AI Language](https://learn.microsoft.com/en-us/training/modules/analyze-text-ai-language/)

# Detect language

```json
{
    "kind": "LanguageDetection",
    "parameters": {
        "modelVersion": "latest"
    },
    "analysisInput":{
        "documents":[
              {
                "id": "1",
                "text": "Hello world",
                "countryHint": "US"
              },
              {
                "id": "2",
                "text": "Bonjour tout le monde"
              }
        ]
    }
}
```

```json
{   "kind": "LanguageDetectionResults",
    "results": {
        "documents": [
          {
            "detectedLanguage": {
              "confidenceScore": 1,
              "iso6391Name": "en",
              "name": "English"
            },
            "id": "1",
            "warnings": []
          },
          {
            "detectedLanguage": {
              "confidenceScore": 1,
              "iso6391Name": "fr",
              "name": "French"
            },
            "id": "2",
            "warnings": []
          }
        ],
        "errors": [],
        "modelVersion": "2022-10-01"
    }
}
```

# Extract key phrases

```json
{
    "kind": "KeyPhraseExtraction",
    "parameters": {
        "modelVersion": "latest"
    },
    "analysisInput":{
        "documents":[
            {
              "id": "1",
              "language": "en",
              "text": "You must be the change you wish to see in the world."
            },
            {
              "id": "2",
              "language": "en",
              "text": "The journey of a thousand miles begins with a single step."
            }
        ]
    }
}
```

The response contains a list of key phrases detected in each document:

```json
{
    "kind": "KeyPhraseExtractionResults",
    "results": {
    "documents": [   
        {
         "id": "1",
         "keyPhrases": [
           "change",
           "world"
         ],
         "warnings": []
       },
       {
         "id": "2",
         "keyPhrases": [
           "miles",
           "single step",
           "journey"
         ],
         "warnings": []
       }
],
    "errors": [],
    "modelVersion": "2021-06-01"
    }
}
```

# Analyze sentiment

For example, you could submit a single document for sentiment analysis like this:

```json
{
  "kind": "SentimentAnalysis",
  "parameters": {
    "modelVersion": "latest"
  },
  "analysisInput": {
    "documents": [
      {
        "id": "1",
        "language": "en",
        "text": "Good morning!"
      }
    ]
  }
}
```

```json
{
  "kind": "SentimentAnalysisResults",
  "results": {
    "documents": [
      {
        "id": "1",
        "sentiment": "positive",
        "confidenceScores": {
          "positive": 0.89,
          "neutral": 0.1,
          "negative": 0.01
        },
        "sentences": [
          {
            "sentiment": "positive",
            "confidenceScores": {
              "positive": 0.89,
              "neutral": 0.1,
              "negative": 0.01
            },
            "offset": 0,
            "length": 13,
            "text": "Good morning!"
          }
        ],
        "warnings": []
      }
    ],
    "errors": [],
    "modelVersion": "2022-11-01"
  }
}
```

# Extract entities

Input for entity recognition is similar to input for other Azure AI Language API functions:

```JSON
{
  "kind": "EntityRecognition",
  "parameters": {
    "modelVersion": "latest"
  },
  "analysisInput": {
    "documents": [
      {
        "id": "1",
        "language": "en",
        "text": "Joe went to London on Saturday"
      }
    ]
  }
}
```

The response includes a list of categorized entities found in each document:

```JSON
{
    "kind": "EntityRecognitionResults",
     "results": {
          "documents":[
              {
                  "entities":[
                  {
                    "text":"Joe",
                    "category":"Person",
                    "offset":0,
                    "length":3,
                    "confidenceScore":0.62
                  },
                  {
                    "text":"London",
                    "category":"Location",
                    "subcategory":"GPE",
                    "offset":12,
                    "length":6,
                    "confidenceScore":0.88
                  },
                  {
                    "text":"Saturday",
                    "category":"DateTime",
                    "subcategory":"Date",
                    "offset":22,
                    "length":8,
                    "confidenceScore":0.8
                  }
                ],
                "id":"1",
                "warnings":[]
              }
          ],
          "errors":[],
          "modelVersion":"2021-01-15"
    }
}
```

# Extract linked entities

In some cases, the same name might be applicable to more than one entity. For example, does an instance of the word "Venus" refer to the planet or the goddess from mythology?

Entity linking can be used to disambiguate entities of the same name by referencing an article in a knowledge base. Wikipedia provides the knowledge base for the Text Analytics service. Specific article links are determined based on entity context within the text.

For example, "I saw Venus shining in the sky" is associated with the link https://en.wikipedia.org/wiki/Venus; while "Venus, the goddess of beauty" is associated with https://en.wikipedia.org/wiki/Venus_(mythology).

As with all Azure AI Language service functions, you can submit one or more documents for analysis:



```JSON
{
  "kind": "EntityLinking",
  "parameters": {
    "modelVersion": "latest"
  },
  "analysisInput": {
    "documents": [
      {
        "id": "1",
        "language": "en",
        "text": "I saw Venus shining in the sky"
      }
    ]
  }
}
```

The response includes the entities identified in the text along with links to associated articles:



```JSON
{
  "kind": "EntityLinkingResults",
  "results": {
    "documents": [
      {
        "id": "1",
        "entities": [
          {
            "bingId": "89253af3-5b63-e620-9227-f839138139f6",
            "name": "Venus",
            "matches": [
              {
                "text": "Venus",
                "offset": 6,
                "length": 5,
                "confidenceScore": 0.01
              }
            ],
            "language": "en",
            "id": "Venus",
            "url": "https://en.wikipedia.org/wiki/Venus",
            "dataSource": "Wikipedia"
          }
        ],
        "warnings": []
      }
    ],
    "errors": [],
    "modelVersion": "2021-06-01"
  }
}
```



---

Exercise Code

```python
from dotenv import load_dotenv
import os

# Import namespaces
# import namespaces
from azure.core.credentials import AzureKeyCredential
from azure.ai.textanalytics import TextAnalyticsClient

def main():
    try:
        # Get Configuration Settings
        load_dotenv()
        ai_endpoint = os.getenv('AI_SERVICE_ENDPOINT')
        ai_key = os.getenv('AI_SERVICE_KEY')

        # Create client using endpoint and key
        credential = AzureKeyCredential(ai_key)
        ai_client = TextAnalyticsClient(endpoint=ai_endpoint, credential=credential)

        # Analyze each text file in the reviews folder
        reviews_folder = 'reviews'
        for file_name in os.listdir(reviews_folder):
            # Read the file contents
            print('\n-------------\n' + file_name)
            text = open(os.path.join(reviews_folder, file_name), encoding='utf8').read()
            print('\n' + text)

            # Get language
            detectedLanguage = ai_client.detect_language(documents=[text])[0]
            print('\nLanguage: {}'.format(detectedLanguage.primary_language.name))

            # Get sentiment
            sentimentAnalysis = ai_client.analyze_sentiment(documents=[text])[0]
            print("\nSentiment: {}".format(sentimentAnalysis.sentiment))

            # Get key phrases
            phrases = ai_client.extract_key_phrases(documents=[text])[0].key_phrases
            if len(phrases) > 0:
                print("\nKey Phrases:")
                for phrase in phrases:
                    print('\t{}'.format(phrase))

            # Get entities
            entities = ai_client.recognize_entities(documents=[text])[0].entities
            if len(entities) > 0:
                print("\nEntities")
                for entity in entities:
                    print('\t{} ({})'.format(entity.text, entity.category))

            # Get linked entities
            entities = ai_client.recognize_linked_entities(documents=[text])[0].entities
            if len(entities) > 0:
                print("\nLinks")
                for linked_entity in entities:
                    print('\t{} ({})'.format(linked_entity.name, linked_entity.url))

    except Exception as ex:
        print(ex)


if __name__ == "__main__":
    main()

```

 

