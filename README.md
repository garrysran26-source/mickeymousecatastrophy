
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Mai Websait</title>

  <style>
    * {
      box-sizing: border-box;
    }

    html, body {
      margin: 0;
      width: 100%;
      height: 100%;
      overflow: hidden;
      background: white;
      font-family: Arial, Helvetica, sans-serif;
    }

    /* Welcome message */
    #welcome {
      position: fixed;
      inset: 0;
      z-index: 100;
      display: flex;
      align-items: center;
      justify-content: center;

      background: white;
      color: black;
      font-size: clamp(30px, 6vw, 75px);
      font-weight: bold;

      transition: opacity 1s ease;
    }

    #welcome.hidden {
      opacity: 0;
      pointer-events: none;
    }

    /* The bouncing Mickey logos */
    .mickey {
      position: absolute;
      width: 190px;
      height: auto;
      user-select: none;
      pointer-events: none;

      will-change: transform;
    }

    /* Optional little title */
    #title {
      position: fixed;
      top: 15px;
      left: 50%;
      transform: translateX(-50%);

      z-index: 10;

      font-size: 24px;
      font-weight: bold;
      color: black;

      opacity: 0.8;
    }
  </style>
</head>

<body>

  <!-- Welcome screen -->
  <div id="welcome">
    welcom tu mai websait
  </div>

  <!-- Website title -->
  <div id="title">
    mai websait :D
  </div>

  <!-- Mickey PNGs -->
  <img class="mickey" src="classic-mickey-mouse5.png" alt="">
  <img class="mickey" src="classic-mickey-mouse7.png" alt="">

  <script>
    const mickeys = document.querySelectorAll(".mickey");

    // Each Mickey gets its own position and speed
    const objects = [];

    mickeys.forEach((mickey, index) => {
      objects.push({
        element: mickey,

        x: 100 + index * 250,
        y: 150 + index * 100,

        // Different speeds so they don't move together
        dx: index === 0 ? 2.7 : -3.1,
        dy: index === 0 ? 2.2 : 2.8
      });
    });

    function animate() {
      const screenWidth = window.innerWidth;
      const screenHeight = window.innerHeight;

      objects.forEach(obj => {
        const width = obj.element.offsetWidth;
        const height = obj.element.offsetHeight;

        obj.x += obj.dx;
        obj.y += obj.dy;

        // Bounce off left and right
        if (obj.x <= 0) {
          obj.x = 0;
          obj.dx *= -1;
        }

        if (obj.x + width >= screenWidth) {
          obj.x = screenWidth - width;
          obj.dx *= -1;
        }

        // Bounce off top and bottom
        if (obj.y <= 0) {
          obj.y = 0;
          obj.dy *= -1;
        }

        if (obj.y + height >= screenHeight) {
          obj.y = screenHeight - height;
          obj.dy *= -1;
        }

        obj.element.style.transform =
          `translate(${obj.x}px, ${obj.y}px)`;
      });

      requestAnimationFrame(animate);
    }

    // Start animation
    animate();


    // Welcome screen disappears after 2.5 seconds
    setTimeout(() => {
      document.getElementById("welcome").classList.add("hidden");
    }, 2500);
  </script>

</body>
</html>
