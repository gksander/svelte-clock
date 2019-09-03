<script>
  /**
   * Component props.
   */
  export let hour;
  export let minute;
  export let second;

  // SVG constants
  const R = 50,
    hourTickL = 6,
    minuteTickL = hourTickL / 3,
    hourHandLength = 25,
    minuteHandLength = 45,
    secondHandLength = 45,
    hours = [...Array(12).keys()],
    minutes = [...Array(60).keys()].filter(m => m % 5 != 0);
</script>

<svg viewBox="0 0 100 100" style="width: 50%; margin: 12px 0px;">
  <circle
    cx={R}
    cy={R}
    r={R - 1}
    style="stroke: white; fill: white; fill-opacity: 0.1" />
  <!-- Hour indicators -->
  <g>
    {#each hours as h}
      <line
        x1={R + (R - 3) * Math.cos((h * 2 * Math.PI) / 12)}
        y1={R + (R - 3) * Math.sin((h * 2 * Math.PI) / 12)}
        x2={R + (R - 3 - hourTickL) * Math.cos((h * 2 * Math.PI) / 12)}
        y2={R + (R - 3 - hourTickL) * Math.sin((h * 2 * Math.PI) / 12)}
        style="stroke: white" />
    {/each}
  </g>
  <!-- Minute indicators -->
  <g>
    {#each minutes as m}
      <line
        x1={R + (R - 3) * Math.cos((m * 2 * Math.PI) / 60)}
        y1={R + (R - 3) * Math.sin((m * 2 * Math.PI) / 60)}
        x2={R + (R - 3 - minuteTickL) * Math.cos((m * 2 * Math.PI) / 60)}
        y2={R + (R - 3 - minuteTickL) * Math.sin((m * 2 * Math.PI) / 60)}
        style="stroke: white; stroke-width: 0.5;" />
    {/each}
  </g>
  <!-- Hour hand -->
  <line
    x1={R}
    y1={R}
    x2={R + hourHandLength * Math.cos(-Math.PI / 2 + (hour * 2 * Math.PI) / 12)}
    y2={R + hourHandLength * Math.sin(-Math.PI / 2 + (hour * 2 * Math.PI) / 12)}
    style="stroke: white" />
  <!-- Minute hand -->
  <line
    x1={R}
    y1={R}
    x2={R + minuteHandLength * Math.cos(-Math.PI / 2 + (minute * 2 * Math.PI) / 60)}
    y2={R + minuteHandLength * Math.sin(-Math.PI / 2 + (minute * 2 * Math.PI) / 60)}
    style="stroke: white;" />
  <!-- Second hand -->
  <line
    x1={R + 5 * Math.cos(Math.PI / 2 + (second * 2 * Math.PI) / 60)}
    y1={R + 5 * Math.sin(Math.PI / 2 + (second * 2 * Math.PI) / 60)}
    x2={R + secondHandLength * Math.cos(-Math.PI / 2 + (second * 2 * Math.PI) / 60)}
    y2={R + secondHandLength * Math.sin(-Math.PI / 2 + (second * 2 * Math.PI) / 60)}
    style="stroke: red" />
  <!-- Throw a circle in the center to cover up intersection -->
  <circle cx={R} cy={R} r={1} style="stroke: white; fill: white" />
</svg>
