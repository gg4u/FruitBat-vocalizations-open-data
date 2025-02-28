# Dataset Documentation

- Title: An Annotated Dataset of Egyptian Fruit Bat Vocalizations Across Varying Contexts and During Vocal Ontogeny​
- Authors: Yosef Prat, Mor Taub, Ester Pratt, Yossi Yovel​
- Publication Date: 2017​
- DOI: https://doi.org/10.6084/m9.figshare.c.3666502.v2​

## Overview

This dataset comprises a comprehensive collection of vocalizations from Egyptian fruit bats (Rousettus aegyptiacus), recorded continuously over more than a year in a controlled laboratory environment. 
The data encompasses various social interactions and developmental stages, providing valuable insights into bat communication and vocal development.​
I applied for the open data program at AWS to help researchers and practicionairs in bioacoustics and AI applied to animal communication and environmental conservation, 
given that large datasets poses budget limitations for data storage and training of neural networks.
The original authors are accredited above.
This repository provides a guideline to make best of use of consuming the dataset hosted on cloud AWS services.

## Dataset Structure

The dataset is organized into the following components:​

### Audio Recordings:

- Format: WAV files​
- Content: Raw audio recordings of bat vocalizations captured during different social interactions and developmental stages.​
- Metadata: Associated metadata files in CSV format containing information such as recording date, time, bat identities, context of interaction, and developmental stage.​


# Accessing the dataset
The dataset is hosted on AWS S3 and can be accessed via the following S3 bucket:

```
s3://egyptian-fruit-bat-vocalizations-open-data/
```

## Example Access Commands:

- List the contents of the bucket (using AWS CLI):

```
aws s3 ls s3://egyptian-fruit-bat-vocalizations-open-data/
```

- Download a specific file (using AWS CLI):​

```
aws s3 cp s3://egyptian-fruit-bat-vocalizations-open-data/audio/recording1.wav .
```

- Download a specific file (using Python / iPython in Jupyter notebooks):
```
import boto3

s3 = boto3.client('s3')
bucket_name = 'egyptian-fruit-bat-vocalizations-open-data'
object_key = 'audio/recording1.wav'
s3.download_file(bucket_name, object_key, 'local_filename.wav')
```

# License 
The original dataset is hosted in archive format FigShare (Springer) [1] and made available under the Creative Commons Attribution 4.0 International License (CC BY 4.0). 
Users are free to share and adapt the material, provided appropriate credit is given to the original authors [2].​

[1] Prat, Yosef; Taub, Mor; Pratt, Ester; Yovel, Yossi (2017). An annotated dataset of Egyptian fruit bat vocalizations across varying contexts and during vocal ontogeny. figshare. Collection. https://doi.org/10.6084/m9.figshare.c.3666502.v2​

[2] Prat, Y., Taub, M., Pratt, E. et al. An annotated dataset of Egyptian fruit bat vocalizations across varying contexts and during vocal ontogeny. Sci Data 4, 170143 (2017). https://doi.org/10.1038/sdata.2017.143​
