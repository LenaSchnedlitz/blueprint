<script lang="ts">
  import AppContent from './AppContent.svelte';
  import Footer from './Footer.svelte';
  import CallToAction from './core/CallToAction.svelte';
  import Logo from './core/Logo.svelte';
  import Tagline from './core/Tagline.svelte';
  import Title from './core/Title.svelte';
  import DarkModeToggle from './core/stickies/DarkModeToggle.svelte';
  import Scroller from './core/stickies/Scroller.svelte';
  import { onMount } from 'svelte';

  let initiate: () => void;

  const action = () => {
    initiate();
    document.body.scrollTo(0, window.innerHeight);
  };

  onMount(() => {
    // workaround for 100vh problem in iOS safari
    const setFullHeight = () => {
      document.documentElement.style.setProperty('--full-height', `${window.innerHeight}px`);
    };
    window.addEventListener('resize', setFullHeight);
    setFullHeight();
  });
</script>

<main>
  <section class="landing">
    <Title>
      <Logo />
      _TITLE_
    </Title>
    <section class="intro">
      <Tagline>
        Tagline why my project is <strong>amazing</strong> and you should definitely try it out <!-- TODO -->
      </Tagline>
      <CallToAction onclick={action}>
        Intriguing Call to Action <!-- TODO -->
      </CallToAction>
    </section>
    <!--
        TODO some background ideas - uncomment/replace/edit however you like
        <BackgroundBlurredBlob/>
        <BackgroundBlob/>
        <BackgroundLines/>
        <BackgroundRubberBand/>
    -->
    <DarkModeToggle />
    <Scroller>Get started</Scroller>
  </section>
  <section class="content">
    <Title>
      <Logo />
      _TITLE_
    </Title>
    <AppContent bind:initiate />
  </section>
</main>
<Footer author="_AUTHOR_" projectLink="_LINK_" />

<style>
  main {
    overflow: hidden;
  }

  .landing {
    position: relative;
    height: var(--full-height);
    background: linear-gradient(to top right, var(--primary-color-2), var(--primary-color-1));
    overflow: hidden;

    /* TODO background pattern - uncomment/replace/edit however you like
    background-color: var(--primary-color-1);
    background-image: radial-gradient(circle, var(--primary-color-2) 10%, transparent 10%), radial-gradient(circle, var(--primary-color-2) 10%, transparent 10%);
    background-size: 30px 30px;
    background-position: 0 0, 15px 15px;
     */
  }

  .intro {
    position: absolute;
    padding: 0 calc(var(--frame) * 2);
    bottom: 15vh;
    z-index: 1;
  }

  @media all and (min-width: 900px) {
    .intro {
      top: 50vh;
      bottom: auto;
      padding-right: 30vw;
    }
  }

  .content {
    position: relative;
    min-height: var(--full-height);
  }
</style>
