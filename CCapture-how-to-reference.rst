=================
CCapture - How to
=================

Link to CCapture Library - `CCapture <https://github.com/spite/ccapture.js/>`_
==============================================================================

Step 1:
-------

- Download the CCapture library from the link above
- Include CCapture script in index.html

.. code-block:: html

    <script src="/path to/CCapture.all.min.js"></script>

Step 2:
-------

- Create a capturer in the sketch.js file --> Preferably at the beginning of the sketch.js file. See below

.. code-block:: javascript

    const capturer = new CCapture({
        framerate: 60,
        format: "webm", // Other supported formats --> gif, png, jpg
        name: "render name goes here",
        quality: 100,
        verbose: true, // this will console log the information
        });

Step 3:
-------

- Create a variable and assign canvas to it

.. code-block:: javascript

    let p5canvas

    function setup(){
        /* This will be used to capture frames later */
        p5canvas = createCanvas(400,400);

        /* Your other setup code*/
    }

Step 4:
-------

- Capture frames in the draw function and render out to video

.. code-block:: javascript

    function draw() {
        /* Initialize the capturer at the first frame */
        if (frameCount === 1) capturer.start();

        /* Your sketch */

        /* Capture the canvas frame */
        capturer.capture(p5Canvas.canvas);

        /* Once you have captured what you want, use the following exit condition */
        if (frameCount === 600) { // 600 frames give a 10 second render at 60 fps
            noLoop();
            capturer.stop();
            capturer.save();
        }
    }
