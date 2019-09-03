<script>
  import { onMount } from "svelte";
  import {
    format as formatDate,
    getHours,
    getMinutes,
    getSeconds
  } from "date-fns";
  import Clock from "./components/Clock.svelte";

  let now = new Date();

  /**
   * Some computed properties: prettied dates, etc.
   */
  $: prettyTime = formatDate(now, `hh:mm.ss a`);
  $: prettyDate = formatDate(now, `EEEE, MM/dd/yyyy`);
  $: millisecond = now.getMilliseconds();
  $: second = parseInt(formatDate(now, `ss`)) + millisecond / 1000;
  $: minute = parseInt(formatDate(now, `m`)) + second / 60;
  $: hour = parseInt(formatDate(now, `hh`)) + minute / 60;

  /**
   * Function to animate:
   * - update the "now" variable to current date, and request to run again on next frame.
   */
  function animate() {
    now = new Date();
    window.requestAnimationFrame(animate);
  }

  /**
   * On mount, start the animation
   */
  onMount(() => {
    animate();
  });
</script>

<style>
  :global(body),
  :global(html) {
    padding: 0;
    margin: 0;
  }

  :global(body) {
    height: 100vh;
    overflow: hidden;
    font-family: "Courier New", Courier, monospace;
    /* Background from: https://leaverou.github.io/css3patterns/#starry-night */
    background-color: #110d1c;
    background-image: radial-gradient(
        white,
        rgba(255, 255, 255, 0.2) 2px,
        transparent 25px
      ),
      radial-gradient(white, rgba(255, 255, 255, 0.15) 1px, transparent 15px),
      radial-gradient(white, rgba(255, 255, 255, 0.1) 2px, transparent 25px),
      radial-gradient(
        rgba(255, 255, 255, 0.4),
        rgba(255, 255, 255, 0.1) 2px,
        transparent 15px
      );
    background-size: 550px 550px, 350px 350px, 250px 250px, 150px 150px;
    background-position: 0 0, 40px 60px, 130px 270px, 70px 100px;
  }

  .wrapper {
    height: 100vh;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .light--text {
    color: white;
    font-weight: 600;
  }

  .text--xl {
    font-size: 2.5em;
  }
  .text--lg {
    font-size: 1.5em;
  }
</style>

<div class="wrapper">
  <div class="light--text text--xl">{prettyTime}</div>
  <Clock {hour} {minute} {second} />
  <div class="light--text text--lg">{prettyDate}</div>
</div>
