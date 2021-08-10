<script>
  let partyText = "Vibe for 30 seconds 🎉";
  let play = false;
  let dancingMusic;
  let i = 0;
  let duck = false;
  let temp = "/extras/doge-flip.gif";
  let progress;
  let interval;

  function delay(delayInms) {
    return new Promise((resolve) => {
      setTimeout(() => {
        resolve(2);
      }, delayInms);
    });
  }
  const generateRandomColors = async () => {
    let randomColor;
    setTimeout(async () => {
      duck = true;
      // dragElement(document.getElementById("mydiv2"));
      while (play && i < 70) {
        if (i % 4 == 0) {
          temp =
            temp == "/extras/doge.gif"
              ? "/extras/doge-flip.gif"
              : "/extras/doge.gif";
          party.confetti(document.getElementById("section"), {
            shapes: ["square", "circle", "roundedRectangle"],
          });
        }
        randomColor = "#" + Math.floor(Math.random() * 16777215).toString(16);
        document.getElementById("section").style.backgroundColor = randomColor;
        i++;
        await delay(250);
      }
      duck = false;
      document.getElementById("section").style.backgroundColor = "#212529";
    }, 17500);
  };

  const resetAudio = () => {
    dancingMusic.pause();
    dancingMusic.currentTime = 0;
  };

  const dancingDog = () => {
    // set defaults to prevent leaking
    clearInterval(interval);
    progress.value = 0;
    let el = document.getElementById("mydiv");
    el.style.left = (0.7 * window.innerWidth) / 2 + "px";
    dancingMusic.play();
    interval = setInterval(() => {
      progress.value += 0.14;
    }, 50);
    generateRandomColors();
    partyText = "Such Doge, Much Wow!";
    setTimeout(() => {
      play = true;
    }, 1500);

    dragElement(document.getElementById("mydiv"));
    setTimeout(() => {
      resetAudio();
      play = false;
      partyText = "Vibe for 30 seconds 🎉";
      i = 0;
      clearInterval(interval);
      progress.value = 0;
    }, 36000);
  };

  function dragElement(elmnt) {
    var pos1 = 0,
      pos2 = 0,
      pos3 = 0,
      pos4 = 0;
    if (document.getElementById(elmnt.id + "header")) {
      // if present, the header is where you move the DIV from:
      document.getElementById(elmnt.id + "header").onmousedown = dragMouseDown;
    } else {
      // otherwise, move the DIV from anywhere inside the DIV:
      elmnt.onmousedown = dragMouseDown;
    }

    function dragMouseDown(e) {
      e = e || window.event;
      e.preventDefault();
      // get the mouse cursor position at startup:
      pos3 = e.clientX;
      pos4 = e.clientY;
      document.onmouseup = closeDragElement;
      // call a function whenever the cursor moves:
      document.onmousemove = elementDrag;
    }

    function elementDrag(e) {
      e = e || window.event;
      e.preventDefault();
      // calculate the new cursor position:
      pos1 = pos3 - e.clientX;
      pos2 = pos4 - e.clientY;
      pos3 = e.clientX;
      pos4 = e.clientY;
      // set the element's new position:
      elmnt.style.top = elmnt.offsetTop - pos2 + "px";
      elmnt.style.left = elmnt.offsetLeft - pos1 + "px";
    }

    function closeDragElement() {
      // stop moving when mouse button is released:
      document.onmouseup = null;
      document.onmousemove = null;
    }
  }
</script>

<section
  id="section"
  class="hero is-dark is-fullheight"
  style="background-color: #212529;"
>
  <progress
    bind:this={progress}
    class="progress is-success is-small"
    value="0"
    max="100"
  />
  <div class="hero-body">
    <div id="mydiv">
      <img src="/dancing.gif" hidden={!play} id="mydivheader" alt="" />
      <img src={temp} hidden={!duck} id="mydiv2header" alt="" />
    </div>
    <audio src="/dancing.mp3" bind:this={dancingMusic} />
    {#if !play}
      <div class="container">
        <div class="columns is-centered">
          <div class="column is-half">
            <div class="buttons">
              <button on:click={dancingDog} class="button is-black"
                >{partyText}</button
              >
              &nbsp
              <a
                href="https://github.com/amalshaji/vibe"
                target="_blank"
                class="button is-info"
              >
                <img src="/github.png" width="25px" alt="" /> &nbsp; Source Code
              </a>
            </div>
          </div>
        </div>
      </div>
    {/if}
  </div>
</section>

<style>
  #mydiv {
    position: absolute;
    z-index: 9;
  }

  .progress {
    border-radius: 0%;
  }

  .progress::-webkit-progress-value {
    background-color: #30aa4e !important;
  }

  .progress::-webkit-progress-bar {
    background-color: #212529 !important;
  }
  .progress::-moz-progress-value {
    background-color: #30aa4e !important;
  }

  .progress::-moz-progress-bar {
    background-color: #212529 !important;
  }

  .progress::-ms-fill {
    background-color: #212529 !important;
    border: none;
  }

  /* Hide scrollbar for Chrome, Safari and Opera */

  #mydivheader,
  #mydiv2header {
    cursor: move;
    z-index: 10;
  }
</style>
