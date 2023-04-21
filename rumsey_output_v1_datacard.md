
# Dataset Card 

## Dataset Description

This dataset contains text on maps recognized from a georeferenced subset of ~57k historical maps from the David Rumsey Map Collection.

- Browse the collection: https://www.davidrumsey.com/ 
- Repository: https://purl.stanford.edu/vn901vj0926
- Point of contact: For information about how this data was created, please contact https://yaoyichi.github.io/. For information about the corpus of physical maps, please contact https://library.stanford.edu/rumsey. For questions about using this data for humanities research, please contact Katie McDonough (k.mcdonough [at] lancaster.ac.uk).

### Dataset Summary

### Dataset Languages

The data here has been collected from maps covering the entire world and printed in many countries over several centuries. Principal languages will include English, French, Spanish, Portuguese, Italian, Dutch, Greek, Russian, Arabic, Chinese, Japanese, Vietnamese, and braille. More information about the physical collection of maps that this data is derived from can be found [here]([url](https://www.davidrumsey.com/about/about)). BCP-47 codes for the languages above are en, fr, es, pt, it, nl, el, ru, ar, zh, ja, and vi.


## Dataset Structure

## Data Instances

Each file contains instances of text as it is found on a single, physical map sheet or a composite of sheets that has been artificially constructed for series maps that fit together to form one digital map of a larger area.

Every text identified by mapKurator is saved as a json `Feature` that is a polygon with geospatial coordinates for its vertices and has the following properties: `text` (the mapKurator predicted transcription of the text within the polygon), `score` (the confidence score for the text detection), `postocr_label` (a prediction for a normalized version of `text` that is based on a post-processing step, details below), and `img_coordinates` (the pixel coordinates of the polygon).

An instance of the output therefore has the following structure:

```json
 {
            "type": "Feature",
            "geometry":
            {
                "type": "Polygon",
                "coordinates":
                [
                    [
                        [
                            -87.788223,
                            17.221021
                        ],
                        [
                            -87.353574,
                            17.096341
                        ],
                        [
                            -86.858518,
                            17.113311
                        ],
                        [
                            -86.405222,
                            17.074285
                        ],
                        [
                            -85.904419,
                            17.122105
                        ],
                        [
                            -85.359606,
                            17.100156
                        ],
                        [
                            -84.865925,
                            17.097613
                        ],
                        [
                            -84.424201,
                            17.009762
                        ],
                        [
                            -83.870715,
                            16.985785
                        ],
                        [
                            -83.729531,
                            17.238058
                        ],
                        [
                            -83.999044,
                            17.531543
                        ],
                        [
                            -84.684278,
                            17.549973
                        ],
                        [
                            -85.291577,
                            17.597953
                        ],
                        [
                            -85.971405,
                            17.604193
                        ],
                        [
                            -86.814296,
                            17.609046
                        ],
                        [
                            -87.672486,
                            17.613572
                        ],
                        [
                            -87.788223,
                            17.221021
                        ]
                    ]
                ]
            },
            "properties":
            {
                "text": "Greenwich",
                "score": 0.6183063984,
                "postocr_label": "GREENWICH",
                "img_coordinates":
                [
                    [
                        692,
                        420
                    ],
                    [
                        706,
                        425
                    ],
                    [
                        722,
                        424
                    ],
                    [
                        737,
                        425
                    ],
                    [
                        754,
                        423
                    ],
                    [
                        772,
                        424
                    ],
                    [
                        788,
                        424
                    ],
                    [
                        803,
                        427
                    ],
                    [
                        821,
                        428
                    ],
                    [
                        826,
                        419
                    ],
                    [
                        817,
                        408
                    ],
                    [
                        794,
                        407
                    ],
                    [
                        774,
                        406
                    ],
                    [
                        751,
                        406
                    ],
                    [
                        723,
                        406
                    ],
                    [
                        695,
                        406
                    ],
                    [
                        692,
                        420
                    ]
                ]
            }
        },
```

### Data Fields


**File name**: drawn from an ID of original map images (provided by David Rumsey Map Collection). This ID corresponds to the `Image No` field in the davidrumsey.com metadata.

<img src="https://user-images.githubusercontent.com/5383572/188785367-446690fd-76fc-47db-b2ae-a1fac4fc61d6.png" width="700">

- `Feature`: an instance of detected text which has a polygon geometry
  - `Polygon` `coordinates`: contains the geospatial coordinates for each vertex of the polygon
  - `Properties`
    - `text`: raw mapKurator-recognized text within polygon 
    - `score`: confidence score for text detection
    - `postocr_label`: output from PostOCR module which updates `text` content (always CAPITALIZED). 
    - `img_coordinates`: pixel cordinates of the bounding polygon

<img src="https://user-images.githubusercontent.com/5383572/188784909-10cd04fd-4b61-4205-a563-33d20f9026db.png" width="700">

## Dataset Creation

### Curation Rationale

This dataset was created for the collaborative project between Machines Reading Maps and the David Rumsey Map Collection in order to enable searching maps in the collection based on their text content, not only based on traditional library metadata (e.g. title, author). It contains data derived from maps that were published in many different parts of the world, in many languages, at many scales, and with different intents. 

The main criterion for inclusion in the dataset was whether a scanned map had been georeferenced. Working with georeferenced maps allows us to translate the pixel coordinates of a text's bounding polygon into geospatial coordinates, thereby "locating" the text automatically.

### Initial Data Collection

#### Accessing map images

ADD

#### Accessing metadata

ADD

### Processing the data

Data was created using [mapKurator](https://github.com/machines-reading-maps/mapkurator-system#model-details) and the [TESTR](https://github.com/mlpc-ucsd/TESTR) model. mapKurator is a fully automatic pipeline to process of large number of scanned historical maps. 

This version of the dataset used the following modules in mapKurator.

1. `ImageCroping` - divides very large map images (>10K pixels) into image patches (1K pixels) to make processing more efficient.
2. `PatchTextSpotter` - uses state-of-the-art network architecture TESTR to detect and recognize text labels on image patches. 
3. `PatchtoMapMerging` - merges patch-level spotting results to re-construct the map-level image.
4. `GeocoordinateConverter` - converts the text label bounding polygons from an image coordinate system to a geocoordiate system. (Both are preserved in output.)
5. `PostOCR` - this module experimentally suggests an alternative based on the content of features named in OpenStreetMap, given that we know there will be errors in the predicted `text` field. The PostOCR module compares the `text` content to a dictionary of all names of features in OpenStreetMap (in this version of the data, this is *only for the United States*) using the [fuzzy query function in elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-fuzzy-query.html) in order to select candidates for an improved result. The top candidate is selected based on word popularity in the dictionary. 


#### Training data
Due to the lack of annotated samples for training, we created a set of synthetic maps to mimic the text styles (e.g., font, spacing, orientation) from a selection of real historical maps. We place names of OpenStreetMap features on a map by considering the shape of the location geometry. We then merge the text with background styles extracted from David Rumsey collection maps. We train the model with these unlimited synthetic maps and apply the model to the historical maps.

#### Source Language Producer
The `text` content was produced by the mapKurator pipeline implementing the [TESTR](https://github.com/mlpc-ucsd/TESTR) model.

## Considerations for Using the Data

### Social Imapct of Dataset

ADD

### Discussion of Biases

#### Detection: False Positives

#### Detection: False Negatives

#### Recognition: Bounding Boxes

#### Recognition: Transcription

- The PostOCR module is biased to return results relevant only to places in the the United States. It should not be seen as likely to be a 'correction' to the original `text` field except in very specific cases of maps whose geographic coverage is limited to the US and which were printed in English. It's also less likely to be as useful for US maps printed before the twentieth century.
- ADD


#### Entity Linking: False Positives
(for V3 of dataset only)



### Other Known Limitations

- Issues related to using the synthetic data as training data?

## Additional Information

Metadata for this data (e.g. information about the maps that the geojson files describe) is available at https://purl.stanford.edu/ss311gz1992.

### Dataset Curators

This dataset was processed by @zekun-li, @Jina-Kim, @MinNamgung, and @linyijun with supervision from Yao-Yi Chiang, Knowledge Computing Lab, University of Minnesota. Data was provided by the David Rumsey Map Collection and Old Maps Online/Klokan Technologies, including contributions from David Rumsey, Drake Zabriskie, David Wong, and Petr Pridal. Project conceptualization and review included many members of the Machines Reading Maps team: Katherine McDonough, Deborah Holmes-Wong, Rainer Simon, and Valeria Vitale.

### Licensing Information

ADD

### Citation Information

ADD

