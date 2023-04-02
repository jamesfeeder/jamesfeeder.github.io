<script lang="ts">
  import { fly, blur } from "svelte/transition";
  import { quartInOut } from "svelte/easing";
  import { scrollRef } from "../utils/stores";
  import { onDestroy } from "svelte";

  let scrollRefValue: Element;

  scrollRef.subscribe((value) => {
    scrollRefValue = value;
  });

  onDestroy(() => {
    scrollRefValue.scrollTop = 0;
  });

  //in:blur={{ duration: 800 }} out:blur={{ duration: 240 }}
</script>

<main
  in:fly={{ y: 120, duration: 480, easing: quartInOut }}
  out:fly={{ x: 120, duration: 240, easing: quartInOut }}
>
  <header in:blur={{ duration: 600 }} out:blur={{ duration: 200 }}>
    <div>
      <h1>Jetsadakorn Maliwan</h1>
      <div class="subtitle">
        <h4>Software Developer /</h4>
        <h4>Front-End Web Developer</h4>
      </div>

      <!-- <h3>Software & Web Developing Skills</h3> -->
      <section class="skill">
        <p>React</p>
        <p>HTML</p>
        <p>SCSS</p>
        <p>TypeScript</p>
        <p>Svelte</p>
        <p>Flutter</p>
        <p>Firebase</p>
        <p>Python</p>
        <p>Unity</p>
        <p>C#</p>
        <p>Git</p>
        <p>Figma</p>
        <p>UX/UI Design</p>
      </section>

      <!-- <h3>Additional Skills</h3>
      <div class="skill">
        <p>Photography</p>
        <p>Photo Editing</p>
        <p>Video Editing</p>
        <p>Color Grading</p>
        <p>Basic Graphics Design</p>
      </div> -->
    </div>
    <div class="contact">
      <a href="mailto:jetsadakorn.maliwan@gmail.com" target="_blank"
        >jetsadakorn.maliwan@gmail.com</a
      >
      <a href="tel:+66986707180" target="_blank">(+66)986707180</a>
      <a href="https://github.com/jamesfeeder" target="_blank"
        >github.com/jamesfeeder</a
      >
    </div>
  </header>
  <section class="exp" in:blur={{ duration: 600 }} out:blur={{ duration: 200 }}>
    <h2>Experience</h2>

    <div class="timeline-item">
      <p class="time">2023</p>
      <h4>
        Speaker in Design Research Day - Bangkok Design Week 2023 @ TCDC Bangkok
      </h4>
      <p>
        Journey of the Waste Town game project. <br />
        Collaborate with Prakakit Ananlertsakul
      </p>
    </div>

    <div class="timeline-item">
      <p class="time">2022 - Preset</p>
      <h4>Banno's Diary Website</h4>
      <p>
        Develop Web Application for order Banno's Diary Line Sticker, including
        tools for managing website content.
      </p>
    </div>

    <div class="timeline-item">
      <p class="time">2022</p>
      <h4>Waste Town, Academic Project</h4>
      <p>
        2D Game for raising social responsibility about waste management
        reference environment in Thailand. <br />
        Collaborate with Prakakit Ananlertsakul
      </p>
    </div>

    <div class="timeline-item">
      <p class="time">2021</p>
      <h4>PSUIC CMDT Website</h4>
      <p>
        Develop custom Wordpress child theme. for PSUIC CMDT Program Website
      </p>
    </div>

    <div class="timeline-item">
      <p class="time">2020</p>
      <h4>
        2<sup>nd</sup> Runner Up - National Software Contest (NSC2020)
      </h4>
      <p>
        Software Developer in SABISU project, application for businesses and
        SMEs Project Manageger
      </p>
    </div>

    <div class="timeline-item">
      <p class="time">2020</p>
      <h4>Nam Yang Thai Cooperative Database Website</h4>
      <p>Develop and database design for website for manage customer data.</p>
    </div>

    <div class="timeline-item">
      <p class="time">2020 - 2021</p>
      <h4>Covid-19 Tracking Status Website</h4>
      <p>
        Develop Covid-19 statistic website focus in Songkhla and University
        area.
      </p>
    </div>

    <div class="timeline-item">
      <p class="time">2020 - Present</p>
      <h4>Name Sticker Renderer</h4>
      <p>Banno's Diary in-house tools for render sticker.</p>
    </div>

    <div class="timeline-item">
      <p class="time">2019</p>
      <h4>Finalist - National Software Contest (NSC2019)</h4>
      <p>Software Developer in My Caregiver project.</p>
    </div>

    <div class="timeline-item">
      <p class="time">2019</p>
      <h4>7<sup>th</sup> PSUIC Student Association</h4>
      <p>
        Public Relations <br />
        Prince of Songkla University International College
      </p>
    </div>

    <h2>Education</h2>

    <div class="timeline-item">
      <p class="time">2018-2022</p>
      <h4>
        International College <br />
        Creative Media Digital Technology
      </h4>
      <p>Prince of Songkla University, Hatyai Campus</p>
    </div>

    <div class="timeline-item">
      <p class="time">2012-2017</p>
      <h4>Sci-Math Ability Program</h4>
      <p>Hatyaiwittayalai School, Songkhla</p>
    </div>
  </section>
</main>

<style lang="scss">
  main {
    max-width: 800px;
    padding: 16px;
    margin: auto;

    header {
      margin-top: 88px;
      display: grid;
      grid-template-columns: 3fr 1fr;
      gap: 24px;

      h1 {
        font-size: 2.6rem;
        margin-top: 0;
        margin-bottom: 8px;
      }

      .subtitle {
        display: flex;
        flex-wrap: wrap;
        column-gap: 6px;
        margin-top: 8px;
        margin-bottom: 24px;

        h4 {
          color: hsl(0, 0%, 50%);
          margin: 0;
        }
      }

      .contact {
        display: flex;
        flex-direction: column;
        justify-content: start;
        align-items: end;
        margin-top: 8px;

        a {
          padding: 4px;
        }

        :last-child {
          margin-bottom: -4px;
        }
      }
    }

    h2 {
      margin-top: 24px;
      margin-bottom: 8px;
    }

    .skill {
      // max-width: 600px;
      display: flex;
      flex-wrap: wrap;
      gap: 8px;

      p {
        background-color: hsl(225, 73%, 57%);
        color: hsl(0, 0%, 100%);
        padding: 4px 8px;
        border-radius: 48px;
        font-size: 0.9rem;
        font-weight: 600;
      }
    }

    .exp {
      margin-top: 32px;
      margin-bottom: 56px;
    }

    .timeline-item {
      .time {
        width: fit-content;
        margin-top: 16px;
        background-color: hsl(225, 73%, 57%);
        color: hsl(0, 0%, 100%);
        padding: 4px 8px;
        border-radius: 48px;
        font-size: 0.8rem;
        font-weight: 600;
      }

      h4 {
        margin-top: 8px;
      }
    }
  }

  @media screen and (max-width: 700px) {
    main {
      header {
        display: block;

        .contact {
          margin-top: 24px;
          justify-content: end;
          align-items: start;
        }
      }
      .exp {
        margin-top: 24px;
      }
    }
  }
</style>
