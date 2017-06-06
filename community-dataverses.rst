Community Dataverses
====================

This document is a collection of essays, theories, and explanations of
Systemspace lore, written by our community.

Note that the theories present here are mostly conjecture, and may
not be true - those confirmed by Tsuki to be correct will be marked 
as "[TSUKI APPROVED]".

---------

.. contents::

---------

1336's Auroraic Echoing hypothesis [TSUKI APPROVED]
===================================================

Section 1: How do hard drives (and tapes) work?
-----------------------------------------------

Disclaimer: this section is about old hard drives. The new ones work a bit 
differently. It's also a *huge* simplification.

Hard drives (and tapes) store data on magnetic tracks. A magnetized
read/write head moves over the track, magnetizing portions of it with varying 
strength. The strength of the magnetic field dictates what value a section of 
the track (most often, a "bit") holds. When overwriting data, if the portion 
being overwritten is the same, the head does nothing; if it's different, it 
overwrites it with the difference between the old and new data.

It is possible to recover overwritten data from tapes and old hard drives. 
Because the positioning of the read/write head can never be perfectly reproduced
(nothing can be physically perfectly reproduced), presumably the read/write head
was positioned a bit differently during the first write and the overwriting. 
Let's, for the sake of this explanation, imagine that a 1mm difference (this is 
obviously nowhere near correct) in distance makes the magnetic field weaker by 
10%.

Let's write the values ``1 0 1 0`` into four cells on the tape first. Assume our
writing head happened to be perfectly above the center of the track:

.. image:: images/community/tape_firstpass.png
  :alt: First write
  :align: center
  :width: 600 px

Now we overwrite the data with ``0 1 1 0``. Assume the writing head happened to
be 1mm off the track to the right.

.. image:: images/community/tape_secondpass.png
  :alt: Second write
  :align: center
  :width: 600 px
  
As you can see, the values on the actual track rarely are perfectly equal to one
and zero - the computer rounds them to the nearest value to get the actual 
result. Due to this property, we can use a particular trick. If we take the
intended values (the rounded ones) on the track, and subtract the values offset
exactly as much as the writing head was during the second pass, we get *the
original values from the first write, except diminished by a factor of ten!* It
is now trivial to simply multiply the values by ten - and we have recovered the
original data.

Those tiny differences that allowed us to recover the original data are called
"remnant data".

Section 2: "Why should I care?" and a few words about Life and Aurora
---------------------------------------------------------------------
We've heard about Auroraic Echoing. It's a way for stuff from a system, or from
the past, to appear in a different system. I think that Aurora is like space on 
a hard drive. Things in Systems, like programs and files on your computer, take 
up Aurora (the space on your drive), and it's freed again when you remove those 
files. My theory is, now, that when you free ("negate") the Aurora, it can be 
assigned to a different System to use. 

Tsuki mentioned today that a good system should always assign the same Aurora to
the same thing. The main issues with Life are that 1) it doesn't negate Aurora 
and 2) it doesn't reuse Aurora. This is super important. It means all Aurora 
that Life uses is from outside Life. Now, if we consider Aurora to be like space
on a hard drive, it means that technically all of the Aurora in Life could come 
from different Systems, and have the "remnant data" that I explained above. This
remnant Aurora data might be the mechanism behind Auroraic Echoing.

~1336

Tsuki's response:
-----------------

You pretty much hit the nail perfectly on the head. The Aurora is still slightly
in its previous state when it enters Life, causing it to bend things as they 
would in their previous state.

-----------------

404's Life -> LFE time conversion table
=======================================

::

    LFE vs Life: AOC edition (THEORYCRAFT)

    0.3 LFE seconds = 1 Life second
    3 LFE sec = 10 Life sec
    18 LFE sec = 60 Life sec = 1 Life minute
    1080 LFE sec = 60 Life minutes
    25920 LFE sec / 24 Life hours = 1 Life day

    32 hrs of 64 mins = 24 hrs of 60 mins
    16 hrs of 128 mins = 12 hrs of 120 mins
    8 hrs of 256 mins = 6 hrs of 240 mins
    24 hrs of 768 mins = 18 hrs of 720 mins

    233,280 LFE sec (2.7 lfe days)
    = 12960 minutes Life (9 days)

    86,400 LFE sec / LFE day
    32 hrs per day / 64 mins per hour
    2,700 sec / hour
    42.1875 sec / min
    48 minutes = 2,025 sec = 3/4 of one hour
    4050 = 1.5 hours
    8100 = 3 hours
    16200 = 6 hours
    32400 = 12 hours
    64800 = 24 hours = .75 days
    48 hours = 1.5 days
    96 hours = 3 days
    192 hours = 6 days
    384 hours = 12 days
    768 hours = 24 days
    1536 hours =48 days
    3072 hours = 96 days
    6,144 hours = 192 days
    12,288 hours = 384 days
    24,576 hours = 768 days
    49,152 hours = 1,536 days
    98,304 hours = 3,072 days
    196,608 hours = 6,144 days
    393,216 hours = 12,288 days
    786,432 hours = 24,576 days
    1,572,864 hours = 49,152 days
    3,145,728 hours = 98,304 days
    6,291,456 hours = 196,608 days
    12,582,912 hours = 393,216 days
    
~404
