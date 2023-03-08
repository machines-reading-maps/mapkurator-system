
# Dataset Card 

## Dataset Description

Text on maps recognized from georeferenced subset of 57k historical maps David Rumsey Map Collection. 

Browse the collection: https://www.davidrumsey.com/ 
Repository: ADD ZENODO LINK to replace https://s3.msi.umn.edu/rumsey_output/geojson_testr_syn_54119.zip
Paper: Forthcoming
Point of contact: For information about how this data was created, please contact https://yaoyichi.github.io/. For information about the corpus of physical maps, please contact https://library.stanford.edu/rumsey. For questions about using this data for humanities research, please contact Katie McDonough (k.mcdonough [at] lancaster.ac.uk).

### Dataset Summary

### Dataset Languages

The data here has been collected from maps covering the entire world and printed in many countries over several centuries. Principal languages will include English, French, Spanish, Portuguese, Italian, Dutch, Greek, Russian, Arabic, Chinese, Japanese, Vietnamese, and braille. More information about the physical collection of maps that this data is derived from can be found [here]([url](https://www.davidrumsey.com/about/about)). BCP-47 codes for the languages above are en, fr, es, pt, it, nl, el, ru, ar, zh, ja, and vi.


## Dataset Structure

## Data Instances

Each file contains instances of text as it is found on a single, physical map sheet or a composite of sheets that has been artificially constructed for series maps that fit together to form one digital map of a larger area.

Within these files, an instance of the output has the following structure:

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

<img src="https://user-images.githubusercontent.com/5383572/188784909-10cd04fd-4b61-4205-a563-33d20f9026db.png" width="700">

File name: drawn from an ID of original map images (provided by David Rumsey Map Collection. This ID corres

<img src="https://user-images.githubusercontent.com/5383572/188785367-446690fd-76fc-47db-b2ae-a1fac4fc61d6.png" width="700">

