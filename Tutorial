# AWS Usage Tutorial

This tutorial guides researchers through accessing and analyzing the "An Annotated Dataset of Egyptian Fruit Bat Vocalizations Across Varying Contexts and During Vocal Ontogeny" using AWS services.​
It is advised to set up an AWS account and install AWS CLI, but you can choose if using cloud computing from AWS or other cloud services. 

## 1. Accessing and Playing Audio Files in Jupyter Notebook

### Step1 
Use boto3 to download a .wav file from the S3 bucket:​

Install `boto3` to connect with AWS S3. 
```
pip install boto3 librosa IPython
```

In the notebook:

```
import boto3

# Initialize the S3 client
s3 = boto3.client('s3')

# Define the S3 bucket and file key
bucket_name = 'egyptian-fruit-bat-vocalizations-open-data'
file_key = 'data/Folder_1/example.wav'  # Replace with the actual file path

# Download the file
s3.download_file(bucket_name, file_key, 'example.wav')
```

### Step2 - Load the audio file using librosa and play it in the notebook:

```
import librosa
from IPython.display import Audio

# Load the audio file
y, sr = librosa.load('example.wav', sr=None) 
# Sample rate if 250000

# Display the audio player
Audio(data=y, rate=sr) 
# Note: Ensure that the sampling rate (sr) is set to a value lower than 192,000 Hz, as higher rates are supported by web browsers for playback.​
```


## 2. Training a TensorFlow Model with Data from S3

### Step1 
Install Tensorflow:

```
pip install tensorflow
```

### Step2 - Read the WAV files in tensorflow

This approach reads the WAV file directly from S3 into memory without saving it locally.
If needed, configure TensorFlow to Read and Stream from S3 (using the `tf.data` API).

```
pip install smart_open boto3
```
In Jupyter:

```
import tensorflow as tf
from smart_open import open
import boto3
import io

# Initialize S3 client



s3 = boto3.client('s3')

# Function to read a WAV file from S3
def read_wav_from_s3(bucket_name, key):
    with open(f's3://{bucket_name}/{key}', 'rb') as s3_file:
        wav_data = s3_file.read()
    return wav_data

# Example usage - The dataset is organised as /data/Folder_[number]/*.wav
bucket_name = 'your-bucket-name' 
key = 'path/to/your-file.wav'
wav_data = read_wav_from_s3(bucket_name, key)

# Decode WAV data
audio, sample_rate = tf.audio.decode_wav(wav_data)
```




### Step3 - Example for Creating a Dataset Pipeline

#### Utility functions
```
import tensorflow as tf

def load_wav_from_s3(bucket_name, file_key):
    s3_uri = f's3://{bucket_name}/{file_key}'
    audio_binary = tf.io.read_file(s3_uri)
    audio, sample_rate = tf.audio.decode_wav(audio_binary)
    return audio, sample_rate

def preprocess_audio(audio, sample_rate):
    # Example: Convert to mono and normalize
    audio = tf.reduce_mean(audio, axis=1)
    audio = audio / tf.reduce_max(tf.abs(audio))
    return audio
```

#### 
Create a tf.data.Dataset to stream data from S3:​

```

# List of S3 file keys
file_keys = [f'data/Folder_1/{i}.wav' for i in range(1, 1001)]  # Example file keys

# Create a TensorFlow dataset
dataset = tf.data.Dataset.from_tensor_slices(file_keys)

# Map the loading and preprocessing functions
dataset = dataset.map(lambda x: preprocess_audio(*load_wav_from_s3(bucket_name, x)))

# Batch and prefetch for performance
dataset = dataset.batch(32).prefetch(tf.data.AUTOTUNE)
```

### Step 4: Building and Training the Model

An example of using this dataset is for segmentation and clustering of bats' utterances.
Check out my master thesis for a comprehensive guide and repository:
https://urn.kb.se/resolve?urn=urn:nbn:se:su:diva-223664

You could use the dataset like this:
```
# Combine dataset with labels
train_dataset = tf.data.Dataset.zip((dataset, tf.data.Dataset.from_tensor_slices(labels)))
```

