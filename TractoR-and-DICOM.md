# TractoR and DICOM

TractoR provides some facilities for working with DICOM files, but the [DICOM standard](http://dicom.nema.org/) is extremely complex, and TractoR's support for the DICOM file format cannot be said to be complete. Due to the varying conventions of the different scanner manufacturers, there can be several subtleties to correctly interpreting a given DICOM file. TractoR tries to follow best practices, and has been tested on files from a range of scanners from different vendors, but the accuracy of the results is not guaranteed.

**Please remember that TractoR is provided with no warranty. It is always advisable to check that your files are being correctly interpreted, for example with regard to orientation, before using these facilities on a regular basis.**

The `dicomtags` TractoR script allows you to list all of the DICOM tags in a particular file, along with their values. For example,

    $ tractor dicomtags $TRACTOR_HOME/tests/data/dicom/01.dcm
    Starting TractoR environment...
    DESCRIPTION                   VALUE
     Group 0002 Length             188
     Media Stored SOP Class UID    1.2.840.10008.5.1.4.1.1.4
     Media Stored SOP Instance U   1.3.12.2.1107.5.2.30.25471.30000008091010241767100006233
     Transfer Syntax UID           1.2.840.10008.1.2.1
     Implementation Class UID      1.3.12.2.1107.5.2
     Implementation Version Name   MR_2004V_VB11A
     Specific Character Set        ISO_IR 100
     Image Type                    ORIGINAL, PRIMARY, M, ND, NORM
     SOP Class UID                 1.2.840.10008.5.1.4.1.1.4
     SOP Instance UID              1.3.12.2.1107.5.2.30.25471.30000008091010241767100006233
     Study Date                    00000000
     Series Date                   00000000
     Acquisition Date              00000000
     Image Date                    00000000
     Study Time                    000000.000000
     Series Time                   000000.000000
     Acquisition Time              000000.000000
     Image Time                    000000.000000
     Accession Number              NA
     Modality                      MR
     Manufacturer                   
     Referring Physician's Name    NA
     Station Name                   
     Study Description              
     Series Description            fl3D_t1_sag
     Manufacturer's Model Name      
     Referenced Image Sequence     <fe><ff>
     Patient's Name                 
     Patient ID                     
     Patient's Birth Date          00000000
     Patient's Sex                  
     Patient's Age                 000Y
     Patient's Weight              NA
     Scanning Sequence             GR
     Sequence Variant              SP
     Scan Options                  NA
     MR Acquisition Type           3D
     Sequence Name                 *fl3d1
     Angio Flag                    N
     Slice Thickness               1
     Repetition Time               11
     Echo Time                     4.94
     Number of Averages            1
     Imaging Frequency             63.682891
     Imaged Nucleus                1H
     Echo Numbers(s)               0
     Magnetic Field Strength       1.4939999580383
     Number of Phase Encoding St   196
     Echo Train Length             1
     Percent Sampling              100
     Percent Phase Field of View   87.5
     Pixel Bandwidth               140
     Device Serial Number           
     Software Versions(s)           
     Protocol Name                 fl3D_t1_sag
     Date of Last Calibration      00000000
     Time of Last Calibration      000000.000000
     Transmitting Coil             Body
     Acquisition Matrix            0, 256, 224, 0
     Phase Encoding Direction      ROW
     Flip Angle                    15
     Variable Flip Angle Flag      N
     SAR                           0.01391938515007
     dB/dt                         0
     Patient Position              HFS
     Study Instance UID            1.3.12.2.1107.5.2.30.25471.30000008091010234898400000004
     Series Instance UID           1.3.12.2.1107.5.2.30.25471.30000008091010241767100006157
     Study ID                      1
     Series Number                 9
     Acquisition Number            1
     Image Number                  76
     Image Position (Patient)      -17.245762825012, -128.9491519928, 121.22033882141
     Image Orientation (Patient)   0, 1, 0, 0, 0, -1
     Frame of Reference UID        1.3.12.2.1107.5.2.30.25471.20080910140448828.0.0.0
     Position Reference Indicato   NA
     Slice Location                -17.245762825012
     Samples per Pixel             1
     Photometric Interpretation    MONOCHROME2
     Rows                          256
     Columns                       224
     Pixel Spacing                 1, 1
     Bits Allocated                16
     Bits Stored                   12
     High Bit                      11
     Pixel Representation          0
     Smallest Image Pixel Value    3
     Largest Image Pixel Value     423
     Window Center                 248
     Window Width                  523
     Window Center & Width Expla   Algo1
     Unknown (0x0029, 0x0010)      SIEMENS CSA HEADER
     Unknown (0x0029, 0x0011)      SIEMENS MEDCOM HEADER
     Unknown (0x0029, 0x0012)      SIEMENS MEDCOM HEADER2
     Unknown (0x0029, 0x1008)      IMAGE NUM 4
     Unknown (0x0029, 0x1009)      20080910
     Unknown (0x0029, 0x1018)      MR
     Unknown (0x0029, 0x1019)      20080910
     Unknown (0x0029, 0x1131)      10.0.456247390
     Unknown (0x0029, 0x1132)      114688
     Unknown (0x0029, 0x1133)      0
     Unknown (0x0029, 0x1134)      DB TO DICOM
     Unknown (0x0029, 0x1260)      com
     Requested Procedure Descrip    
     Unknown (0x0040, 0x0244)      00000000
     Unknown (0x0040, 0x0245)      000000.000000
     Unknown (0x0040, 0x0253)      MR20080910140448
     Unknown (0x0040, 0x0254)       
     Storage Media File-set UID    1.3.12.2.1107.5.2.30.25471.30000008091107165685900000001
     Unknown (0x0088, 0x0200)      <fe><ff>
    Experiment completed with 0 warning(s) and 0 error(s)

Different scans within a single session are often divided into different image "series", and these can be separated using the `dicomsort` script:

    $ tractor dicomsort $TRACTOR_HOME/tests/data/dicom
    Starting TractoR environment...
    * * INFO: Reading series identifiers from 4 files
    * * INFO: Found series 8, 9; creating subdirectories
    * * INFO: Series 8 includes 2 files; description is "DTIb3000s5"
    * * INFO: Series 9 includes 2 files; description is "fl3D_t1_sag"
    Experiment completed with 0 warning(s) and 0 error(s)

Finally, a directory of DICOM files can be converted to an Analyze/NIfTI/MGH image using the `dicomread` script:

    $ tractor dicomread $TRACTOR_HOME/tests/data/dicom/9_fl3D_t1_sag
    Starting TractoR environment...
    * * INFO: Looking for DICOM files in directory /usr/local/tractor/tests/data/dicom/9_fl3D_t1_sag
    * * INFO: Reading image information from 2 files
    INFO: [x2] Data matrix is transposed relative to acquisition matrix
    * * INFO: Image orientation is PIR
    * * INFO: Data set contains 1 volume(s); 2 slice(s) per volume
         Image source : /usr/local/tractor/tests/data/dicom/9_fl3D_t1_sag
     Image dimensions : 2 x 224 x 256 voxels
     Voxel dimensions : 1 x 1 x 1 mm
    Coordinate origin : (19.25,95.05,134.78)
      Additional tags : 0
           Sparseness : 0.84% (dense storage)
    Experiment completed with 0 warning(s) and 0 error(s)

As of TractoR version 2.1.0, the `imageinfo` script can be used instead, if only information about the image formed from the DICOM directory is required.
