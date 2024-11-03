# Ballot Interpretation

Ballot interpretation begins with an image of the ballot transmitted from the scanner. Once the image is available to the application, it starts by trying to interpreting the ballot as a [hand marked ballot](hand-marked-ballots.md).

Before trying to make sense of the ballot, the interpreter checks the image for vertical streaks. Vertical streaks likely indicate some sort of smudge or debris in the scanner that could interfere with the ballot image. The interpreter looks for columns of black without gaps, excluding the edges of the ballot which may be black simply from the way the scanner creates images.

<div>

<figure><img src="../.gitbook/assets/c357279b-5d32-41e0-a158-6127932f9bc3-back_debug_vertical_streaks.png" alt=""><figcaption><p>Vertical streak detected</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/9242ad5e-82ff-4bd3-9c97-9e16ab51b517-front_debug_vertical_streaks.png" alt=""><figcaption><p>No vertical streak detected</p></figcaption></figure>

</div>

If a streak is detected, the interpreter exits and surfacse the error to the application which will alert the user.

The interpreter then identifies the timing mark grid. It begins by finding all shapes in the image. It then narrows the list of shapes down to ones that look like timing marks and then further narrows the list down to timing mark shapes that fall along the edges of the image in a line.

<div>

<figure><img src="../.gitbook/assets/9242ad5e-82ff-4bd3-9c97-9e16ab51b517-front_debug_contours.png" alt=""><figcaption><p>All shapes</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/9242ad5e-82ff-4bd3-9c97-9e16ab51b517-front_debug_candidate_timing_marks.png" alt=""><figcaption><p>Timing mark shapes</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/9242ad5e-82ff-4bd3-9c97-9e16ab51b517-front_debug_partial_timing_marks.png" alt=""><figcaption><p>Timing mark shapes along edges</p></figcaption></figure>

</div>

As in the example above, the interpreter might not have found all timing marks at this point. It infers any missing timing marks and identifies the corners in order to construct a complete timing mark grid. If at any point the interpreter does not have enough information to comfortably find the complete mark grid or if the detected grid is too rotated or skewed, it exits which causes the application to reject the ballot.

<div>

<figure><img src="../.gitbook/assets/9242ad5e-82ff-4bd3-9c97-9e16ab51b517-front_debug_corner_match_info.png" alt=""><figcaption><p>Identified corners</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/9242ad5e-82ff-4bd3-9c97-9e16ab51b517-front_debug_complete_timing_marks.png" alt=""><figcaption><p>Identified timing marks</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/9242ad5e-82ff-4bd3-9c97-9e16ab51b517-front_debug_timing_mark_grid.png" alt=""><figcaption><p>Timing mark grid</p></figcaption></figure>

</div>

Next the interpreter will search the bottom left and top right corners of the image for a QR code.&#x20;

* search for QR code
* normalize orientation
* check mismatches on front and back
* score bubbles
* build interpreted page layout
* score write in areas



* attempt BMD interpretation - search for QR code in entire sheet
* save sheet
