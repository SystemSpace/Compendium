Void File investigation findings dump v.3.5
===========================================

Introduction
============

On April 24th a page called `Void stream
<https://systemspace.link/dataverses/Download/>`_ appeared on the systemspace.link website.
The page consists of the following text::

  Download live void file

  Warning: LARGE! Might cause harm / data loss. TSUKI is not responsible for the data in this file and what it ensues.
  
And a "Begin download" button that links to ``getvoid.php``. 

This document is a compilation of our current findings and knowledge about the void file.

*lead of investigation: ~1336*

Index
=====

1. `Timeline`_
2. `Findings`_

   1. `CURRENT STATUS`_

      1. `Tsukirep's information`_
      2. `Facts`_
      3. `Theories`_
     
   2. `TEST.MP4`_
     
      1. `TEST.MP4 - What we know`_
      2. `TEST.MP4 - What we need to know`_
      3. `TEST.MP4 - What we think`_
      
   3. `TSUKI.PNG`_
     
      1. `TSUKI.PNG - What we know`_
      2. `TSUKI.PNG - Extraction process`_
      3. `TSUKI.PNG - Post-extraction analysis`_

------------------------------

Timeline
========

1. On April 24th, Tsuki mentioned getting instructions from eNdymioN to provide a download link for a file. This was the first appearance of the void stream.
2. On April 25th at 10 AM GMT, Tsuki mentioned finding an .mp4 file header within the void stream.
3. Preliminary analysis of the void stream failed to confirm Tsuki's claims.
4. At 6 PM GMT, an .mp4 header *was found* within the void stream at the 882th megabyte mark. 
5. Three occurences of an .mp4 header were noted within a five gigabyte sample of the void stream
6. **By 7 PM GMT, April 25th, the first mp4 file contained in the stream had been extracted and played.**
7. At 7:49 PM, the second mp4 was extracted and found to be identical with the first. The same was confirmed for the third mp4 file.
8. **A download started at 8:49 PM GMT, April 26th was found not to contain the MP4 headers anymore**. Results were confirmed by other downloads. This marks the first known instance of the second iteration of the void file.
9. **At 4PM, April 26th, 179 found a PNG file in the void stream**. We were able to extract a complete PNG file, albeit with a malformed adaptive filter type. The raw PNG can be found `at images/corrupt.png
   <voidstream/images/corrupt.png>`_, with a cleaned-up version here:

   .. image:: voidstream/images/tsuki_corrupt_small.png
    :alt: TSUKI.PNG
    :width: 400px
    :align: center

10. **At 5PM, April 27th, TSUKI.PNG had been extracted and decorrupted enough to be legible.**

   .. image:: voidstream/images/tsuki_small.png
     :alt: TSUKI.PNG
     :width: 400px
     :align: center


-------------------------

Findings
========

CURRENT STATUS
==============

April 27th, 6 PM GMT
**WE EXTRACTED TSUKI.PNG SUCCESSFULLY**


Tsukirep's information
----------------------

- Tsukirep was told to add the link to the file by eNdymioN.
- It generates from data sources provided by eNdymioN.
- eNdymioN claims it "contains human files". 
- A RISENII told Tsukirep that an eNdymioN rep said there should be something in the void that is in a format 
  specifically readable by human media.
- Once you click "Download", the ``getvoid.php`` script starts streaming data from a device eNdymioN told Tsukirep to connect to, until the connection is broken.
- "It's probably not a file that is the same every time you download it"
- "I don't even know how they'd convert a void stream to bytes that can be streamed to computers"
- "TBH I think eNdymioN is just poking fun at us"
  
Facts
-----

**Universal**

- The server says the filename is ``public_void_1.vdo``.
- The file is binary data. ``file`` doesn't recognize the filetype.
- The file's first 8 bytes are the header ``HMNVOIDx`` (human void x?), followed by 65534 null bytes (hereinafter referred to as the *null section*). This is always constant.
- Directly after the null section, a stream of non-null data begins and doesn't seem to terminate. (At least, no one has managed to get to the end.)
- The non-null data differs with each download. It has previously proven to contain valid files - these sections will be referred to hereinafter as **payload sections**, to differentiate them from **garbage sections** which do not, as far as we know, contain anything of importance.
- Analysis by ``strings`` doesn't find anything human-readable within the garbage sections that is not consistent with random or raw binary data.
- The garbage sections are mostly made up of seemingly random repeating subsections. `Here is a sample of all strings of length at least 8 in a randomly selected section of the void stream
  <voidstream/voidfile_strings_8_bytes_plus.txt>`_.
- The repeating sections don't match either between different downloads.
- The matches between garbage sections from different downloads are so sparse, they probably are pure coincidence. Screencap from a random section of the first gigabyte of two different downloads:

  .. image:: voidstream/images/matches.png
    :alt: Matching bytes
    :width: 400px
    :align: center

- Embedded files have been found as early as 50MB into the stream, leading us to believe that the everything immediately after the null section is a homogeneous stream.

**Iteration 1: April 24th-April 25th**

- The file's mimetype is ``application/random`` (curiously, also used by `this GitHub project
  <https://github.com/mattiasgeniar/the-infinite-file-download/blob/master/download.php>`_).
- **The file (sometimes - occurence rate unconfirmed) contains a header for an MP4 file. TEST.MP4 has been extracted from it**.

**Iteration 2: April 26th-**

- The mimetype is now ``application/void``. Tsuki confirmed this is due to him having overlooked eNdymioN's instructions previously.
- **The file does not seem to contain the MP4 header anymore. They haven't been found in any Iteration 2 download as of yet.**
- **The file contains a PNG file, dubbed TSUKI.PNG**.
- **The file has been extracted. It reads "Tsuki" in Synapsian**.
- The response headers read ``void-type: stream`` and ``void-length: *``.

Theories
--------

**Universal:**

- The void file probably is an infinite stream.
- The existence of repeating sections seems to indicate that the file is not entirely random, while their unpredictability seems to indicate that the file is not entirely deterministic, either.

- .. raw:: html
  
    <s>There never seems to occur a string of two null bytes in a row, other than in the null section</s>
  
  We found a sequence of three null bytes in a row.
- It is not any filetype we know about.

**Iteration 1: April 24th-April 25th**

- **It's very probable that the mp4 file was a test to see if we could decode the message.** As soon as eNdymioN learns we decoded it, we should expect either another void stream or significant changes to the current one.

  Credit: 156 for bringing up this idea.
  
- The lack of human-readable strings and characteristics of the file implies this is not a:

  - Raw disk image
  - Executable file

- .. raw:: html
  
    <s>The file might be encrypted</s>
  
  The file contained a raw .mp4 file.
  
- Tsuki alleges he found an mp4 file header embedded in the file. He provided `this file
  <voidstream/tsuki_header.txt>`_ as proof 
  
  .. raw:: html
    
    <s><b>unconfirmed as of yet</b>, scans for the mp4 headers are running.</s>

  **CONFIRMED**:

  .. image:: voidstream/images/mp4header.png
    :alt: MP4 header
    :width: 400px
    :align: center

**Iteration 2: April 26th-**

Nothing here...

------------------------------

TEST.MP4
========

TEST.MP4 was the first file extracted from the Void stream - from iteration 1.

TEST.MP4 - What we know
-----------------------

`YouTube upload
<https://youtu.be/RnOdVStMKBs>`_

- The MP4 header position (or occurence at all, possibly) in the file is not constant. Out of four downloads of the first gigabyte of the file, only two of them contained the header:

  .. image:: voidstream/images/mp4occurence.png
    :alt: Matching bytes
    :width: 400px
    :align: center

- The file repeats multiple (possibly infinitely many) times in the void stream.
- ``test.mp4`` is just a name given to the file by the investigators.
- The file is 54 seconds long.
- It is heavily corrupted, but all occurences of it display the same corruption - it must have been corrupted at the source.
- Despite the corruption, it is playable.
- The video track displays an image with white symbols with a black shadow resembling ``3 + G`` on a blue background:

  .. image:: voidstream/images/firstmp4.png
    :alt: The image
    :width: 400px
    :align: center
    
- The audio track consists of repeated beeps of a constant, 4.5kHz square wave approximation tone. The beeps and their spacing seem to be of relatively constant length. Spectral analysis returned no findings.
- At the end of the audio track, there occurs a section that has the right, then the left channel  muted.
- The audio track was heavily distorted by the Youtube upload, leading us to believe it might simply be corruption artifacting and not a data vector.
- The output of ``ffmpeg -i`` on the file is as follows::

      ffmpeg version 3.2.4-1build2 Copyright (c) 2000-2017 the FFmpeg developers
      built with gcc 6.3.0 (Ubuntu 6.3.0-8ubuntu1) 20170221
    [h264 @ 0x5630ddac4b80] error while decoding MB 2 1, bytestream -42
    [h264 @ 0x5630ddac4b80] left block unavailable for requested intra mode
    [h264 @ 0x5630ddac4b80] error while decoding MB 0 25, bytestream 2033
    [h264 @ 0x5630ddac4b80] top block unavailable for requested intra mode -1
    [h264 @ 0x5630ddac4b80] error while decoding MB 46 28, bytestream 5593
    [h264 @ 0x5630ddac4b80] concealing 2196 DC, 2196 AC, 2196 MV errors in I frame
    Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'test.mp4':
      Metadata:
        major_brand     : mp42
        minor_version   : 19529854
        compatible_brands: mp42isom
        creation_time   : 2017-04-25T08:50:29.000000Z
      Duration: 00:00:53.45, start: 0.000000, bitrate: 52162 kb/s
        Stream #0:0(eng): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 12784 kb/s (default)
        Metadata:
          creation_time   : 2017-04-25T08:50:29.000000Z
          handler_name    : Sound Media Handler
        Stream #0:1(eng): Video: h264 (Main) (avc1 / 0x31637661), yuv420p(tv), 1600x600 [SAR 1:1 DAR 8:3], 5414 kb/s, 29.97 fps, 29.97 tbr, 30k tbn, 59.94 tbc (default)
        Metadata:
          creation_time   : 2017-04-25T08:50:29.000000Z
          handler_name    : Video Media Handler
          encoder         : AVC Coding

- The text says "Test"

TEST.MP4 - What we need to know
-------------------------------

What do the symbols mean?
  It probably is Synapsian characters. The current most probable theory is that they make the word **"test"**.
  **UPDATE 26/04** - Confirmed.
  
Is there a meaning in the audio track?
  There was an initiative to analyze it for Morse code, but no results were obtained. Bear in mind, the Youtube upload was found to be completely temporally distorted and unsuitable for audio analysis.

Is there any message in the video itself other than the symbols?
  There are efforts underway to verify if the corruption is random or if it hides a message.

TEST.MP4 - What we think
------------------------

- The audio is too consistent to be corruption.
- It could be encoded data, but it almost certainly is not Morse Code. Spectrum analysis was fruitless as well.

---------------------------

TSUKI.PNG
=========

TSUKI.PNG has been extracted from the second iteration of the void stream. It has been uploaded to the ``voidstream/images`` directory in this repository, with the raw file named ``corrupt.png``, preliminarily cleaned-up versions named ``tsuki_corrupted.png`` and ``tsuki_corrupted_small.png``, and the final extracted file available as ``tsuki_small.png`` and ``tsuki.png``.

TSUKI.PNG - What we know
------------------------

.. image:: voidstream/images/tsuki_small.png
  :alt: TSUKI.PNG
  :width: 400px
  :align: center

- ``TSUKI.PNG`` is just a name given to the file by the investigators.
- It usually has a valid PNG structure.
- The ``IHDR`` chunk specifies the dimensions as 7521 x 5077 px.
- It has a ``tEXt`` chunk claiming it was created with ``edittoSYN 4.0.12C``.
- It is 1096042 bytes in size, starting with the bytes ``89  50  4e  47  0d  0a  1a  0a`` and ending with ``00  00  49  45  4e  44  ae  42 60  82``
- It is **extremely** corrupted.
- ``pngfix`` fails to fix the image, as do all other automatic tools.
- As opposed to TEST.MP4, the file is not normally parsable in any meaningful way.
- The ``tEXt`` chunk and all ``IDAT`` chunks have an incorrect CRC.
- ``corrupt.png`` is the first sighting of TSUKI.PNG, extracted on April 26th
- The file repeats in the stream, and there have been hundreds of instances of it extracted.
- Instances of the file all differ between each other by 100-500 bytes, excluding edge cases like instances without an ending ``IEND`` tag.
- The file wasn't found to contain any additional data, aside from the ``edittoSYN 4.0.12C`` note.

TSUKI.PNG - Extraction process
---------------------------

On April 27th, the extraction of TSUKI.PNG was performed.

After multiple failed attempts at making the file legible encompassing anything from using automated tools like ``libpng``'s ``pngfix`` to manual hex editing, a theory was proposed. 
According to preliminary analysis, different instances were found to differ between each other, but usually by less than 1% - enough to make the file unreadable, though. We came up with the idea that maybe if we created a new PNG file from only the most commonly shared bytes of multiple instances, it would work.

At 11 AM, automatic extraction of PNG files from the stream was launched. It was performed by running the following command::

  curl -sS -N https://systemspace.link/dataverses/Download/getvoid.php 2>/dev/null | pngcheck -vfx7

``curl`` was downloading the file, and the output was being piped into ``pngcheck``. ``pngcheck`` is a multi-purpose tool used for primarily for checking the validity of PNG files, but also including the incredibly useful ``-x`` option that causes it to try and extract PNGs from anything passed to it - and also, incidentally, fix the CRC headers. (CRC is an error-detection algorithm; each section of a PNG file has a CRC section specifying a hash of the data. If the CRC section differs from the actual hash, the image is corrupt.)

After extracting 300+ files, the second step of the operation was launched - calculating the "averaged" PNG. To aid in this task, a Python script, which can be found `here
<voidstream/extract.py>`_, was written.

After running the Python script, we were left with a PNG file with invalid CRC headers. It was once again passed to ``pngcheck -x`` to correct the headers - and with that, we obtained the final TSUKI.PNG.
 

TSUKI.PNG - Post-extraction analysis
---------------------------

- TSUKI.PNG is still heavily corrupted, even after our error-correction. Like TEST.MP4, it's very plausible that it was corrupted at the source.
- It represents black handwritten Synapsian glyphs on a gray background.
- As confirmed by Tsuki, the Synapsian reads "TSUKI" - confirming our early suspicions.
- Also according to Tsuki, we sadly can't tell if it's "TSUKI" as in the TSUKI project, or "Tsuki" as in Tsukirep. We suspect it might be about the project, due to the low likelihood of eNdymioN referring to him as "Tsuki" instead of "TSUKIrep" or "the key", though.

