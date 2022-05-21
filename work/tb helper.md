# exmpale

h265
```bash
 ~/bin/br100_testenc_h265_cmodels -P 0 -L 123  -w 1280 -y 720 -a 0 -b 2 -i 720p_nv12.yuv   -o 720p_cmodels.265

./br100_testenc_h26x  -P 0 -L 123 -x 1280 -y 720 -a 0 -b 2 -i /home/bright/stream/720p_nv12.yuv -o 720p_silicon.265  --memType=2

 ./br100_testenc_h26x  -P 0 -L 123 -x 1280 -y 720 -a 0 -b 2 -i media/gpu/vcodec/stream/encoder/Jockey_1280x720_yuv420p.yuv  -o 720_asic.265  --memType=2  --waitInterval=500000

./brv_unit_test --gtest_filter=TestBrvEncH26x.enc_hevc_0

./br100_testenc_h26x  -P 0 -L 123 -x 1280 -y 720 -a 0 -b 1 -i  /home/bright/br_build/media/gpu/vcodec/stream/encoder/Jockey_1280x720_yuv420p.yuv  -o 720_asic.265  --memType=2  --hashType=1
```
#CLI help
```c
Default parameters are marked inside []. More detailed descriptions of
C-Model command line parameters can be found from C-Model Command Line API Manual.

  -H --help                        This help

 Parameters affecting encoder input/output frames:
  -i[s] --input                    Read input video sequence from file. [input.yuv]
  -o[s] --output                   Write output HEVC/H.264 stream to file. [stream.hevc]
  -a[n] --firstPic                 The first picture to encode in the input file. [0]
  -b[n] --lastPic                  The last picture to encode in the input file. [100]
        --outReconFrame            0..1 Reconstructed frame output mode. [1]
                                     0 - Do not output reconstructed frames.
                                     1 - Output reconstructed frames.
  -f[n] --outputRateNumer          1..1048575 Output picture rate numerator. [30]
  -F[n] --outputRateDenom          1..1048575 Output picture rate denominator. [1]
                                   Encoded frame rate will be
                                   outputRateNumer/outputRateDenom fps
  -j[n] --inputRateNumer           1..1048575 Input picture rate numerator. [30]
  -J[n] --inputRateDenom           1..1048575 Input picture rate denominator. [1]

 Parameters affecting input frame and encoded frame resolutions and cropping:
  -w[n] --lumWidthSrc              Width of source image in pixels. [176]
  -h[n] --lumHeightSrc             Height of source image in pixels. [144]
  -x[n] --width                    Width of encoded output image in pixels. [--lumWidthSrc]
  -y[n] --height                   Height of encoded output image in pixels. [--lumHeightSrc]
  -X[n] --horOffsetSrc             Output image horizontal cropping offset, must be even. [0]
  -Y[n] --verOffsetSrc             Output image vertical cropping offset, must be even. [0]
 
 Parameters affecting input frame and reference frame buffer alignment in memory:
        --inputAlignmentExp        0, 4..12 Alignment value of input frame buffer. [4]
                                     0 = Disable alignment
                                     4..12 = Base address of input frame buffer and each line are aligned to 2^inputAlignmentExp.
        --refAlignmentExp          0, 4..12 Reference frame buffer alignment [0]
                                     0 = Disable alignment 
                                     4..12 = Base address of reference frame buffer and each line are aligned to 2^refAlignmentExp.
        --refChromaAlignmentExp    0, 4..12 Reference frame buffer alignment for chroma [0]
                                     0 = Disable alignment 
                                     4..12 = Base address of chroma reference frame buffer and each line are aligned to 2^refChromaAlignmentExp.

 Parameters for pre-processing frames before encoding:
  -l[n] --inputFormat              Input YUV format. [0]
                                     0 - YUV420 planar CbCr (IYUV/I420)
                                     1 - YUV420 semiplanar CbCr (NV12)
                                     2 - YUV420 semiplanar CrCb (NV21)
                                     3 - YUYV422 interleaved (YUYV/YUY2)
                                     4 - UYVY422 interleaved (UYVY/Y422)
                                     5 - RGB565 16bpp
                                     6 - BGR565 16bpp
                                     7 - RGB555 16bpp
                                     8 - BGR555 16bpp
                                     9 - RGB444 16bpp
                                     10 - BGR444 16bpp
                                     11 - RGB888 32bpp
                                     12 - BGR888 32bpp
                                     13 - RGB101010 32bpp
                                     14 - BGR101010 32bpp
                                     15 - YUV420 10 bit planar CbCr (I010)
                                     16 - YUV420 10 bit planar CbCr (P010)
                                     17 - YUV420 10 bit planar CbCr packed
                                     18 - YUV420 10 bit packed (Y0L2)
                                     19 - YUV420 customer private tile for HEVC
                                     20 - YUV420 customer private tile for H.264
                                     21 - YUV420 semiplanar CbCr customer private tile
                                     22 - YUV420 semiplanar CrCb customer private tile
                                     23 - YUV420 P010 customer private tile
                                     24 - YUV420 semiplanar 101010 
                                     26 - YUV420 8 bit tile 64x4 
                                     27 - YUV420 CbCr 8 bit tile 64x4 
                                     28 - YUV420 10 bit tile 32x4 
                                     29 - YUV420 10 bit tile 48x4 
                                     30 - YUV420 CrCb 10 bit tile 48x4 
                                     31 - YUV420 8 bit tile 128x2 
                                     32 - YUV420 CbCr 8 bit tile 128x2 
                                     33 - YUV420 10 bit tile 96x2 
                                     34 - YUV420 CrCb 10 bit tile 96x2 
                                     35 - YUV420 semiplanar 8 bit tile 8x8 
                                     36 - YUV420 semiplanar 10 bit tile 8x8 
  -O[n] --colorConversion          RGB to YCbCr color conversion type. [0]
                                     0 - ITU-R BT.601, RGB limited [16..235] (BT601_l.mat)
                                     1 - ITU-R BT.709, RGB limited [16..235] (BT709_l.mat)
                                     2 - User defined, coefficients defined in test bench.
                                     3 - ITU-R BT.2020
                                     4 - ITU-R BT.601, RGB full [0..255] (BT601_f.mat)
                                     5 - ITU-R BT.601, RGB limited [0..219] (BT601_219.mat)
                                     6 - ITU-R BT.709, RGB full [0..255] (BT709_f.mat)
        --mirror                   Mirror input image. [0]
                                     0 - disabled
                                     1 - mirror
  -r[n] --rotation                 Rotate input image. [0]
                                     0 - disabled
                                     1 -  90 degrees right
                                     2 -  90 degrees left
                                     3 - 180 degrees right
  -Z[n] --videoStab               Enable video stabilization or scene change detection. [0]
                                    Stabilization works by adjusting cropping offset for
                                    every frame. Scene change detection encodes scene
                                    changes as intra frames, it is enabled when
                                    input resolution == encoded resolution.

        --scaledWidth              0..width, width of encoder down-scaled image, 0=disable [0]
        --scaledHeight             0..height, height of encoder down-scaled image, 0=disable [0], written in scaled.yuv
        --scaledOutputFormat       scaler output frame format, 0=YUV422, 1=YUV420 semiplanar CbCr (NV12) [0]
        --interlacedFrame          0=Input progressive field
                                   1=Input frame with fields interlaced [0]
        --fieldOrder               Interlaced field order, 0=bottom first, 1=top first [0]
        --codedChromaIdc           coded chroma format idc.[1]
                                     0-4:0:0
                                     1-4:2:0

 Parameters for SW to convert input to customized specific format:
        --formatCustomizedType     -1..13 Set customized input format ID. [-1]
                                     -1 = Disable format conversion
                                     0..13 = Convert to one customized format

 Parameters affecting the output stream and encoding tools:
  -P[n] --profile                  VC8000E/HEVC encoder profile [0]
                                     VC8000E/HEVC encoder only supports Main profile, Main Still Picture profile, and Main 10 profile.
                                     0 - Main profile
                                     1 - Main Still Picture profile
                                     2 - Main 10 profile
                                     3 - MAINREXT profile
                                   VC8000E/H.264 encoder profile [11]
                                     VC8000E/H.264 only supports Baseline, Main, High, High 10 profiles.
                                     9  - Baseline profile
                                     10 - Main profile
                                     11 - High profile
                                     12 - High 10 profile
  -L[n] --level                    VC8000E/HEVC level. 180 = level 6.0*30 [180]
                                     VC8000E/HEVC HW only supports less than or equal to level 5.1 High tier in real-time.
                                     For levels 5.0 and 5.1, support resolutions up to 4096x2048 with 4K@60fps performance.
                                     For levels greater than level 5.1, support in non-realtime mode.
                                     Each level has resolution and bitrate limitations:
                                     30  - level 1.0  QCIF      (176x144)       128 kbps
                                     60  - level 2.0  CIF       (352x288)       1.5 Mbps
                                     63  - level 2.1  Q720p     (640x360)       3.0 Mbps
                                     90  - level 3.0  QHD       (960x540)       6.0 Mbps
                                     93  - level 3.1  720p HD   (1280x720)      10.0 Mbps
                                     120 - level 4.0  2Kx1080   (2048x1080)     12.0 Mbps   High tier 30 Mbps
                                     123 - level 4.1  2Kx1080   (2048x1080)     20.0 Mbps   High tier 50 Mbps
                                     150 - level 5.0  4096x2160 (4096x2160)     25.0 Mbps   High tier 100 Mbps
                                     153 - level 5.1  4096x2160 (4096x2160)     40.0 Mbps   High tier 160 Mbps
                                     156 - level 5.2  4096x2160 (4096x2160)     60.0 Mbps   High tier 240 Mbps
                                     180 - level 6.0  8192x4320 (8192x4320)     60.0 Mbps   High tier 240 Mbps
                                     183 - level 6.1  8192x4320 (8192x4320)     120.0 Mbps  High tier 480 Mbps
                                     186 - level 6.2  8192x4320 (8192x4320)     240.0 Mbps  High tier 800 Mbps
                                   VC8000E/H.264 level. 51 = Level 5.1 [51]
                                     10 - H264_LEVEL_1 
                                     99 - H264_LEVEL_1_b 
                                     11 - H264_LEVEL_1_1 
                                     12 - H264_LEVEL_1_2 
                                     13 - H264_LEVEL_1_3 
                                     20 - H264_LEVEL_2 
                                     21 - H264_LEVEL_2_1 
                                     22 - H264_LEVEL_2_2
                                     30 - H264_LEVEL_3 
                                     31 - H264_LEVEL_3_1 
                                     32 - H264_LEVEL_3_2 
                                     40 - H264_LEVEL_4 
                                     41 - H264_LEVEL_4_1 
                                     42 - H264_LEVEL_4_2 
                                     50 - H264_LEVEL_5 
                                     51 - H264_LEVEL_5_1 
                                     52 - H264_LEVEL_5_2 
                                     60 - H264_LEVEL_6 
                                     61 - H264_LEVEL_6_1 
                                     62 - H264_LEVEL_6_2 
        --tier                     VC8000E/HEVC encoder tier [0]
                                     VC8000E/HEVC encoder only supports Main tier and High tier
                                     0 - Main tier
                                     1 - High tier
        --bitDepthLuma             bit depth of luma samples in encoded stream [8]
                                     8=8 bit,9=9 bit, 10=10bit
        --bitDepthChroma           bit depth of chroma samples in encoded stream [8]
                                     8=8 bit,9=9 bit, 10=10bit
  -N[n] --byteStream               Stream type. [1]
                                     0 - NAL units. NAL sizes are returned in file <nal_sizes.txt>
                                     1 - byte stream according to HEVC Standard Annex B.
        --ivf                      IVF encapsulation, for AV1 only. [1]
                                     0 - OBU raw output
                                     1 - IVF output (default)
  -k[n] --videoRange               0..1 Video signal sample range in encoded stream. [0]
                                     0 - Y range in [16..235]; Cb, Cr in [16..240]
                                     1 - Y, Cb, Cr range in [0..255]
        --streamBufChain           Enable two output stream buffers. [0]
                                     0 - Single output stream buffer.
                                     1 - Two output stream buffers chained together.
                                     Note the minimum allowable size of the first stream buffer is 11k bytes.
  -S[n] --sei                      Enable SEI messages (buffering period + picture timing) [0]
                                   Writes Supplemental Enhancement Information messages
                                   containing information about picture time stamps
                                   and picture buffering into stream.
        --codecFormat              Select Video Codec Format  [0]
                                   0: HEVC video format encoding
                                   1: H.264 video format encoding
                                   2: AV1 video format encoding
  -p[n] --cabacInitFlag            0..1 Initialization value for CABAC. [0]
  -K[n] --enableCabac              0=OFF (CAVLC), 1=ON (CABAC). [1]
  -e[n] --sliceSize                [0..height/ctu_size] slice size in number of CTU rows [0]
                                     0 to encode each picture in one slice
                                     [1..height/ctu_size] to encode each slice with N CTU rows
  -D[n] --disableDeblocking        0..1 Disable deblocking filter [0]
                                     0 = Inloop deblocking filter enabled (better quality)
                                     1 = Inloop deblocking filter disabled
  -M[n] --enableSao                0..1 Disable or enable SAO filter [1]
                                     0 = SAO disabled
                                     1 = SAO enabled
  -W[n] --tc_Offset                -6..6 Controls deblocking filter alpha_c0_offset (H.264) or tc_offset (HEVC). [-2]
  -E[n] --beta_Offset              -6..6 Deblocking filter beta_offset (H.264 and HEVC). [5]
        --enableDeblockOverride    0..1 Deblocking override enable flag [0]
                                     0 = Disable override
                                     1 = Enable override
        --deblockOverride          0..1 Deblocking override flag [0]
                                     0 = Do not override filter parameters
                                     1 = Override filter parameters
        --tile=a:b:c               HEVC Tile setting: Tile is enabled when num_tile_columns * num_tile_rows > 1. [1:1:1]
                                       a: num_tile_columns 
                                       b: num_tile_rows 
                                       c: loop_filter_across_tiles_enabled_flag 
        --enableScalingList        0..1 Use average or default scaling list. [0]
                                     0 = Use average scaling list.
                                     1 = Use default scaling list.
        --RPSInSliceHeader         0..1 Encoding RPS in the slice header. [0]
                                   0 = not encoding RPS in the slice header. 
                                   1 = encoding RPS in the slice header. 
        --POCConfig=a:b:c          POC type/number of bits settings.
                                       a: picOrderCntType. [0] 
                                       b: log2MaxPicOrderCntLsb.[16] 
                                       c: log2MaxFrameNum.[12] 
      --psyFactor                0..4 Weight of psycho-visual encoding. [0]
                                     0 = disable psy-rd.
                                     1..4 = encode psy-rd, and set strength of psyFactor, larger favor better subjective quality.

 Parameters affecting GOP pattern, rate control and output stream bitrate:
  -R[n] --intraPicRate             Intra-picture rate in frames. [0]
                                   Forces every Nth frame to be encoded as intra frame.
                                   0 = Do not force
  -B[n] --bitPerSecond             10000..levelMax, target bitrate for rate control, in bps. [1000000]
        --tolMovingBitRate         0..2000, percent tolerance over target bitrate of moving bitrate [2000]
        --monitorFrames            10..120, how many frames will be monitored for moving bitrate [frame rate]
        --bitVarRangeI             10..10000, percent variations over the average bits per frame for I frame [10000]
        --bitVarRangeP             10..10000, percent variations over the average bits per frame for P frame [10000]
        --bitVarRangeB             10..10000, percent variations over the average bits per frame for B frame [10000]
        --staticSceneIbitPercent  0...100 I frame bits percent of bitrate in static scene [80]
  --crf[n]                         -1..51 Constant rate factor mode, working with look-ahead turned on. -1=disable. [-1]
                                   CRF mode is to keep a certain level of quality based on crf value, working as constant QP with complexity rate control.
                                   CRF adjusts frame level QP within range of crf constant +-3 based on frame complexity. CRF will disable VBR mode if both enabled.
  -U[n] --picRc                    0=OFF, 1=ON Picture rate control. [0]
                                   Calculates a new target QP for every frame.
        --smoothPsnrInGOP          0=disable, 1=enable Smooth PSNR for frames in one GOP. [0]
                                   Only affects gopSize > 1.
  -u[n] --ctbRc                    0..3 CTB QP adjustment mode for Rate Control and Subjective Quality. [0]
                                     0 = No CTB QP adjustment.
                                     1 = CTB QP adjustment for Subjective Quality only.
                                     2 = CTB QP adjustment for Rate Control only. (For HwCtbRcVersion >= 1 only)
                                     3 = CTB QP adjustment for both Subjective Quality and Rate Control. (For HwCtbRcVersion >= 1 only)
                                     4 = CTB QP adjustment for Subjective Quality only, reversed.
                                     6 = CTB QP adjustment for both Subjective Quality reversed and Rate Control. (For HwCtbRcVersion >= 1 only)
        --blockRCSize              Block size in CTB QP adjustment for Subjective Quality [0]
                                     0=64x64 ,1=32x32, 2=16x16
        --rcQpDeltaRange           Max absolute value of CU/MB QP delta relative to frame QP in CTB RC [10]
                                   0..15 for HwCtbRcVersion <= 1; 0..51 for HwCtbRcVersion > 1.
        --rcBaseMBComplexity       0..31 MB complexity base in CTB QP adjustment for Subjective Quality [15]
                                   qpOffset is larger for CU/MB with larger complexity offset from rcBaseMBComplexity.
        --tolCtbRcInter            Tolerance of CTB Rate Control for INTER frames. <float> [0.0]
                                   CTB RC will try to limit INTER frame bits within the range of:
                                       [targetPicSize/(1+tolCtbRcInter), targetPicSize*(1+tolCtbRcInter)].
                                   A negative number means no bitrate limit in CTB RC.
        --tolCtbRcIntra            Tolerance of CTB Rate Control for INTRA frames. <float> [-1.0]
        --ctbRowQpStep             The maximum accumulated QP adjustment step per CTB Row allowed by CTB rate control.
                                   Default value is [4] for H.264 and [16] for HEVC.
                                   QP_step_per_CTB = (ctbRowQpStep / Ctb_per_Row) and limited by maximum = 4.
        --picQpDeltaRange          Min:Max. Qp_Delta range in picture RC.
                                   Min: -10..-1 Minimum Qp_Delta in picture RC. [-2]
                                   Max:  1..10  Maximum Qp_Delta in picture RC. [3]
                                   This range only applies to two neighboring frames of the same coding type.
                                   This range doesn't apply when HRD overflow occurs.
  -C[n] --hrdConformance           0=OFF, 1=ON HRD conformance. [0]
                                   Uses standard defined model to limit bitrate variance.
  -c[n] --cpbSize                  HRD Coded Picture Buffer size in bits. [1000000]
                                   Buffer size used by the HRD model.
  -g[n] --bitrateWindow            1..300, Bitrate window length in frames [intraPicRate]
                                   Rate control allocates bits for one window and tries to
                                   match the target bitrate at the end of each window.
                                   Typically window begins with an intra frame, but this
                                   is not mandatory.
        --gopSize                  GOP Size. [0]
                                   0..8, 0 for adaptive GOP size; 1~7 for fixed GOP size
        --gopConfig                User-specified GOP configuration file, which defines the GOP structure table.
                                   FrameN Type POC QPoffset QPfactor TemporalId num_ref_pics ref_pics used_by_cur
                                     -FrameN: Normal GOP config. The table should contain gopSize lines, named Frame1, Frame2, etc.
                                      The frames are listed in decoding order.
                                     -Type: Slice type, can be either P or B.
                                     -POC: Display order of the frame within a GOP, ranging from 1 to gopSize.
                                     -QPoffset: It is added to the QP parameter to set the final QP value used for this frame.
                                     -QPfactor: Weight used during rate distortion optimization.
                                     -TemporalId: temporal layer ID.
                                     -num_ref_pics: The number of reference pictures kept for this frame,
                                      including references for current and future pictures.
                                     -ref_pics: A List of num_ref_pics integers,
                                      specifying the delta_POC of the reference pictures kept, relative to the POC of the current frame or LTR's index.
                                     -used_by_cur: A List of num_ref_pics binaries,
                                      specifying whether the corresponding reference picture is used by current picture.
                                     If this config file is not specified, default parameters will be used.
                                   Frame0 Type QPoffset QPfactor TemporalId num_ref_pics ref_pics used_by_cur LTR Offset Interval
                                     -Frame0: Special GOP config. The table should contain gopSize lines.
                                      The frames are listed in decoding order.
                                     -Type: Slice type. If the value is not reserved, it overrides the value in normal config for special frame. [-255]
                                     -QPoffset: If the value is not reserved, it overrides the value in normal config for special frame. [-255]
                                     -QPfactor: If the value is not reserved, it overrides the value in normal config for special frame. [-255]
                                     -TemporalId: temporal layer ID. If the value is not reserved, it overrides the value in normal config for special frame. [-255]
                                     -num_ref_pics: The number of reference pictures kept for this frame
                                      including references for current and future pictures.
                                     -ref_pics: A List of num_ref_pics integers,
                                      specifying the delta_POC of the reference pictures kept, relative to the POC of the current frame or LTR's index.
                                     -used_by_cur: A List of num_ref_pics binaries, specifying whether the corresponding reference picture is used by current picture.
                                     -LTR: 0..VCENC_MAX_LT_REF_FRAMES. long term reference setting, 0 - common frame, 1..VCENC_MAX_LT_REF_FRAMES - long term reference's index
                                     -Offset: If LTR = 0, POC_Frame_Use_LTR(0) - POC_LTR. POC_LTR is LTR's POC, POC_Frame_Use_LTR(0) is the first frame after LTR that uses the LTR as reference.
                                              If LTR != 0, the offset of the first LTR frame to the first encoded frame.
                                     -Interval: If LTR = 0, POC_Frame_Use_LTR(n+1) - POC_Frame_Use_LTR(n). The POC delta between two consecutive frames that use the same LTR as reference.
                                                If LTR != 0, POC_LTR(n+1) - POC_LTR(n). POC_LTR is LTR's POC; the POC delta between two consecutive frames that encoded as the same LTR index.
                                     If this config file is not specified, default parameters will be used.
        --LTR=a:b:c[:d]            a:b:c[:d] long term reference setting
                                       a: POC_delta of two frames which are used as LTR.
                                       b: POC_Frame_Use_LTR(0) - POC_LTR. POC_LTR is LTR's POC, POC_Frame_Use_LTR(0) is the first frame after LTR that uses the LTR as reference.
                                       c: POC_Frame_Use_LTR(n+1) - POC_Frame_Use_LTR(n). The POC delta between two consecutive frames that use the same LTR as reference.
                                       d: QP delta for frame using LTR. [0]
        --gopLowdelay              Use default low delay GOP configuration if --gopConfig is not specified, only valid for gopSize <= 4. [0]
                                   0 = Disable gopLowdelay mode
                                   1 = Enable gopLowdelay mode
  -s[n] --picSkip                  0=OFF, 1=ON Picture skip rate control. [0]
                                   Allows rate control to skip frames if needed.
  -q[n] --qpHdr                    -1..51, Initial target QP. [26]
                                   -1 = Encoder calculates initial QP. NOTE: use -q-1
                                   The initial QP used in the beginning of stream.
  -n[n] --qpMin                    0..51, Minimum frame header QP for any slices. [0]
  -m[n] --qpMax                    0..51, Maximum frame header QP for any slices. [51]
        --qpMinI                   0..51, Minimum frame header QP, overriding qpMin for I slices. [0]
        --qpMaxI                   0..51, Maximum frame header QP, overriding qpMax for I slices. [51]
  -A[n] --intraQpDelta             -51..51, Intra QP delta. [-5]
                                   QP difference between target QP and intra frame QP.
  -G[n] --fixedIntraQp             0..51, Fixed Intra QP, 0 = disabled. [0]
                                   Use fixed QP value for every intra frame in stream.
  -V[n] --bFrameQpDelta            -1..51, B Frame QP Delta. [-1]
                                   QP difference between B Frame QP and target QP.
                                   If a GOP config file is specified by --gopConfig, it will be overridden.
                                   -1 not take effect, 0-51 could take effect.
  -I[n] --chromaQpOffset           -12..12 Chroma QP offset. [0]
        --vbr                      0=OFF, 1=ON. Variable Bitrate control by qpMin. [0]
        --sceneChange               Frame1:Frame2:..:Frame20. Specify scene change frames, seperated by ':'. Max number of scene change frames is 20.
        --gdrDuration              how many frames it will take to do GDR [0]
                                   0 : disable GDR (Gradual decoder refresh), >0: enable GDR
                                   The starting point of GDR is the frame with type set to VCENC_INTRA_FRAME.
                                   intraArea and roi1Area are used to implement the GDR function.
        --skipFramePOC             0..n Force encode whole frame as Skip Frame when POC=n. [0]
                                   0: Disable. 
                                   none zero: set the frame POC to be encoded as Skip Frame. 

 Parameters affecting coding:
  -z[s] --userData                 SEI User data file name. File is read and inserted
                                     as an SEI message before the first frame.
        --cir                      start:interval for Cyclic Intra Refresh.
                                   Forces CTBs in intra mode. [0:0]
        --intraArea                left:top:right:bottom CTB coordinates
                                       Specifies the rectangular area of CTBs to
                                       force encoding in intra mode.
        --ipcm1Area                left:top:right:bottom CTB coordinates
        --ipcm2Area                left:top:right:bottom CTB coordinates
                                       Specifies the rectangular area of CTBs to
                                       force encoding in IPCM mode.
        --ipcmMapEnable            Enable the IPCM Map. 0-disable, 1-enable. [0]
        --ipcmMapFile              User-specified IPCM map file, which defines the IPCM flag for each CTB in the frame.
                                   The block size is 64x64 for HEVC and 16x16 for H.264.
        --roi1Area                 left:top:right:bottom CTB coordinates
        --roi2Area                 left:top:right:bottom CTB coordinates
        --roi3Area                 left:top:right:bottom CTB coordinates
        --roi4Area                 left:top:right:bottom CTB coordinates
        --roi5Area                 left:top:right:bottom CTB coordinates
        --roi6Area                 left:top:right:bottom CTB coordinates
        --roi7Area                 left:top:right:bottom CTB coordinates
        --roi8Area                 left:top:right:bottom CTB coordinates
                                       Specifies the rectangular area of CTBs as
                                       Region Of Interest with lower QP.
        --roi1DeltaQp              -30..0 (-51..51 if absolute ROI QP supported), QP delta value for ROI 1 CTBs. [0]
        --roi2DeltaQp              -30..0 (-51..51 if absolute ROI QP supported), QP delta value for ROI 2 CTBs. [0]
        --roi3DeltaQp              -30..0 (-51..51 if absolute ROI QP supported), QP delta value for ROI 3 CTBs. [0]
        --roi4DeltaQp              -30..0 (-51..51 if absolute ROI QP supported), QP delta value for ROI 4 CTBs. [0]
        --roi5DeltaQp              -30..0 (-51..51 if absolute ROI QP supported), QP delta value for ROI 5 CTBs. [0]
        --roi6DeltaQp              -30..0 (-51..51 if absolute ROI QP supported), QP delta value for ROI 6 CTBs. [0]
        --roi7DeltaQp              -30..0 (-51..51 if absolute ROI QP supported), QP delta value for ROI 7 CTBs. [0]
        --roi8DeltaQp              -30..0 (-51..51 if absolute ROI QP supported), QP delta value for ROI 8 CTBs. [0]
        --roi1Qp                   0..51, absolute QP value for ROI 1 CTBs. [-1]. Negative value means invalid.,
                                     and another value is used to calculate the QP in the ROI area.
        --roi2Qp                   0..51, absolute QP value for ROI 2 CTBs. [-1]
        --roi3Qp                   0..51, absolute QP value for ROI 3 CTBs. [-1]
        --roi4Qp                   0..51, absolute QP value for ROI 4 CTBs. [-1]
        --roi5Qp                   0..51, absolute QP value for ROI 5 CTBs. [-1]
        --roi6Qp                   0..51, absolute QP value for ROI 6 CTBs. [-1]
        --roi7Qp                   0..51, absolute QP value for ROI 7 CTBs. [-1]
        --roi8Qp                   0..51, absolute QP value for ROI 8 CTBs. [-1]
                                   roi1Qp..roi8Qp are only valid when absolute ROI QP is supported. Use either roiDeltaQp or roiQp.
        --roiMapDeltaQpBlockUnit   Set the DeltaQp block size for ROI DeltaQp map file. 0-64x64,1-32x32,2-16x16,3-8x8. [0]
        --roiMapDeltaQpEnable      Enable the QP delta for ROI regions in the frame. 0-disable,1-enable. [0]
        --roiMapDeltaQpFile        User-specified DeltaQp map file, which defines the QP delta for each block in the frame.
                                   The block size is defined by --roiMapDeltaQpBlockUnit.
                                   The QP delta range is from -30 to 0 if absolute ROI QP is not supported.
                                   The QP delta range is from -51 to 51 if absolute ROI QP is supported.
                                   Absolute QP range is from 0 to 51 and specified with a prefix 'a', for example, 'a26'.
                                   To calculate block width and height, alignment of 64 for the picture width and height should be used.
        --roiMapInfoBinFile        User-specified ROI map info binary file, which defines the QP delta or absolute ROI QP for each block in the frame.
                                   The block size is defined by --roiMapDeltaQpBlockUnit, one byte per block.
                                   The byte bitmap of QpDelta/Skip/IPCM is related to --RoiQpDeltaVer. QP delta range is from -51 to 51.
                                   Absolute QP range is from 0 to 51.
        --RoiQpDeltaVer            1..3, ROI Qp Delta map version number, valid only if --roiMapInfoBinFile is present.
        --RoimapCuCtrlInfoBinFile  User-specified ROI map CU control info binary file, which defines the ROI CU control info for each CU in the frame.
                                   The CU control structure size is related to --RoiCuCtrlVer.
                                   The number of controlled CUs is aligned to 64 of picture width and height in 8x8 unit.
        --RoiCuCtrlVer             3..7, ROI map CU control version number, valid only if --RoimapCuCtrlInfoBinFile is present.

 Parameters setting Skip Map:
        --skipMapEnable            0..1 Enable Skip Map Mode. 0-Disable, 1-Enable. [0]
        --skipMapBlockUnit         Block size in Skip Map Mode. [0]
                                   0-64x64, 1-32x32, 2-16x16. Only 64x64 and 32x32 are valid for HEVC.
        --skipMapFile              User-specified Skip Map File, which defines the Skip forcing mode for each block in the frame.
                                   1 indicates Skip forcing mode for a block and 0 indicates not.
                                   To calculate block width and height, an alignment of 64 of picture width and height should be used.

 Parameters setting constant chroma:
        --enableConstChroma        0..1 Enable/Disable setting chroma to a constant pixel value. [0]
                                     0 = Disable. 
                                     1 = Enable. 
        --constCb                  0..255 for 8-bit [128]; 0..1023 for 10-bit [512]. The constant pixel value for Cb. 
        --constCr                  0..255 for 8-bit [128]; 0..1023 for 10-bit [512]. The constant pixel value for Cr. 

 Parameters affecting coding and performance:
        --preset                   0...4 for HEVC. 0..1 for H264. Trade off performance and compression efficiency
                                     Higher value means high quality but worse performance. User need explict claim preset when use this option
        --rdoLevel                 1..3 Programable hardware RDO Level [3]
                                     Lower value means lower quality but better performance.
                                     Higher value means higher quality but worse performance.
        --enableRdoQuant           0..1 Enable/Disable RDO Quantization.
                                     0 = Disable (Default if hardware does not support RDOQ).
                                     1 = Enable (Default if hardware supports RDOQ).

 Parameters affecting reporting:
        --enableOutputCuInfo       0..2 Enable/Disable writting CU encoding information to external memory [0]
                                     0 = Disable. 
                                     1 = Enable. 
                                     2 = Enable and also write information in file <cuInfo.txt>. 
        --hashtype                 hash type for frame data hash. [0]
                                     0=disable, 1=crc32, 2=checksum32. 
        --ssim                     0..1 Enable/Disable SSIM calculation [1]
                                   0 = Disable. 
                                   1 = Enable. 
        --enableVuiTimingInfo       Write VUI timing info in SPS. [1]
                                    0=disable. 
                                    1=enable. 

 Parameters affecting lookahead encoding:
        --lookaheadDepth            0, 4..40 The number of look-ahead frames. [0]
                                      0 = Disable 2-pass encoding.
                                      4-40 = Set the number of look-ahead frames and enable 2-pass encoding.
        --halfDsInput               External provided half-downsampled input YUV file.
        --aq_mode                   Mode for Adaptive Quantization - 0:none 1:uniform AQ 2:auto variance 3:auto variance with bias to dark scenes. Default 0
        --aq_strength               Reduces blocking and blurring in flat and textured areas (0 to 3.0). Default 1.00
        --tune                       0...2 Tune parameters for best psnr/ssim/subjective quality. [0]
                                       0 = best psnr score: disable aq-mode/psy-rd. 
                                       1 = best ssim score: enable aq-mode, disable psy-rd. 
                                       2 = best subjective quality: enable aq-mode/psy-rd. 

 Parameters affecting Reference Frame Compressor:
        --compressor               0..3 Enable/Disable Embedded Compression [0]
                                     0 = Disable compression
                                     1 = Only enable luma compression
                                     2 = Only enable chroma compression
                                     3 = Enable both luma and chroma compression
        --enableP010Ref            0..1 Enable/Disable P010 reference format [0]
                                     0 = Disable. 
                                     1 = Enable. 

 Parameters affecting low latency input:
        --inputLineBufferMode 0..4 Input buffer mode control. [0]
                                 0 = Disable input line buffer.
                                 1 = Enable. SW handshaking. Loop-back enabled.
                                 2 = Enable. HW handshaking. Loop-back enabled.
                                 3 = Enable. SW handshaking. Loop-back disabled.
                                 4 = Enable. HW handshaking. Loop-back disabled.
        --inputLineBufferDepth 0..511. The number of CTB/MB rows to control loop-back/handshaking. [1]
                                 Control loop-back mode if it is enabled:
                                   There are two continuous ping-pong input buffers; each contains inputLineBufferDepth CTB/MB rows.
                                 Control HW handshaking if it is enabled:
                                   Handshaking signal is processed per inputLineBufferDepth CTB/MB rows.
                                 Control SW handshaking if it is enabled:
                                   IRQ is sent and Read Count Register is updated every time inputLineBufferDepth CTB/MB rows have been read.
                                 0 is only allowed with inputLineBufferMode=3, IRQ won't be sent and Read Count Register won't be updated.
        --inputLineBufferAmountPerLoopback 0..1023. Handshake sync amount for every loop-back. [0]
                                 0 = Disable input line buffer. 
                                 1~1023 = The number of slices per loop-back 

 Parameters affecting stream multi-segment output:
        --streamMultiSegmentMode 0..2 Stream multi-segment mode control. [0]
                                   0 = Disable stream multi-segment mode. 
                                   1 = Enable stream multi-segment mode. No SW handshaking. Loop-back is enabled.
                                   2 = Enable stream multi-segment mode. SW handshaking. Loop-back is enabled.
        --streamMultiSegmentAmount 2..16. The total amount of segments to control loop-back/SW handshaking/IRQ. [4]

 Parameters affecting noise reduction:
        --noiseReductionEnable     Enable/disable noise reduction (NR). [0]
                                   0 = Disable NR.
                                   1 = Enable NR.
        --noiseLow                 1..30 minimum noise value [10]
        --noiseFirstFrameSigma     1..30 noise estimation for start frames [11]

 Parameters affecting smart background detection:
        --smartConfig              Usr configuration file for the Smart Algorithm. 

 Parameters affecting motion estimation and global motion:
        --gmvFile                  File containing ME Search Range Offset for list0.
                                     Search Offsets of each frame are listed sequentially line by line.
                                     To set frame-level offset, there should be only one coordinate per line for the whole frame.
                                     For example: (MVX, MVY)
        --gmv                      MVX:MVY. Horizontal and vertical offsets of ME Search Range for list0 at frame level. [0:0]
                                     If both --gmvFile and --gmv are specified, only gmvFile will be applied.
                                     MVX should be 64-aligned and within the range of [-128, +128].
                                     MVY should be 16-aligned and within the range of [-128, +128].
        --gmvList1                 MVX:MVY. ME Search Range Offset for list1 at frame level. [0:0]
        --gmvList1File             File containing ME Search Range Offset for list1.
        --MEVertRange              ME vertical search range. Only valid if the function is supported in this version. [0]
                                   Should be 24 or 48 for H.264; 40 or 64 for HEVC/AV1.
                                   0 - The maximum vertical search range of this version will be used.

 Parameters affecting runtime log level:
        --verbose                  0..1 Log printing mode [0]
                                     0: Print brief information.
                                     1: Print more detailed information.

 Parameters dump registers to sw_reg.trc:
        --dumpRegister             0..1 dump register enable [0]
                                   0: no register dump.
                                   1: print register dump.

 Raster scan output for recon on FPGA & HW:
        --rasterscan               0..1 raster scan enable [0]
                                   0: disable raster scan output.
                                   1: enable raster scan output.

 enable/disable recon write to DDR if it's pure I-frame encoding:
        --writeReconToDDR       0..1 recon write to DDR enable [1]
                                   0: disable recon write to DDR.
                                   1: enable recon write to DDR.

 Parameters affecting HDR10: 
        --HDR10_display=dx0:dy0:dx1:dy1:dx2:dy2:wx:wy:max:min    Mastering display color volume SEI message
                                   dx0 : 0...50000 Component 0 normalized x chromaticity coordinates [0]
                                   dy0 : 0...50000 Component 0 normalized y chromaticity coordinates [0]
                                   dx1 : 0...50000 Component 1 normalized x chromaticity coordinates [0]
                                   dy1 : 0...50000 Component 1 normalized y chromaticity coordinates [0]
                                   dx2 : 0...50000 Component 2 normalized x chromaticity coordinates [0]
                                   dy2 : 0...50000 Component 2 normalized y chromaticity coordinates [0]
                                   wx  : 0...50000 White point normalized x chromaticity coordinates [0]
                                   wy  : 0...50000 White point normalized y chromaticity coordinates [0]
                                   max : Nominal maximum display luminance [0]
                                   min : Nominal minimum display luminance [0]
        --HDR10_lightlevel=maxlevel:avglevel    Content light level info SEI message
                                   maxlevel : max content light level
                                   avglevel : max picture average light level
        --HDR10_colordescription=primary:transfer:matrix    Color description
                                   primary : 0..9 Index of chromaticity coordinates in Table E.3 in HEVC spec [9]
                                   transfer : 0..2 The reference opto-electronic transfer characteristic 
                                              function of the source picture in Table E.4 in HEVC spec [0]
                                              0 = ITU-R BT.2020, 1 = SMPTE ST 2084, 2 = ARIB STD-B67
                                   matrix : 0..9 Index of matrix coefficients used in deriving luma and chroma signals 
                                            from the green, blue, and red or Y, Z, and X primaries in Table E.5 in HEVC spec [9]

 Parameters for external SRAM:
  --extSramLumHeightBwd            0=no external SRAM, 1..16=The number of line count is 4*extSramLumHeightBwd. [hevc:16,h264:12]
  --extSramChrHeightBwd            0=no external SRAM, 1..16=The number of line count is 4*extSramChrHeightBwd. [hevc:8,h264:6]
  --extSramLumHeightFwd            0=no external SRAM, 1..16=The number of line count is 4*extSramLumHeightFwd. [hevc:16,h264:12]
  --extSramChrHeightFwd            0=no external SRAM, 1..16=The number of line count is 4*extSramChrHeightFwd. [hevc:8,h264:6]

 Parameters for MMU control:
  --mmuEnable                      0=disable MMU if MMU exists, 1=enable MMU if MMU exists. [0]

 Parameters for DEC400 compressed table(tile status):
  --dec400TableInput               Read input DEC400 compressed table from file. [dec400CompTableinput.bin]

 Parameters for AXI alignment:
  --AXIAlignment                   AXI alignment setting (in hexadecimal format). [0]
                                     bit[31:28] AXI_burst_align_wr_common
                                     bit[27:24] AXI_burst_align_wr_stream
                                     bit[23:20] AXI_burst_align_wr_chroma_ref
                                     bit[19:16] AXI_burst_align_wr_luma_ref
                                     bit[15:12] AXI_burst_align_rd_common
                                     bit[11: 8] AXI_burst_align_rd_prp
                                     bit[ 7: 4] AXI_burst_align_rd_ch_ref_prefetch
                                     bit[ 3: 0] AXI_burst_align_rd_lu_ref_prefetch

 Parameters for AV1 TX type search:
  --TxTypeSearchEnable             0=Tx type search disable, 1=Tx type search enable. [0]

 Temporary testing parameters for internal use:
  --parallelCoreNum                1..4 The number of cores running in parallel at frame level. [1]
  --smoothingIntra                 0..1 Enable or disable the strong_intra_smoothing_enabled_flag (HEVC only). 0=Normal, 1=Strong. [1]
  --testId                         Internal test ID. [0]
  --roiMapDeltaQpBinFile           User-specified DeltaQp map binary file, only valid when lookaheadDepth > 0.
                                   Every byte stands for a block unit deltaQp in raster-scan order.
                                   The block unit size is defined by --roiMapDeltaQpBlockUnit (0-64x64,1-32x32,2-16x16,3-8x8).
                                   Frame width and height are aligned to block unit size when setting deltaQp per block.
                                   Frame N data is followed by Frame N+1 data immediately in display order.
  --RoimapCuCtrlIndexBinFile       User-specified ROI map CU control index binary file, which defines where the ROI info is included in the file --RoimapCuCtrlInfoBinFile.
                                     If --RoimapCuCtrlIndexBinFile is not specified, the ROI info about CUs in each CTB should be included in the file --RoimapCuCtrlInfoBinFile.
                                     If --RoimapCuCtrlIndexBinFile is specified, the ROI info about CUs in each CTB should be included in the file --RoimapCuCtrlIndexBinFile.


 Temporary testing multiple encoder instances in multi-thread mode or multi-process mode:
    --multimode                   Specify encoders running in parallel in multi-thread or multi-process mode. [0]
                                    0: disable
                                    1: multi-thread mode
                                    2: multi-process mode
    --streamcfg                   Specify the filename storing encoder options


 Parameters for OSD overlay controls (i should be a number from 1 to 8):
    --overlayEnables              8 bits indicate enable for 8 overlay region. [0]
                                    1: region 1 enabled
                                    2: region 2 enabled
                                    3: region 1 and 2 enabled
                                    and so on.
    --olInputi                    input file for overlay region 1-8. [olInputi.yuv]
                                    for example --olInput1    --olFormati                   0..2 Specify the overlay input format. [0]
                                    0: ARGB8888
                                    1: NV12
                                    2: Bitmap
    --olAlphai                    0..255 Specify a global alpha value for NV12 and Bitmap overlay format. [0]
    --olWidthi                    Width of overlay region. Must be set if region enabled. [0]
                                    Must be under 8 aligned for bitmap format. 
    --olHeighti                   Height of overlay region. Must be set if region enabled. [0]
    --olXoffseti                  Horizontal offset of overlay region top left pixel. [0]
                                    must be under 2 aligned condition. [0]
    --olYoffseti                  Vertical offset of overlay region top left pixel. [0]
                                    must be under 2 aligned condition. [0]
    --olYStridei                  Luma stride in bytes. Default value is based on format.
                                    [olWidthi * 4] if ARGB8888.
                                    [olWidthi] if NV12.
                                    [olWidthi / 8] if Bitmap.
    --olUVStridei                 Chroma stride in bytes. Default value is based on luma stride.
    --olCropXoffseti              OSD cropping top left horizontal offset. [0]
                                    must be under 2 aligned condition.
                                    for bitmap format, must be under 8 aligned condition.
    --olCropYoffseti              OSD cropping top left vertical offset. [0]
                                    must be under 2 aligned condition.
                                    must be under 8 aligned condition for bitmap format.
    --olCropWidthi                OSD cropping width. [olWidthi]
                                    for bitmap format, must be under 8 aligned condition.
    --olCropHeighti               OSD cropping height. [olHeighti]
    --olBitmapYi                  OSD bitmap format Y value. [0]
    --olBitmapUi                  OSD bitmap format U value. [0]
    --olBitmapVi                  OSD bitmap format V value. [0]

``````bash
