# TractoR and DICOM

TractoR provides some facilities for working with DICOM files, but the [DICOM standard](http://dicom.nema.org/) is extremely complex, and TractoR's support for the DICOM file format cannot be said to be complete. Due to the varying conventions of the different scanner manufacturers, there can be several subtleties to correctly interpreting a given DICOM file. TractoR tries to follow best practices, and has been tested on files from a range of scanners from different vendors, but the accuracy of the results is not guaranteed.

**Please remember that TractoR is provided with no warranty. It is always advisable to check that your files are being correctly interpreted, for example with regard to orientation, before using these facilities on a regular basis.**

The `dicomtags` TractoR script allows you to list all of the DICOM tags in a particular file, along with their values. For example,

<pre>
<code>$ </code><kbd>tractor dicomtags $TRACTOR_HOME/tests/data/dicom/01.dcm</kbd>
<code>Starting TractoR environment...
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
Experiment completed with 0 warning(s) and 0 error(s)</code>
</pre>

For files from a Siemens scanner which contain an embedded, proprietary ASCII header, this can be extracted by setting the "SiemensAscii" option:

<pre>
<code>$ </code><kbd>tractor dicomtags $TRACTOR_HOME/tests/data/dicom/01.dcm SiemensAscii:true</kbd>
<code>Starting TractoR environment...

ulVersion                                = 0x1421cf5
tSequenceFileName                        = "%SiemensSeq%\gre"
tProtocolName                            = "fl3D+AF8-t1+AF8-sag"
tReferenceImage0                         = "1.3.12.2.1107.5.2.30.25471.30000008091010241767100000032"
tReferenceImage1                         = "1.3.12.2.1107.5.2.30.25471.30000008091010241767100000031"
tReferenceImage2                         = "1.3.12.2.1107.5.2.30.25471.30000008091010241767100000030"
ucScanRegionPosValid                     = 0x1
sProtConsistencyInfo.flNominalB0         = 1.494
sProtConsistencyInfo.flGMax              = 28
sProtConsistencyInfo.flRiseTime          = 5.88
sProtConsistencyInfo.lMaximumMatrixMode  = 3
sProtConsistencyInfo.lMaximumNofRxReceiverChannels = 32
sGRADSPEC.sEddyCompensationX.aflAmplitude[0] = -0.00673472
sGRADSPEC.sEddyCompensationX.aflAmplitude[1] = 0.0185389
sGRADSPEC.sEddyCompensationX.aflAmplitude[2] = -0.0125668
sGRADSPEC.sEddyCompensationX.aflAmplitude[3] = 0.000339731
sGRADSPEC.sEddyCompensationX.aflAmplitude[4] = 0.000556022
sGRADSPEC.sEddyCompensationX.aflTimeConstant[0] = 0.843937
sGRADSPEC.sEddyCompensationX.aflTimeConstant[1] = 0.67546
sGRADSPEC.sEddyCompensationX.aflTimeConstant[2] = 0.496574
sGRADSPEC.sEddyCompensationX.aflTimeConstant[3] = 0.0134406
sGRADSPEC.sEddyCompensationX.aflTimeConstant[4] = 0.00199835
sGRADSPEC.sEddyCompensationY.aflAmplitude[0] = 9.24251e-006
sGRADSPEC.sEddyCompensationY.aflAmplitude[1] = 0.00338827
sGRADSPEC.sEddyCompensationY.aflAmplitude[2] = -0.00623998
sGRADSPEC.sEddyCompensationY.aflAmplitude[3] = 0.000360011
sGRADSPEC.sEddyCompensationY.aflAmplitude[4] = 0.000695038
sGRADSPEC.sEddyCompensationY.aflTimeConstant[0] = 4.94781
sGRADSPEC.sEddyCompensationY.aflTimeConstant[1] = 0.475772
sGRADSPEC.sEddyCompensationY.aflTimeConstant[2] = 0.333851
sGRADSPEC.sEddyCompensationY.aflTimeConstant[3] = 0.0235249
sGRADSPEC.sEddyCompensationY.aflTimeConstant[4] = 0.00199169
sGRADSPEC.sEddyCompensationZ.aflAmplitude[0] = 0.000714731
sGRADSPEC.sEddyCompensationZ.aflAmplitude[1] = 0.00586569
sGRADSPEC.sEddyCompensationZ.aflAmplitude[2] = -0.00139115
sGRADSPEC.sEddyCompensationZ.aflAmplitude[3] = 0.00043755
sGRADSPEC.sEddyCompensationZ.aflAmplitude[4] = 0.000151853
sGRADSPEC.sEddyCompensationZ.aflTimeConstant[0] = 3.65802
sGRADSPEC.sEddyCompensationZ.aflTimeConstant[1] = 0.72544
sGRADSPEC.sEddyCompensationZ.aflTimeConstant[2] = 0.436477
sGRADSPEC.sEddyCompensationZ.aflTimeConstant[3] = 0.00752999
sGRADSPEC.sEddyCompensationZ.aflTimeConstant[4] = 0.000623619
sGRADSPEC.bEddyCompensationValid         = 1
sGRADSPEC.sB0CompensationX.aflAmplitude[0] = 0.0881172
sGRADSPEC.sB0CompensationX.aflAmplitude[1] = -0.256792
sGRADSPEC.sB0CompensationX.aflAmplitude[2] = -0.0108957
sGRADSPEC.sB0CompensationX.aflTimeConstant[0] = 0.634173
sGRADSPEC.sB0CompensationX.aflTimeConstant[1] = 0.437914
sGRADSPEC.sB0CompensationX.aflTimeConstant[2] = 0.00199995
sGRADSPEC.sB0CompensationY.aflAmplitude[0] = -0.180742
sGRADSPEC.sB0CompensationY.aflAmplitude[1] = 0.258984
sGRADSPEC.sB0CompensationY.aflAmplitude[2] = -0.0131336
sGRADSPEC.sB0CompensationY.aflTimeConstant[0] = 0.859313
sGRADSPEC.sB0CompensationY.aflTimeConstant[1] = 0.671842
sGRADSPEC.sB0CompensationY.aflTimeConstant[2] = 0.002
sGRADSPEC.sB0CompensationZ.aflAmplitude[0] = 0.0472476
sGRADSPEC.sB0CompensationZ.aflAmplitude[1] = 0.00701532
sGRADSPEC.sB0CompensationZ.aflAmplitude[2] = -0.0100074
sGRADSPEC.sB0CompensationZ.aflTimeConstant[0] = 0.632508
sGRADSPEC.sB0CompensationZ.aflTimeConstant[1] = 0.0393254
sGRADSPEC.sB0CompensationZ.aflTimeConstant[2] = 0.002
sGRADSPEC.bB0CompensationValid           = 1
sGRADSPEC.sCrossTermCompensationXY.aflAmplitude[0] = -0.000719198
sGRADSPEC.sCrossTermCompensationXY.aflTimeConstant[0] = 0.251639
sGRADSPEC.sCrossTermCompensationXZ.aflAmplitude[0] = -0.000914648
sGRADSPEC.sCrossTermCompensationXZ.aflTimeConstant[0] = 0.39668
sGRADSPEC.sCrossTermCompensationYX.aflAmplitude[0] = 0.00174321
sGRADSPEC.sCrossTermCompensationYX.aflTimeConstant[0] = 0.311602
sGRADSPEC.sCrossTermCompensationYZ.aflAmplitude[0] = 0.000162325
sGRADSPEC.sCrossTermCompensationYZ.aflTimeConstant[0] = 1.7505
sGRADSPEC.sCrossTermCompensationZX.aflAmplitude[0] = 0.00045993
sGRADSPEC.sCrossTermCompensationZX.aflTimeConstant[0] = 0.251497
sGRADSPEC.sCrossTermCompensationZY.aflAmplitude[0] = -0.000359235
sGRADSPEC.sCrossTermCompensationZY.aflTimeConstant[0] = 0.28182
sGRADSPEC.bCrossTermCompensationValid    = 1
sGRADSPEC.lOffsetX                       = -114
sGRADSPEC.lOffsetY                       = 13
sGRADSPEC.lOffsetZ                       = 147
sGRADSPEC.bOffsetValid                   = 1
sGRADSPEC.lDelayX                        = 13
sGRADSPEC.lDelayY                        = 13
sGRADSPEC.lDelayZ                        = 10
sGRADSPEC.bDelayValid                    = 1
sGRADSPEC.flSensitivityX                 = 7.96827e-005
sGRADSPEC.flSensitivityY                 = 7.97279e-005
sGRADSPEC.flSensitivityZ                 = 9.04655e-005
sGRADSPEC.bSensitivityValid              = 1
sGRADSPEC.alShimCurrent[0]               = 1053
sGRADSPEC.alShimCurrent[1]               = 258
sGRADSPEC.alShimCurrent[2]               = -299
sGRADSPEC.alShimCurrent[3]               = -67
sGRADSPEC.alShimCurrent[4]               = 30
sGRADSPEC.bShimCurrentValid              = 1
sGRADSPEC.ucMode                         = 0x1
sTXSPEC.asNucleusInfo[0].tNucleus        = "1H"
sTXSPEC.asNucleusInfo[0].lFrequency      = 63682891
sTXSPEC.asNucleusInfo[0].bFrequencyValid = 1
sTXSPEC.asNucleusInfo[0].flReferenceAmplitude = 216.107
sTXSPEC.asNucleusInfo[0].bReferenceAmplitudeValid = 1
sTXSPEC.asNucleusInfo[0].flAmplitudeCorrection = 1
sTXSPEC.asNucleusInfo[0].bAmplitudeCorrectionValid = 1
sTXSPEC.asNucleusInfo[1].bFrequencyValid = 1
sTXSPEC.asNucleusInfo[1].bReferenceAmplitudeValid = 1
sTXSPEC.asNucleusInfo[1].bAmplitudeCorrectionValid = 1
sTXSPEC.aRFPULSE[0].tName                = "SRFExcit"
sTXSPEC.aRFPULSE[0].bAmplitudeValid      = 0x1
sTXSPEC.aRFPULSE[0].flAmplitude          = 92.1055
sTXSPEC.lNoOfTraPulses                   = 1
sTXSPEC.lBTB1ParallelCapacity            = 4
sTXSPEC.lBTB1SerialCapacity              = 22
sTXSPEC.lBTB2ParallelCapacity            = 4
sTXSPEC.lBTB2SerialCapacity              = 22
sTXSPEC.bBTBValid                        = 1
sTXSPEC.flKDynMagnitudeMin               = 0.5
sTXSPEC.flKDynMagnitudeMax               = 1.5
sTXSPEC.flKDynMagnitudeClipLow           = 1
sTXSPEC.flKDynMagnitudeClipHigh          = 1
sTXSPEC.flKDynPhaseMax                   = 0.698132
sTXSPEC.flKDynPhaseClip                  = 0.174533
sTXSPEC.bKDynValid                       = 1
sTXSPEC.ucRFPulseType                    = 0x1
sTXSPEC.ucExcitMode                      = 0x1
sTXSPEC.ucSimultaneousExcitation         = 0x1
sRXSPEC.lGain                            = 1
sRXSPEC.bGainValid                       = 1
sRXSPEC.aFFT_SCALE[0].lRxChannel         = 1
sRXSPEC.aFFT_SCALE[0].flFactor           = 0.0329893
sRXSPEC.aFFT_SCALE[0].bValid             = 1
sRXSPEC.aFFT_SCALE[1].lRxChannel         = 2
sRXSPEC.aFFT_SCALE[1].flFactor           = 0.033267
sRXSPEC.aFFT_SCALE[1].bValid             = 1
sRXSPEC.aFFT_SCALE[2].lRxChannel         = 3
sRXSPEC.aFFT_SCALE[2].flFactor           = 0.032716
sRXSPEC.aFFT_SCALE[2].bValid             = 1
sRXSPEC.aFFT_SCALE[3].lRxChannel         = 4
sRXSPEC.aFFT_SCALE[3].flFactor           = 0.0309373
sRXSPEC.aFFT_SCALE[3].bValid             = 1
sRXSPEC.aFFT_SCALE[4].lRxChannel         = 5
sRXSPEC.aFFT_SCALE[4].flFactor           = 0.0306855
sRXSPEC.aFFT_SCALE[4].bValid             = 1
sRXSPEC.aFFT_SCALE[5].lRxChannel         = 6
sRXSPEC.aFFT_SCALE[5].flFactor           = 0.0303617
sRXSPEC.aFFT_SCALE[5].bValid             = 1
sRXSPEC.aFFT_SCALE[6].lRxChannel         = 7
sRXSPEC.aFFT_SCALE[6].flFactor           = 0.0315314
sRXSPEC.aFFT_SCALE[6].bValid             = 1
sRXSPEC.aFFT_SCALE[7].lRxChannel         = 8
sRXSPEC.aFFT_SCALE[7].flFactor           = 0.0323501
sRXSPEC.aFFT_SCALE[7].bValid             = 1
sRXSPEC.aFFT_SCALE[8].lRxChannel         = 9
sRXSPEC.aFFT_SCALE[8].flFactor           = 0.032852
sRXSPEC.aFFT_SCALE[8].bValid             = 1
sRXSPEC.aFFT_SCALE[9].lRxChannel         = 10
sRXSPEC.aFFT_SCALE[9].flFactor           = 0.0308782
sRXSPEC.aFFT_SCALE[9].bValid             = 1
sRXSPEC.aFFT_SCALE[10].lRxChannel        = 11
sRXSPEC.aFFT_SCALE[10].flFactor          = 0.0316006
sRXSPEC.aFFT_SCALE[10].bValid            = 1
sRXSPEC.aFFT_SCALE[11].lRxChannel        = 12
sRXSPEC.aFFT_SCALE[11].flFactor          = 0.031059
sRXSPEC.aFFT_SCALE[11].bValid            = 1
sRXSPEC.bVariCapVoltagesValid            = 1
sRXSPEC.alDwellTime[0]                   = 14000
sRXSPEC.alDwellTime[1]                   = 7500
sAdjFreSpec.ulMode                       = 0x1
sAdjShimSpec.ulMode                      = 0x2
sAdjWatSupSpec.ulMode                    = 0x1
alTR[0]                                  = 11000
alTI[0]                                  = 300000
lContrasts                               = 1
alTE[0]                                  = 4940
alTE[1]                                  = 20000
acFlowComp[0]                            = 1
acFlowComp[1]                            = 1
lCombinedEchoes                          = 1
sSliceArray.asSlice[0].sPosition.dSag    = -4.745762712
sSliceArray.asSlice[0].sPosition.dCor    = -16.94915254
sSliceArray.asSlice[0].sPosition.dTra    = -6.77966102
sSliceArray.asSlice[0].sNormal.dSag      = 1
sSliceArray.asSlice[0].dThickness        = 176
sSliceArray.asSlice[0].dPhaseFOV         = 224
sSliceArray.asSlice[0].dReadoutFOV       = 256
sSliceArray.lSize                        = 1
sSliceArray.lSag                         = 1
sSliceArray.lConc                        = 1
sSliceArray.ucMode                       = 0x4
sSliceArray.sTSat.dThickness             = 40
sSliceArray.sTSat.dGap                   = 10
sGroupArray.asGroup[0].nSize             = 1
sGroupArray.asGroup[0].dDistFact         = 0.2
sGroupArray.anMember[1]                  = -1
sGroupArray.lSize                        = 1
sGroupArray.sPSat.dThickness             = 50
sGroupArray.sPSat.dGap                   = 10
sAutoAlign.dAAMatrix[0]                  = 1
sAutoAlign.dAAMatrix[5]                  = 1
sAutoAlign.dAAMatrix[10]                 = 1
sAutoAlign.dAAMatrix[15]                 = 1
sNavigatorPara.ucRespComp                = 0x4
sNavigatorPara.adFree[13]                = 150000
sPrepPulses.ucFatSat                     = 0x4
sPrepPulses.ucWaterSat                   = 0x4
sPrepPulses.ucInversion                  = 0x4
sPrepPulses.ucSatRecovery                = 0x1
sPrepPulses.ucFatSatMode                 = 0x2
sLineTag.dDistance                       = 20
sGridTag.dDistance                       = 8
sKSpace.lBaseResolution                  = 256
sKSpace.lPhaseEncodingLines              = 224
sKSpace.dPhaseResolution                 = 1
sKSpace.lPartitions                      = 176
sKSpace.lImagesPerSlab                   = 176
sKSpace.dSliceResolution                 = 1
sKSpace.ucPhasePartialFourier            = 0x8
sKSpace.ucSlicePartialFourier            = 0x8
sKSpace.ucAveragingMode                  = 0x2
sKSpace.ucMultiSliceMode                 = 0x2
sKSpace.ucDimension                      = 0x4
sKSpace.unReordering                     = 0x1
sFastImaging.lEPIFactor                  = 1
sFastImaging.lTurboFactor                = 1
sFastImaging.lSegments                   = 1
sFastImaging.ulEnableRFSpoiling          = 0x1
sPhysioImaging.lSignal1                  = 1
sPhysioImaging.lMethod1                  = 1
sPhysioImaging.lSignal2                  = 1
sPhysioImaging.lMethod2                  = 1
sPhysioImaging.lPhases                   = 1
sPhysioImaging.lRetroGatedImages         = 16
sPhysioImaging.sPhysioECG.lTriggerPulses = 1
sPhysioImaging.sPhysioECG.lTriggerWindow = 5
sPhysioImaging.sPhysioECG.lArrhythmiaDetection = 1
sPhysioImaging.sPhysioECG.lCardiacGateOnThreshold = 100000
sPhysioImaging.sPhysioECG.lCardiacGateOffThreshold = 700000
sPhysioImaging.sPhysioPulse.lTriggerPulses = 1
sPhysioImaging.sPhysioPulse.lTriggerWindow = 5
sPhysioImaging.sPhysioPulse.lCardiacGateOnThreshold = 100000
sPhysioImaging.sPhysioPulse.lCardiacGateOffThreshold = 700000
sPhysioImaging.sPhysioExt.lTriggerPulses = 1
sPhysioImaging.sPhysioExt.lTriggerWindow = 5
sPhysioImaging.sPhysioExt.lCardiacGateOnThreshold = 100000
sPhysioImaging.sPhysioExt.lCardiacGateOffThreshold = 700000
sPhysioImaging.sPhysioResp.lRespGateThreshold = 20
sPhysioImaging.sPhysioResp.lRespGatePhase = 2
sPhysioImaging.sPhysioResp.dGatingRatio  = 0.3
sSpecPara.lPhaseCyclingType              = 1
sSpecPara.lPhaseEncodingType             = 1
sSpecPara.lRFExcitationBandwidth         = 1
sSpecPara.ucRemoveOversampling           = 0x1
sSpecPara.lDecouplingType                = 1
sSpecPara.lNOEType                       = 1
sSpecPara.lExcitationType                = 1
sSpecPara.lSpectralSuppression           = 1
sDiffusion.ulMode                        = 0x1
sAngio.ucPCFlowMode                      = 0x2
sAngio.ucTOFInflow                       = 0x4
sPreScanNormalizeFilter.ucOn             = 0x1
sEllipticalFilter.ucMode                 = 0x1
sPat.lAccelFactPE                        = 1
sPat.lAccelFact3D                        = 1
sPat.ucPATMode                           = 0x1
sPat.ucRefScanMode                       = 0x1
ucEnableIntro                            = 0x1
ucDisableChangeStoreImages               = 0x1
ucReconstructionMode                     = 0x1
ucPHAPSMode                              = 0x1
ucDixon                                  = 0x1
lAverages                                = 1
adFlipAngleDegree[0]                     = 15
lScanTimeSec                             = 332
lTotalScanTimeSec                        = 334
dRefSNR                                  = 328906.4548
dRefSNR_VOI                              = 328906.4548
tdefaultEVAProt                          = "%SiemensEvaDefProt%\Breast\Breast.evp"
tcurrentEVAProt                          = "%CURRENTEVAPROT%\EVA357.tmp"
asCoilSelectMeas[0].tNucleus             = "1H"
asCoilSelectMeas[0].iGlobalRFactor       = 3
asCoilSelectMeas[0].asList[0].sCoilElementID.tCoilID = "HeadMatrix"
asCoilSelectMeas[0].asList[0].sCoilElementID.lCoilCopy = 1
asCoilSelectMeas[0].asList[0].sCoilElementID.tElement = "HE4"
asCoilSelectMeas[0].asList[0].lElementSelected = 1
asCoilSelectMeas[0].asList[0].lRxChannelConnected = 1
asCoilSelectMeas[0].asList[1].sCoilElementID.tCoilID = "HeadMatrix"
asCoilSelectMeas[0].asList[1].sCoilElementID.lCoilCopy = 1
asCoilSelectMeas[0].asList[1].sCoilElementID.tElement = "H4S"
asCoilSelectMeas[0].asList[1].lElementSelected = 1
asCoilSelectMeas[0].asList[1].lRxChannelConnected = 2
asCoilSelectMeas[0].asList[2].sCoilElementID.tCoilID = "HeadMatrix"
asCoilSelectMeas[0].asList[2].sCoilElementID.lCoilCopy = 1
asCoilSelectMeas[0].asList[2].sCoilElementID.tElement = "H4T"
asCoilSelectMeas[0].asList[2].lElementSelected = 1
asCoilSelectMeas[0].asList[2].lRxChannelConnected = 3
asCoilSelectMeas[0].asList[3].sCoilElementID.tCoilID = "HeadMatrix"
asCoilSelectMeas[0].asList[3].sCoilElementID.lCoilCopy = 1
asCoilSelectMeas[0].asList[3].sCoilElementID.tElement = "HE3"
asCoilSelectMeas[0].asList[3].lElementSelected = 1
asCoilSelectMeas[0].asList[3].lRxChannelConnected = 4
asCoilSelectMeas[0].asList[4].sCoilElementID.tCoilID = "HeadMatrix"
asCoilSelectMeas[0].asList[4].sCoilElementID.lCoilCopy = 1
asCoilSelectMeas[0].asList[4].sCoilElementID.tElement = "H3S"
asCoilSelectMeas[0].asList[4].lElementSelected = 1
asCoilSelectMeas[0].asList[4].lRxChannelConnected = 5
asCoilSelectMeas[0].asList[5].sCoilElementID.tCoilID = "HeadMatrix"
asCoilSelectMeas[0].asList[5].sCoilElementID.lCoilCopy = 1
asCoilSelectMeas[0].asList[5].sCoilElementID.tElement = "H3T"
asCoilSelectMeas[0].asList[5].lElementSelected = 1
asCoilSelectMeas[0].asList[5].lRxChannelConnected = 6
asCoilSelectMeas[0].asList[6].sCoilElementID.tCoilID = "HeadMatrix"
asCoilSelectMeas[0].asList[6].sCoilElementID.lCoilCopy = 1
asCoilSelectMeas[0].asList[6].sCoilElementID.tElement = "HE2"
asCoilSelectMeas[0].asList[6].lElementSelected = 1
asCoilSelectMeas[0].asList[6].lRxChannelConnected = 7
asCoilSelectMeas[0].asList[7].sCoilElementID.tCoilID = "HeadMatrix"
asCoilSelectMeas[0].asList[7].sCoilElementID.lCoilCopy = 1
asCoilSelectMeas[0].asList[7].sCoilElementID.tElement = "H2S"
asCoilSelectMeas[0].asList[7].lElementSelected = 1
asCoilSelectMeas[0].asList[7].lRxChannelConnected = 8
asCoilSelectMeas[0].asList[8].sCoilElementID.tCoilID = "HeadMatrix"
asCoilSelectMeas[0].asList[8].sCoilElementID.lCoilCopy = 1
asCoilSelectMeas[0].asList[8].sCoilElementID.tElement = "H2T"
asCoilSelectMeas[0].asList[8].lElementSelected = 1
asCoilSelectMeas[0].asList[8].lRxChannelConnected = 9
asCoilSelectMeas[0].asList[9].sCoilElementID.tCoilID = "HeadMatrix"
asCoilSelectMeas[0].asList[9].sCoilElementID.lCoilCopy = 1
asCoilSelectMeas[0].asList[9].sCoilElementID.tElement = "HE1"
asCoilSelectMeas[0].asList[9].lElementSelected = 1
asCoilSelectMeas[0].asList[9].lRxChannelConnected = 10
asCoilSelectMeas[0].asList[10].sCoilElementID.tCoilID = "HeadMatrix"
asCoilSelectMeas[0].asList[10].sCoilElementID.lCoilCopy = 1
asCoilSelectMeas[0].asList[10].sCoilElementID.tElement = "H1S"
asCoilSelectMeas[0].asList[10].lElementSelected = 1
asCoilSelectMeas[0].asList[10].lRxChannelConnected = 11
asCoilSelectMeas[0].asList[11].sCoilElementID.tCoilID = "HeadMatrix"
asCoilSelectMeas[0].asList[11].sCoilElementID.lCoilCopy = 1
asCoilSelectMeas[0].asList[11].sCoilElementID.tElement = "H1T"
asCoilSelectMeas[0].asList[11].lElementSelected = 1
asCoilSelectMeas[0].asList[11].lRxChannelConnected = 12
asCoilSelectMeas[0].sCOILPLUGS.aulPlugId[0] = 0xff
asCoilSelectMeas[0].sCOILPLUGS.aulPlugId[1] = 0xee
asCoilSelectMeas[0].sCOILPLUGS.aulPlugId[2] = 0xee
asCoilSelectMeas[0].sCOILPLUGS.aulPlugId[3] = 0xad
asCoilSelectMeas[0].sCOILPLUGS.aulPlugId[4] = 0xee
asCoilSelectMeas[0].sCOILPLUGS.aulPlugId[5] = 0xee
asCoilSelectMeas[0].sCOILPLUGS.aulPlugId[6] = 0x5d
asCoilSelectMeas[0].sCOILPLUGS.aulPlugId[7] = 0xb1
asCoilSelectMeas[0].sCOILPLUGS.aulPlugId[8] = 0xee
asCoilSelectMeas[0].sCOILPLUGS.aulPlugId[9] = 0xb2
asCoilSelectMeas[0].sCOILPLUGS.aulPlugId[10] = 0xee
asCoilSelectMeas[0].sCOILPLUGS.auiNmbrOfNibbles[0] = 0x2
asCoilSelectMeas[0].sCOILPLUGS.auiNmbrOfNibbles[1] = 0x2
asCoilSelectMeas[0].sCOILPLUGS.auiNmbrOfNibbles[2] = 0x2
asCoilSelectMeas[0].sCOILPLUGS.auiNmbrOfNibbles[3] = 0x2
asCoilSelectMeas[0].sCOILPLUGS.auiNmbrOfNibbles[4] = 0x2
asCoilSelectMeas[0].sCOILPLUGS.auiNmbrOfNibbles[5] = 0x2
asCoilSelectMeas[0].sCOILPLUGS.auiNmbrOfNibbles[6] = 0x2
asCoilSelectMeas[0].sCOILPLUGS.auiNmbrOfNibbles[7] = 0x2
asCoilSelectMeas[0].sCOILPLUGS.auiNmbrOfNibbles[8] = 0x2
asCoilSelectMeas[0].sCOILPLUGS.auiNmbrOfNibbles[9] = 0x2
asCoilSelectMeas[0].sCOILPLUGS.auiNmbrOfNibbles[10] = 0x2
ulApplicationDetails                     = 0x1
sEFISPEC.bEFIDataValid                   = 1

Experiment completed with 0 warning(s) and 0 error(s)</code>
</pre>

Different scans within a single session are often divided into different image "series", and these can be separated using the `dicomsort` script:

<pre>
<code>$ </code><kbd>tractor dicomsort $TRACTOR_HOME/tests/data/dicom</kbd>
<code>Starting TractoR environment...
* * INFO: Reading series identifiers from 4 files
* * INFO: Found series 8, 9; creating subdirectories
* * INFO: Series 8 includes 2 files; description is "DTIb3000s5"
* * INFO: Series 9 includes 2 files; description is "fl3D_t1_sag"
Experiment completed with 0 warning(s) and 0 error(s)</code>
</pre>

Finally, a directory of DICOM files can be converted to an Analyze/NIfTI/MGH image using the `dicomread` script:

<pre>
<code>$ </code><kbd>tractor dicomread $TRACTOR_HOME/tests/data/dicom/9_fl3D_t1_sag</kbd>
<code>Starting TractoR environment...
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
Experiment completed with 0 warning(s) and 0 error(s)</code>
</pre>

As of TractoR version 2.1.0, the `imageinfo` script can be used instead, if only information about the image formed from the DICOM directory is required.
