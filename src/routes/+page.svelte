<script>
    import { onMount } from 'svelte';
    let scrollContainer;
    let scrollTop = 0;
    let raf;

    // Throttled scroll handler using requestAnimationFrame
    function handleScroll() {
        if (raf) cancelAnimationFrame(raf);
        raf = requestAnimationFrame(() => {
            scrollTop = scrollContainer.scrollTop;
        });
    }

    onMount(() => {
        scrollContainer.addEventListener('scroll', handleScroll, {
            passive: true,
        });
    });

    // Compute animation progress [0..1]
    $: progress = Math.min(scrollTop / 700, 1);
    // Angle from 90deg to 0
    $: angle = 90 * (1 - progress);
    // Scale from 0 (hidden) to 1 (full size)
    $: scale = progress;
    // Opacity from 0 to 1
    $: opacity = progress;
</script>

<svelte:head>
    <link
        href="https://fonts.googleapis.com/css2?family=DM+Serif+Text:ital@0;1&family=Lexend:wght@100..900&family=Source+Code+Pro:ital,wght@0,200..900;1,200..900&display=swap"
        rel="stylesheet"
    />
</svelte:head>

<div
    bind:this={scrollContainer}
    class="main snap-y snap-mandatory h-screen w-full overflow-y-auto text-gray-200 select-none"
>
    <!-- Hero -->
    <section
        class="bio snap-start h-5/6 flex flex-col items-center justify-center p-5"
    >
        <div class="flex gap-20 items-center">
            <img
                class="rounded-full w-64 border-3 border-white"
                src="https://media.licdn.com/dms/image/v2/D5603AQFi7Qng77F2KQ/profile-displayphoto-shrink_800_800/B56ZdCCcF9HoAc-/0/1749159625765?e=1756944000&v=beta&t=yi7plZms_VSjEt2p7MVonPzlpRpREHqoGqDGtKt2V9c"
                alt=""
            />
            <div class="text-left max-w-screen-xl">
                <div class="text-white text-5xl font-bold mb-4">Hi, I'm</div>
                <div
                    class="name text-[6rem] font-normal leading-[0.8] -ml-2 tracking-tight gradient-text mb-6"
                >
                    Raima Falor
                </div>
                <p class="mt-8 text-white text-xl max-w-xl">
                    I'm a second year Computer Science student at Santa Clara
                    University, driven by a passion for creating meaningful
                    digital experiences through web and UX design. Through
                    tutoring, app design projects, and community leadership
                    initiatives, I've developed collaborative skills that bridge
                    the gap between innovative ideas and impactful execution.
                </p>
                <p class="mt-4 font-bold text-white text-lg max-w-xl">
                    Below, you'll see interactive demos of my latest projects :)
                </p>
            </div>
        </div>
    </section>

    <!-- Project 1: Campus Cues -->
    <section class="snap-start h-full w-full relative grid project-section">
        <div
            class="title-section grid place-items-center text-white px-12 my-6 rounded-tr-lg rounded-br-lg"
        >
            <div class="title min-w-64">
                <h2 class="font-semibold text-3xl">Campus Cues</h2>
                <p class="text-lg mt-4">
                    A web app designed to help students find and share campus
                    events.
                </p>
                <ul class="languages list-none text-lg mt-4">
                    <li>Svelte</li>
                    <li>TypeScript</li>
                    <li>Supabase</li>
                    <li>Tailwind CSS</li>
                </ul>
            </div>
        </div>
        <div class="iframe-wrapper grid place-items-center w-full h-full p-6">
            <iframe
                class="{progress < 1
                    ? 'pointer-events-none'
                    : ''} w-full h-full rounded-lg shadow-md border-none smooth-anim"
                src="https://campuscues.vercel.app/?demo"
                allowfullscreen
                style="
                    transform-origin: right center;
                    transform: rotateY({angle}deg) scale({scale});
                    opacity: {opacity};
                "
            ></iframe>
        </div>
    </section>

    <!-- Project 1: Campus Cues -->
    <section class="snap-start h-full w-full relative grid project-section">
        <div class="iframe-wrapper grid place-items-center w-full h-full p-6">
            <iframe
                class="{progress < 1
                    ? 'pointer-events-none'
                    : ''} w-full h-full rounded-lg shadow-md border-none smooth-anim"
                src="https://portfolio-match.vercel.app/?demo"
                allowfullscreen
                style="
                    transform-origin: right center;
                    transform: rotateY({angle}deg) scale({scale});
                    opacity: {opacity};
                "
            ></iframe>
        </div>
        <div
            class="title-section grid place-items-center text-white px-12 my-6 rounded-tr-lg rounded-br-lg"
        >
            <div class="title min-w-64">
                <h2 class="font-semibold text-3xl">Portfolio Match</h2>
                <p class="text-lg mt-4">
                    A web app designed to help students find and share their
                    portfolios.
                </p>
                <ul class="languages list-none text-lg mt-4">
                    <li>Svelte</li>
                    <li>TypeScript</li>
                    <li>Supabase</li>
                    <li>Tailwind CSS</li>
                </ul>
            </div>
        </div>
    </section>
</div>

<style>
    .main {
        background: linear-gradient(to left, #e7c14f, #1398b6, #01aba6);
        background-size: 150% 100%;
        background-position: 0% 0%;
        scroll-behavior: smooth;
        scroll-snap-stop: always;
    }

    .gradient-text {
        background-image: linear-gradient(to right, #ffd93d, #ffd93d);
        background-clip: text;
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
    }

    .iframe-wrapper {
        perspective: 1000px;
    }

    .smooth-anim {
        will-change: transform, opacity;
    }

    .name {
        font-family: 'Lexend', sans-serif;
    }

    .bio {
        font-family: 'Source Code Pro', serif;
    }

    .project-section {
        font-family: 'Lexend', sans-serif;
        grid-template-columns: min-content 1fr;
        grid-template-rows: auto;
    }

    .project-section:nth-child(odd) {
        margin-top: 1em;
        grid-template-columns: 1fr min-content;
    }

    .languages {
        font-family: 'Source Code Pro', monospace;
    }

    @media (max-width: 640px) {
        .project-section {
            grid-template-columns: 1fr;
            grid-template-rows: auto 1fr;
        }
        .title {
            padding-block: 1.2em;
        }
    }
</style>
