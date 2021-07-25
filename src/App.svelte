<script>
  let party = "Vibe for 30 seconds 🎉";
  let play = false;
  let dancingMusic;

  const dancingDog = () => {
    party = "🎉🎉🎉🎉🎉🎉";
    setTimeout(() => {
      play = true;
    }, 2000);

    dancingMusic.play();
    dragElement(document.getElementById("mydiv"));
    setTimeout(() => {
      play = false;
      party = "Vibe for 30 seconds 🎉";
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

<section class="hero is-dark is-fullheight" style="overflow: hidden;">
  <div class="hero-body">
    <div id="mydiv">
      <img src="/dancing.gif" hidden={!play} id="mydivheader" alt="" />
    </div>
    <audio src="/dancing.mp3" bind:this={dancingMusic} />
    {#if !play}
      <button on:click={dancingDog} class="button is-link">{party}</button>
      &nbsp
      <a
        href="https://github.com/amalshaji/vibe"
        target="_blank"
        class="button is-light"
      >
        <img src="/github.png" alt="" /> &nbsp; GitHub
      </a>
    {/if}
  </div>
</section>

<style>
  #mydiv {
    position: absolute;
    z-index: 9;
  }

  #mydivheader {
    cursor: move;
    z-index: 10;
  }
</style>
