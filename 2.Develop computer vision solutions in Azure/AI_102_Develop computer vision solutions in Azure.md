# 1:Submitting an image for analysis

```python
from azure.ai.vision.imageanalysis import ImageAnalysisClient
from azure.ai.vision.imageanalysis.models import VisualFeatures
from azure.core.credentials import AzureKeyCredential

client = ImageAnalysisClient(
    endpoint="<YOUR_RESOURCE_ENDPOINT>",
    credential=AzureKeyCredential("<YOUR_AUTHORIZATION_KEY>")
)

result = client.analyze(
    image_data=<IMAGE_DATA_BYTES>, # Binary data from your image file
    visual_features=[VisualFeatures.CAPTION, VisualFeatures.TAGS],
    gender_neutral_caption=True,
)
```

---



Available visual features are contained in the `VisualFeatures` enumeration:

- VisualFeatures.TAGS: Identifies tags about the image, including objects, scenery, setting, and actions
- VisualFeatures.OBJECTS: Returns the bounding box for each detected object
- VisualFeatures.CAPTION: Generates a caption of the image in natural language
- VisualFeatures.DENSE_CAPTIONS: Generates more detailed captions for the objects detected
- VisualFeatures.PEOPLE: Returns the bounding box for detected people
- VisualFeatures.SMART_CROPS: Returns the bounding box of the specified aspect ratio for the area of interest
- VisualFeatures.READ: Extracts readable text



## Processing the response

This method returns a JSON document containing the requested information. The JSON response for image analysis looks similar to this example, depending on your requested features:

JSONCopy

```JSON
{
  "apim-request-id": "abcde-1234-5678-9012-f1g2h3i4j5k6",
  "modelVersion": "<version>",
  "denseCaptionsResult": {
    "values": [
      {
        "text": "a house in the woods",
        "confidence": 0.7055229544639587,
        "boundingBox": {
          "x": 0,
          "y": 0,
          "w": 640,
          "h": 640
        }
      },
      {
        "text": "a trailer with a door and windows",
        "confidence": 0.6675070524215698,
        "boundingBox": {
          "x": 214,
          "y": 434,
          "w": 154,
          "h": 108
        }
      }
    ]
  },
  "metadata": {
    "width": 640,
    "height": 640
  }
}
```



# 2:Read text with Azure AI Vision Image Analysis

```python
from azure.ai.vision.imageanalysis import ImageAnalysisClient
from azure.ai.vision.imageanalysis.models import VisualFeatures
from azure.core.credentials import AzureKeyCredential

client = ImageAnalysisClient(
    endpoint="<YOUR_RESOURCE_ENDPOINT>",
    credential=AzureKeyCredential("<YOUR_AUTHORIZATION_KEY>")
)

result = client.analyze(
    image_data=<IMAGE_DATA_BYTES>, # Binary data from your image file
    visual_features=[VisualFeatures.READ],
    language="en",
)
```

result:

```JSON
{
    "metadata":
    {
        "width": 500,
        "height": 430
    },
    "readResult":
    {
        "blocks":
        [
            {
                "lines":
                [
                    {
                        "text": "Hello World!",
                        "boundingPolygon":
                        [
                            {"x":251,"y":265},
                            {"x":673,"y":260},
                            {"x":674,"y":308},
                            {"x":252,"y":318}
                        ],
                        "words":
                        [
                            {
                                "text":"Hello",
                                "boundingPolygon":
                                [
                                    {"x":252,"y":267},
                                    {"x":307,"y":265},
                                    {"x":307,"y":318},
                                    {"x":253,"y":318}
                                ],
                            "confidence":0.996
                            },
                            {
                                "text":"World!",
                                "boundingPolygon":
                                [
                                    {"x":318,"y":264},
                                    {"x":386,"y":263},
                                    {"x":387,"y":316},
                                    {"x":319,"y":318}
                                ],
                                "confidence":0.99
                            }
                        ]
                    },
                ]
            }
        ]
    }
}
```



# 3: Exercise Code - Text Analysis

```Python
from dotenv import load_dotenv
import os
import time
import sys
from PIL import Image, ImageDraw
from matplotlib import pyplot as plt

# import namespaces
from azure.ai.vision.imageanalysis import ImageAnalysisClient
from azure.ai.vision.imageanalysis.models import VisualFeatures
from azure.core.credentials import AzureKeyCredential


def main():

    # Clear the console
    os.system('cls' if os.name=='nt' else 'clear')

    try:
        # Get Configuration Settings
        load_dotenv()
        ai_endpoint = os.getenv('AI_SERVICE_ENDPOINT')
        ai_key = os.getenv('AI_SERVICE_KEY')

        # Get image
        image_file = 'images/Lincoln.jpg'
        if len(sys.argv) > 1:
            image_file = sys.argv[1]


       # Authenticate Azure AI Vision client
        cv_client = ImageAnalysisClient(
            endpoint=ai_endpoint,
            credential=AzureKeyCredential(ai_key))

        
        # Read text in image
        with open(image_file,"rb") as f:
            image_data = f.read()
        print(f"\nReading text in {image_file}")

        result = cv_client.analyze(
            image_data = image_data,
            visual_features = [VisualFeatures.Read]

        )

        # Print the text
        if result.read is not None:
            print("\nText:")
    
            for line in result.read.blocks[0].lines:
                print(f" {line.text}")        
        # Annotate the text in the image
        annotate_lines(image_file, result.read)
        
        # Find individual words in each line
        print ("\nIndividual words:")
        for line in result.read.blocks[0].lines:
            for word in line.words:
                print(f"  {word.text} (Confidence: {word.confidence:.2f}%)")
        # Annotate the words in the image
        annotate_words(image_file, result.read)


    except Exception as ex:
        print(ex)

def annotate_lines(image_file, detected_text):
    print(f'\nAnnotating lines of text in image...')

     # Prepare image for drawing
    image = Image.open(image_file)
    fig = plt.figure(figsize=(image.width/100, image.height/100))
    plt.axis('off')
    draw = ImageDraw.Draw(image)
    color = 'cyan'

    for line in detected_text.blocks[0].lines:
        # Draw line bounding polygon
        r = line.bounding_polygon
        rectangle = ((r[0].x, r[0].y),(r[1].x, r[1].y),(r[2].x, r[2].y),(r[3].x, r[3].y))
        draw.polygon(rectangle, outline=color, width=3)

    # Save image
    plt.imshow(image)
    plt.tight_layout(pad=0)
    textfile = 'lines.jpg'
    fig.savefig(textfile)
    print('  Results saved in', textfile)
    
def annotate_words(image_file, detected_text):
    print(f'\nAnnotating individual words in image...')

     # Prepare image for drawing
    image = Image.open(image_file)
    fig = plt.figure(figsize=(image.width/100, image.height/100))
    plt.axis('off')
    draw = ImageDraw.Draw(image)
    color = 'cyan'

    for line in detected_text.blocks[0].lines:
        for word in line.words:
            # Draw word bounding polygon
            r = word.bounding_polygon
            rectangle = ((r[0].x, r[0].y),(r[1].x, r[1].y),(r[2].x, r[2].y),(r[3].x, r[3].y))
            draw.polygon(rectangle, outline=color, width=3)

    # Save image
    plt.imshow(image)
    plt.tight_layout(pad=0)
    textfile = 'words.jpg'
    fig.savefig(textfile)
    print('  Results saved in', textfile)



if __name__ == "__main__":
    main()

```





# 4:Detect and analyze faces

```python
from azure.ai.vision.face import FaceClient
from azure.ai.vision.face.models import *
from azure.core.credentials import AzureKeyCredential

face_client = FaceClient(
    endpoint="<YOUR_RESOURCE_ENDPOINT>",
    credential=AzureKeyCredential("<YOUR_RESOURCE_KEY>"))

# Specify facial features to be retrieved
features = [FaceAttributeTypeDetection01.HEAD_POSE,
            FaceAttributeTypeDetection01.OCCLUSION,
            FaceAttributeTypeDetection01.ACCESSORIES]

# Use client to detect faces in an image
with open("<IMAGE_FILE_PATH>", mode="rb") as image_data:
    detected_faces = face_client.detect(
        image_content=image_data.read(),
        detection_model=FaceDetectionModel.DETECTION01,
        recognition_model=FaceRecognitionModel.RECOGNITION01,
        return_face_id=True,
        return_face_attributes=features,
    )
```

A response for an image containing a single face might look similar to the following example:

```json
[
    {
        'faceRectangle': {'top': 174, 'left': 247, 'width': 246, 'height': 246}
        'faceAttributes':
        {
            'headPose':{'pitch': 3.7, 'roll': -7.7, 'yaw': -20.9},
            'accessories':
                [
                    {'type': 'glasses', 'confidence': 1.0}
                ],
            'occlusion':{'foreheadOccluded': False, 'eyeOccluded': False, 'mouthOccluded': False}
        }
    }
]
```



# 5:Exercise Code - Detect and analyze faces

```python
from dotenv import load_dotenv
import os
import sys
from PIL import Image, ImageDraw
from matplotlib import pyplot as plt

# Import namespaces
# Import namespaces
from azure.ai.vision.face import FaceClient
from azure.ai.vision.face.models import FaceDetectionModel, FaceRecognitionModel, FaceAttributeTypeDetection01
from azure.core.credentials import AzureKeyCredential

def main():

    # Clear the console
    os.system('cls' if os.name=='nt' else 'clear')

    try:
        # Get Configuration Settings
        load_dotenv()
        cog_endpoint = os.getenv('AI_SERVICE_ENDPOINT')
        cog_key = os.getenv('AI_SERVICE_KEY')

        # Get image
        image_file = 'images/face1.jpg'
        if len(sys.argv) > 1:
            image_file = sys.argv[1]


        # Authenticate Face client
        # Authenticate Face client
        face_client = FaceClient(
            endpoint=cog_endpoint,
            credential=AzureKeyCredential(cog_key))


        # Specify facial features to be retrieved
        # Specify facial features to be retrieved
        features = [FaceAttributeTypeDetection01.HEAD_POSE,
                    FaceAttributeTypeDetection01.OCCLUSION,
                    FaceAttributeTypeDetection01.ACCESSORIES]

        # Get faces
        with open(image_file, mode="rb") as image_data:
            detected_faces = face_client.detect(
                image_content=image_data.read(),
                detection_model=FaceDetectionModel.DETECTION01,
                recognition_model=FaceRecognitionModel.RECOGNITION01,
                return_face_id=False,
                return_face_attributes=features,
            )

        face_count = 0
        if len(detected_faces) > 0:
            print(len(detected_faces), 'faces detected.')
            for face in detected_faces:
            
                # Get face properties
                face_count += 1
                print('\nFace number {}'.format(face_count))
                print(' - Head Pose (Yaw): {}'.format(face.face_attributes.head_pose.yaw))
                print(' - Head Pose (Pitch): {}'.format(face.face_attributes.head_pose.pitch))
                print(' - Head Pose (Roll): {}'.format(face.face_attributes.head_pose.roll))
                print(' - Forehead occluded?: {}'.format(face.face_attributes.occlusion["foreheadOccluded"]))
                print(' - Eye occluded?: {}'.format(face.face_attributes.occlusion["eyeOccluded"]))
                print(' - Mouth occluded?: {}'.format(face.face_attributes.occlusion["mouthOccluded"]))
                print(' - Accessories:')
                for accessory in face.face_attributes.accessories:
                    print('   - {}'.format(accessory.type))
                # Annotate faces in the image
                annotate_faces(image_file, detected_faces)
 
 

    except Exception as ex:
        print(ex)

def annotate_faces(image_file, detected_faces):
    print('\nAnnotating faces in image...')

    # Prepare image for drawing
    fig = plt.figure(figsize=(8, 6))
    plt.axis('off')
    image = Image.open(image_file)
    draw = ImageDraw.Draw(image)
    color = 'lightgreen'

    # Annotate each face in the image
    face_count = 0
    for face in detected_faces:
        face_count += 1
        r = face.face_rectangle
        bounding_box = ((r.left, r.top), (r.left + r.width, r.top + r.height))
        draw = ImageDraw.Draw(image)
        draw.rectangle(bounding_box, outline=color, width=5)
        annotation = 'Face number {}'.format(face_count)
        plt.annotate(annotation,(r.left, r.top), backgroundcolor=color)
    
    # Save annotated image
    plt.imshow(image)
    outputfile = 'detected_faces.jpg'
    fig.savefig(outputfile)
    print(f'  Results saved in {outputfile}\n')


if __name__ == "__main__":
    main()
```



6:image classification

```python
from msrest.authentication import ApiKeyCredentials
from azure.cognitiveservices.vision.customvision.prediction import CustomVisionPredictionClient


 # Authenticate a client for the prediction API
credentials = ApiKeyCredentials(in_headers={"Prediction-key": "<YOUR_PREDICTION_RESOURCE_KEY>"})
prediction_client = CustomVisionPredictionClient(endpoint="<YOUR_PREDICTION_RESOURCE_ENDPOINT>",
                                                 credentials=credentials)

# Get classification predictions for an image
image_data = open("<PATH_TO_IMAGE_FILE>"), "rb").read()
results = prediction_client.classify_image("<YOUR_PROJECT_ID>",
                                           "<YOUR_PUBLISHED_MODEL_NAME>",
                                           image_data)

# Process predictions
for prediction in results.predictions:
    if prediction.probability > 0.5:
        print(image, ': {} ({:.0%})'.format(prediction.tag_name, prediction.probability))
```



# 6: Exercise Code - CustomVision - Train-classifier.py

```python
from azure.cognitiveservices.vision.customvision.training import CustomVisionTrainingClient
from azure.cognitiveservices.vision.customvision.training.models import ImageFileCreateBatch, ImageFileCreateEntry, Region
from msrest.authentication import ApiKeyCredentials
import time
import os

def main():
    from dotenv import load_dotenv
    global training_client
    global custom_vision_project

    # Clear the console
    os.system('cls' if os.name=='nt' else 'clear')

    try:
        # Get Configuration Settings
        load_dotenv()
        training_endpoint = os.getenv('TrainingEndpoint')
        training_key = os.getenv('TrainingKey')
        project_id = os.getenv('ProjectID')

        # Authenticate a client for the training API
        credentials = ApiKeyCredentials(in_headers={"Training-key": training_key})
        training_client = CustomVisionTrainingClient(training_endpoint, credentials)

        # Get the Custom Vision project
        custom_vision_project = training_client.get_project(project_id)

        # Upload and tag images
        Upload_Images('more-training-images')

        # Train the model
        Train_Model()
        
    except Exception as ex:
        print(ex)

def Upload_Images(folder):
    print("Uploading images...")
    tags = training_client.get_tags(custom_vision_project.id)
    for tag in tags:
        print(tag.name)
        for image in os.listdir(os.path.join(folder,tag.name)):
            image_data = open(os.path.join(folder,tag.name,image), "rb").read()
            training_client.create_images_from_data(custom_vision_project.id, image_data, [tag.id])

def Train_Model():
    print("Training ...")
    iteration = training_client.train_project(custom_vision_project.id)
    while (iteration.status != "Completed"):
        iteration = training_client.get_iteration(custom_vision_project.id, iteration.id)
        print (iteration.status, '...')
        time.sleep(5)
    print ("Model trained!")


if __name__ == "__main__":
    main()
```

# 7: Exercise Code - CustomVision - Test-classifier.py

```PYTHON
from azure.cognitiveservices.vision.customvision.prediction import CustomVisionPredictionClient
from msrest.authentication import ApiKeyCredentials
import os

def main():
    from dotenv import load_dotenv

    # Clear the console
    os.system('cls' if os.name=='nt' else 'clear')

    try:
        # Get Configuration Settings
        load_dotenv()
        prediction_endpoint = os.getenv('PredictionEndpoint')
        prediction_key = os.getenv('PredictionKey')
        project_id = os.getenv('ProjectID')
        model_name = os.getenv('ModelName')

        # Authenticate a client for the prediction API
        credentials = ApiKeyCredentials(in_headers={"Prediction-key": prediction_key})
        prediction_client = CustomVisionPredictionClient(endpoint=prediction_endpoint, credentials=credentials)

        # Classify test images
        for image in os.listdir('test-images'):
            image_data = open(os.path.join('test-images',image), "rb").read()
            results = prediction_client.classify_image(project_id, model_name, image_data)

            # Loop over each label prediction and print any with probability > 50%
            for prediction in results.predictions:
                if prediction.probability > 0.5:
                    print(image, ': {} ({:.0%})'.format(prediction.tag_name, prediction.probability))
    except Exception as ex:
        print(ex)

if __name__ == "__main__":
    main()

```



# 8:Develop an object detection client application

```python
from msrest.authentication import ApiKeyCredentials
from azure.cognitiveservices.vision.customvision.prediction import CustomVisionPredictionClient


 # Authenticate a client for the prediction API
credentials = ApiKeyCredentials(in_headers={"Prediction-key": "<YOUR_PREDICTION_RESOURCE_KEY>"})
prediction_client = CustomVisionPredictionClient(endpoint="<YOUR_PREDICTION_RESOURCE_ENDPOINT>",
                                                 credentials=credentials)

# Get classification predictions for an image
image_data = open("<PATH_TO_IMAGE_FILE>", "rb").read()
results = prediction_client.detect_image("<YOUR_PROJECT_ID>",
                                           "<YOUR_PUBLISHED_MODEL_NAME>",
                                           image_data)

# Process predictions
for prediction in results.predictions:
    if prediction.probability > 0.5:
        left = prediction.bounding_box.left
        top = prediction.bounding_box.top 
        height = prediction.bounding_box.height
        width =  prediction.bounding_box.width
        print(f"{prediction.tag_name} ({prediction.probability})")
        print(f"  Left:{left}, Top:{top}, Height:{height}, Width:{width}")
```

# 9:Detect objects in images

## 1=tagged-images.json

```json
{
    "files": [
        {
            "filename": "image11.jpg",
            "tags": [
                {
                    "tag": "orange",
                    "left": 0.501782656,
                    "top": 0.141307935,
                    "width": 0.30014348,
                    "height": 0.421263933
                },
                {
                    "tag": "banana",
                    "left": 0.117563143,
                    "top": 0.269699484,
                    "width": 0.4181828,
                    "height": 0.629577756
                }
            ]
        },
        {
            "filename": "image12.jpg",
            "tags": [
                {
                    "tag": "banana",
                    "left": 0.0266054422,
                    "top": 0.429971635,
                    "width": 0.9334502,
                    "height": 0.5663317
                },
                {
                    "tag": "apple",
                    "left": 0.594586432,
                    "top": 0.139771029,
                    "width": 0.2337932,
                    "height": 0.313067973
                },
                {
                    "tag": "orange",
                    "left": 0.24538058,
                    "top": 0.06600542,
                    "width": 0.230479121,
                    "height": 0.3283311
                }
            ]
        },
        {
            "filename": "image13.jpg",
            "tags": [
                {
                    "tag": "orange",
                    "left": 0.508894742,
                    "top": 0.155026585,
                    "width": 0.370887518,
                    "height": 0.512516
                },
                {
                    "tag": "banana",
                    "left": 0.08663659,
                    "top": 0.253976226,
                    "width": 0.382285058,
                    "height": 0.584964633
                }
            ]
        },
        {
            "filename": "image14.jpg",
            "tags": [
                {
                    "tag": "apple",
                    "left": 0.6080398,
                    "top": 0.222880378,
                    "width": 0.3454436,
                    "height": 0.498601437
                },
                {
                    "tag": "banana",
                    "left": 0.08858037,
                    "top": 0.2583913,
                    "width": 0.394662261,
                    "height": 0.6532483
                }
            ]
        },
        {
            "filename": "image15.jpg",
            "tags": [
                {
                    "tag": "orange",
                    "left": 0.124889567,
                    "top": 0.160744965,
                    "width": 0.365462124,
                    "height": 0.503556669
                },
                {
                    "tag": "banana",
                    "left": 0.530725956,
                    "top": 0.261967421,
                    "width": 0.380674481,
                    "height": 0.5697762
                }
            ]
        },
        {
            "filename": "image16.jpg",
            "tags": [
                {
                    "tag": "banana",
                    "left": 0.24473004,
                    "top": 0.316017568,
                    "width": 0.621397436,
                    "height": 0.62547636
                },
                {
                    "tag": "apple",
                    "left": 0.2669289,
                    "top": 0.1570937,
                    "width": 0.2849568,
                    "height": 0.373458445
                }
            ]
        },
        {
            "filename": "image17.jpg",
            "tags": [
                {
                    "tag": "banana",
                    "left": 0.137872428,
                    "top": 0.3037218,
                    "width": 0.6171047,
                    "height": 0.6428385
                },
                {
                    "tag": "apple",
                    "left": 0.446089834,
                    "top": 0.158026949,
                    "width": 0.2905319,
                    "height": 0.368484139
                }
            ]
        },
        {
            "filename": "image18.jpg",
            "tags": [
                {
                    "tag": "banana",
                    "left": 0.345145166,
                    "top": 0.315790027,
                    "width": 0.389697134,
                    "height": 0.5641991
                },
                {
                    "tag": "orange",
                    "left": 0.6284472,
                    "top": 0.160571277,
                    "width": 0.25890553,
                    "height": 0.321568727
                },
                {
                    "tag": "orange",
                    "left": 0.0472412556,
                    "top": 0.317386866,
                    "width": 0.344220281,
                    "height": 0.451182485
                }
            ]
        },
        {
            "filename": "image19.jpg",
            "tags": [
                {
                    "tag": "orange",
                    "left": 0.190300852,
                    "top": 0.04908291,
                    "width": 0.6819816,
                    "height": 0.89233005
                }
            ]
        },
        {
            "filename": "image20.jpg",
            "tags": [
                {
                    "tag": "orange",
                    "left": 0.296974,
                    "top": 0.11914885,
                    "width": 0.467207551,
                    "height": 0.6827575
                }
            ]
        },
        {
            "filename": "image21.jpg",
            "tags": [
                {
                    "tag": "orange",
                    "left": 0.235896885,
                    "top": 0.144391567,
                    "width": 0.5458362,
                    "height": 0.739897847
                }
            ]
        },
        {
            "filename": "image22.jpg",
            "tags": [
                {
                    "tag": "orange",
                    "left": 0.242359161,
                    "top": 0.039894,
                    "width": 0.632171631,
                    "height": 0.903954148
                }
            ]
        },
        {
            "filename": "image23.jpg",
            "tags": [
                {
                    "tag": "orange",
                    "left": 0.242662221,
                    "top": 0.06341483,
                    "width": 0.670523345,
                    "height": 0.7936373
                }
            ]
        },
        {
            "filename": "image24.jpg",
            "tags": [
                {
                    "tag": "banana",
                    "left": 0.06202866,
                    "top": 0.319153845,
                    "width": 0.9132734,
                    "height": 0.640570164
                }
            ]
        },
        {
            "filename": "image25.jpg",
            "tags": [
                {
                    "tag": "banana",
                    "left": 0.234958112,
                    "top": 0.165271968,
                    "width": 0.51941216,
                    "height": 0.77990067
                }
            ]
        },
        {
            "filename": "image26.jpg",
            "tags": [
                {
                    "tag": "banana",
                    "left": 0.123737864,
                    "top": 0.311502129,
                    "width": 0.6994619,
                    "height": 0.6375427
                }
            ]
        },
        {
            "filename": "image27.jpg",
            "tags": [
                {
                    "tag": "banana",
                    "left": 0.147404462,
                    "top": 0.332391232,
                    "width": 0.708104849,
                    "height": 0.41904977
                }
            ]
        },
        {
            "filename": "image28.jpg",
            "tags": [
                {
                    "tag": "banana",
                    "left": 0.294261217,
                    "top": 0.262935251,
                    "width": 0.476716518,
                    "height": 0.7041446
                }
            ]
        },
        {
            "filename": "image29.jpg",
            "tags": [
                {
                    "tag": "apple",
                    "left": 0.152405351,
                    "top": 0.105940014,
                    "width": 0.598258257,
                    "height": 0.8126528
                }
            ]
        },
        {
            "filename": "image30.jpg",
            "tags": [
                {
                    "tag": "apple",
                    "left": 0.255153179,
                    "top": 0.1485295,
                    "width": 0.528649,
                    "height": 0.7251674
                }
            ]
        },
        {
            "filename": "image31.jpg",
            "tags": [
                {
                    "tag": "apple",
                    "left": 0.227940559,
                    "top": 0.146328539,
                    "width": 0.561518431,
                    "height": 0.767682433
                }
            ]
        },
        {
            "filename": "image32.jpg",
            "tags": [
                {
                    "tag": "apple",
                    "left": 0.18220368,
                    "top": 0.0870502,
                    "width": 0.602320552,
                    "height": 0.7840438
                }
            ]
        },
        {
            "filename": "image33.jpg",
            "tags": [
                {
                    "tag": "apple",
                    "left": 0.2639115,
                    "top": 0.153765231,
                    "width": 0.55621016,
                    "height": 0.7570554
                }
            ]
        }
    ]
}
```







## 2=Add-tagged-images.py

```Python
from azure.cognitiveservices.vision.customvision.training import CustomVisionTrainingClient
from azure.cognitiveservices.vision.customvision.training.models import ImageFileCreateBatch, ImageFileCreateEntry, Region
from msrest.authentication import ApiKeyCredentials
import time
import json
import os

def main():
    from dotenv import load_dotenv
    global training_client
    global custom_vision_project

    # Clear the console
    os.system('cls' if os.name=='nt' else 'clear')

    try:
        # Get Configuration Settings
        load_dotenv()
        training_endpoint = os.getenv('TrainingEndpoint')
        training_key = os.getenv('TrainingKey')
        project_id = os.getenv('ProjectID')

        # Authenticate a client for the training API
        credentials = ApiKeyCredentials(in_headers={"Training-key": training_key})
        training_client = CustomVisionTrainingClient(training_endpoint, credentials)

        # Get the Custom Vision project
        custom_vision_project = training_client.get_project(project_id)

        # Upload and tag images
        Upload_Images('images')
    except Exception as ex:
        print(ex)



def Upload_Images(folder):
    print("Uploading images...")

    # Get the tags defined in the project
    tags = training_client.get_tags(custom_vision_project.id)

    # Create a list of images with tagged regions
    tagged_images_with_regions = []

    # Get the images and tagged regions from the JSON file
    with open('tagged-images.json', 'r') as json_file:
        tagged_images = json.load(json_file)
        for image in tagged_images['files']:
            # Get the filename
            file = image['filename']
            # Get the tagged regions
            regions = []
            for tag in image['tags']:
                tag_name = tag['tag']
                # Look up the tag ID for this tag name
                tag_id = next(t for t in tags if t.name == tag_name).id
                # Add a region for this tag using the coordinates and dimensions in the JSON
                regions.append(Region(tag_id=tag_id, left=tag['left'],top=tag['top'],width=tag['width'],height=tag['height']))
            # Add the image and its regions to the list
            with open(os.path.join(folder,file), mode="rb") as image_data:
                tagged_images_with_regions.append(ImageFileCreateEntry(name=file, contents=image_data.read(), regions=regions))

    # Upload the list of images as a batch
    upload_result = training_client.create_images_from_files(custom_vision_project.id, ImageFileCreateBatch(images=tagged_images_with_regions))
    # Check for failure
    if not upload_result.is_batch_successful:
        print("Image batch upload failed.")
        for image in upload_result.images:
            print("Image status: ", image.status)
    else:
        print("Images uploaded.")

if __name__ == "__main__":
    main()
```

