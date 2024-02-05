<script>
  import { onMount } from 'svelte';
  import Profile from './profile.svelte';

  const relationshipStart = 1684173600;

  function updateProgress(progress) {
    const progressLine = document.getElementById('progress');
    progressLine.style.setProperty("--progress", `${progress}%`)
  }

  function yearsBetweenDates(t1, t2) {
    const millisecondsPerYear = 1000 * 60 * 60 * 24 * 365.25;
    const date1 = new Date(t1 * 1000);
    const date2 = new Date(t2 * 1000);

    const differenceMilliseconds = Math.abs(date2 - date1);
    const yearsPassed = differenceMilliseconds / millisecondsPerYear;

    return Math.floor(yearsPassed);
  }

  function getFormattedTimeDifference(unixTimestamp) {
    const currentTime = new Date().getTime();
    const difference = currentTime - unixTimestamp * 1000;

    const millisecondsInDay = 1000 * 60 * 60 * 24;
    const millisecondsInYear = millisecondsInDay * 365;

    const years = Math.floor(difference / millisecondsInYear);
    const remainingMilliseconds = difference % millisecondsInYear;
    const days = Math.floor(remainingMilliseconds / millisecondsInDay);

    if (years === 0) return `${days} dana`;

    return `${years} godina, ${days} dana`;
  }

  const formattedTime = getFormattedTimeDifference(relationshipStart);
  onMount(()=> {
    const now = new Date().getTime();
    const years = yearsBetweenDates(relationshipStart, now);

    const remaining = relationshipStart + 3.154e+7 - now;
    const total = relationshipStart + (3.154e+7*(years===1?2:years)) - relationshipStart;
    updateProgress(Math.abs(total/remaining)) // 50
  })
</script>

<div class="main-container">
  <div class="container">
    <svelte:component this={Profile} username="hena" image="https://cdn.discordapp.com/attachments/1130972374368522301/1204156930906529852/16439165a5076c94bea6b32b4e448ba8.jpg?ex=65d3b588&is=65c14088&hm=60b1fb2f5b3db7a31bf7a71dab42f6644d15406efba940bb109be0283b11f268&"></svelte:component>
    <img class="middle-heart" src="./heart.svg" alt="heart"/>
    <svelte:component this={Profile} username="kadraa" image="https://cdn.discordapp.com/attachments/1130972374368522301/1204157702499213393/kadraapfp.png?ex=65d3b640&is=65c14140&hm=6247c212ce72d33b5545144e42beb0b139d995818d89111687c2e62e0f22a640&"></svelte:component>
  </div>
  <p>
    su zajedno
  </p>
  <h1>
    {formattedTime}
  </h1>
  <div class="progress-container">
    <div class="progress-bar">
      <div class="progress" id="progress"></div>
    </div>
  </div>
</div>

<style>
  .main-container {
    display: flex;
    height: 80%;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }

  .container {
    display: flex;
    align-items: center;
    justify-content: center;
    column-gap: 24px;
  }

  p {
    font-size: 30pt;
    color: rgb(200, 200, 200);
    padding: 0;
    margin: 0;
    margin-top: 18px;
  }

  h1 {
    color: rgb(240, 240, 240);
    margin-top: 0.1em;
    margin-bottom: 0.8em;
  }

  @keyframes heartbeat {
  0% {
    transform: scale(1);
  }
  20% {
    transform: scale(1.1);
  }
  40% {
    transform: scale(1);
  }
  60% {
    transform: scale(1.1);
  }
  80% {
    transform: scale(1);
  }
  100% {
    transform: scale(1);
  }
}

  .middle-heart {
    aspect-ratio: 1;
    height: 48px;
    width: 48px;
    translate: 0 50%;
    animation: heartbeat 1.5s infinite;
  }

  .progress-container {
    width: 80%;
    max-width: 400px;
    background-color: #f0f0f0;
    border-radius: 5px;
  }

  .progress-bar {
    position: relative;
    width: 100%;
    height: 8px;
  }

  .progress {
    --progress: 0;
    width: var(--progress);
    height: 100%;
    background-color: #f4abba;
    border-radius: 5px;
  }

  .progress::after {
    position: absolute;
    aspect-ratio: 1;
    height: 12px;
    content: "";
    left: var(--progress);
    background-image: "./heart.svg";
    background-repeat: no-repeat;
    background-size: 100%;
    background-position: 50% 50%;
    translate: -70% -125%;
  }
</style>