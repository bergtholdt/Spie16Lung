# Pulmonary Nodule Detection Using a Cascaded SVM Classifier

This repository contains the data used for producing the results in the SPIE16 paper "
used in the SPIE16 Paper" (9785-038).

There are two alternative version. In ``volumes_json`` you can find all Volumes as JavaScript Object Notation (JSON) encoded deep nested data structure including Cliques and Annotations. These contain a lot of fields not necessarily needed by 3rd parties. A subset of relevant fields and individual tables can be found in the ``*.csv`` files (comma separated values) or alternatively in the ``*.json`` files. There is one for table for each: Volumes, Cliques, Annotations and Contours. Note that some fields are encoded as lists of strings. If you load the csv-file in Excel, some rows containing long strings are not read correctly.

- ``volumes.csv / volumes.json``

| Field               | Description                                                       |
| -----               | -----                                                             |
| PatientID           | the unique LIDC/IDRI PatientID                                    |
| Dataset             | "Training", "Verify" or "Test" (Verify is also used for Training) |
| SeriesUID           | DICOM tag SeriesInstanceUID                                       |
| StudyUID            | DICOM tag StudyInstanceUID                                        |
| ImageType           | list of DICOM ImageType tags                                      |
| FrameOfReferenceUID | DICOM tag FrameOfReferenceUID                                     |
| XRayTubeCurrent     | DICOM tag XRayTubeCurrent                                         |
| KVP                 | DICOM tag KVP                                                     |
| ImageFileNames      | list of original dicom file-names used in this volume (in order)  |
| ImageUIDs           | list of dicom SOPInstanceUID of each slice                        |

- ``annotations.csv / annotations.json``

| Field               | Description                                                                                                            |
| -----               | -----                                                                                                                  |
| AnnotationID        | the unique (internal) AnnotationID                                                                                     |
| Primitive           | 0 for Nodules and NonNodules, 5 for NoduleVolume                                                                       |
| AnnotationData      | either bounding box for NoduleVolume or position and radius for Nodule/ NonNodule (DICOM Patient Coordiantes)          |
| VolumeID            | the unique VolumeID                                                                                                    |
| HUMax               | maximum Hounsfield unit in Annotation                                                                                  |
| HUMean              | mean Hounsfield unit in Annotation                                                                                     |
| HUMin               | minimal Hounsfield unit in Annotation                                                                                  |
| HUStd               | standard deviation of Hounsfield units in Annotation                                                                   |
| Label               | a label prefixed by the type NoduleVolume, Nodule or NonNodule, followed by the original label from LIDC/IDRI XML data |
| AnnotationsIncluded | for NoduleVolume, AnnotationIDs of contours that are included in this NoduleVolume                                     |
| AnnotationsExcluded | for NoduleVolume, AnnotationIDs of contours that are excluded in this NoduleVolume                                     |

- ``contours.csv / contours.json``

| Field          | Description                                                                                        |
| -----          | -----                                                                                              |
| AnnotationID   | the unique (internal) AnnotationID                                                                 |
| Primitive      | 2 for contours (input to NoduleVolumes)                                                            |
| AnnotationData | the triplets of contour coordinates in DICOM patient coordiantes                                   |
| VolumeID       | the unique VolumeID                                                                                |
| ImageUID       | dicom SOPInstanceUID of the corresponding slice                                                    |
| SlicePosition  | the slice number within the volume (starting from 0)                                               |
| Label          | a label prefixed by the type NoduleContour, followed by the original label from LIDC/IDRI XML data |


- ``cliques.csv / cliques.json``

| Field             | Description                                                                                   |
| -----             | -----                                                                                         |
| CliqueID          | the unique CliqueID                                                                           |
| PatientID         | the unique LIDC/IDRI PatientID                                                                |
| VolumeID          | the unique VolumeID (SeriesInstanceUID plus a number to force uniqueness within dicom series) |
| AnnoCount         | number of Annotations in the Clique                                                           |
| NoduleCount       | number of Annotations labeled as "Nodule < 3mm" in this Clique                                |
| NoduleVolumeCount | number of Annotations labeled as "Nodule >= 3mm" in this Clique                               |
| NonNoduleCount    | number of Annotions labeled as "NonNodule" in this Clique                                     |
| Annotations       | list of AnnotationIDs as cross reqference to Annotation table                                 |
| DiameterMean      | mean diameter of annotations in this clique                                                   |
| Diameters         | list of diameters                                                                             |
| DiceMean          | mean of all pairwise dice coefficients                                                        |
| Dices             | all pairwise dice coefficients                                                                |
| HUMax             | maximum Hounsfield unit in Clique                                                             |
| HUMean            | mean Hounsfield unit in Clique                                                                |
| HUMin             | minimal Hounsfield unit in Clique                                                             |
| HUStd             | standard deviation of Hounsfield units in Clique                                              |
| VolumeMean        | mean of all Annotation's volumes in $mm^3$                                                    |
| Volumes           | the Annotation's volumes in $mm^3$                                                            |

