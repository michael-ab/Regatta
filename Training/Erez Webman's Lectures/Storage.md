[Erez Webman - Storage](https://drive.google.com/drive/u/0/folders/1_eb0M7Y_xXKfNtyqiV6ZYmFM_OXIv86z "https://drive.google.com/drive/u/0/folders/1_eb0M7Y_xXKfNtyqiV6ZYmFM_OXIv86z") (Watch this even if you know storage as the videos touch Regatta related material)

File system
Block Volume
Block Device
![[Erez - Intro and block device]]

LSA -> Log Structured Array
Log Structured File System
L2P (L-to-P) (Call also R2P row to physical) -> Logical to physical

![[LSA]]


> [!NOTE] 
> Implementation of R2P is B-Tree at Regatta
> See in confluence why we don't using a Hash Table https://rdbproject.atlassian.net/wiki/spaces/RDBRD/pages/1061814291 


> [!NOTE] Segment
> R2P is per segment at Regatta
> Each segment as is own R2P and LSA
> Segment have a size between 1 GB to 10 GB
> Catalog map tables to segments
