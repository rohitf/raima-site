<script>
    import { onMount } from 'svelte';
    let iframeVisible = false;
    let firstSectionHeight = 0;
    let scrollContainer;

    function handleScroll() {
        if (!iframeVisible && scrollContainer.scrollTop >= firstSectionHeight) {
            setTimeout(() => {
                iframeVisible = true;
                scrollContainer.removeEventListener('scroll', handleScroll);
            }, 200); // Delay to allow for scroll animation
        }
    }

    onMount(() => {
        // calculate height of the first snap-start section
        const firstSection = document.querySelector('.bio');
        firstSectionHeight = firstSection
            ? firstSection.offsetHeight - 20
            : window.innerHeight;
        // listen on the scrollable main container, not window
        scrollContainer.addEventListener('scroll', handleScroll);
    });
</script>

<svelte:head>
    <link
        href="https://fonts.googleapis.com/css2?family=DM+Serif+Text:ital@0;1&family=Lexend:wght@100..900&family=Source+Code+Pro:ital,wght@0,200..900;1,200..900&display=swap"
        rel="stylesheet"
    />
</svelte:head>

<div
    bind:this={scrollContainer}
    class="main h-screen w-full overflow-y-auto snap-y snap-mandatory text-gray-200 select-none"
>
    <!-- Hero -->
    <section
        class="bio snap-start h-5/6 flex flex-col items-center justify-center p-5"
    >
        <div class="text-left max-w-screen-xl">
            <div class="text-white text-5xl font-bold mb-4">Hello, I'm</div>
            <div
                class="name text-[6rem] font-normal leading-[0.8] -ml-2 tracking-tight gradient-text mb-6"
            >
                Raima Falor
            </div>
            <p class="mt-12 text-white text-lg max-w-xl">
                I'm a first-year Computer Science student at Santa Clara
                University, driven by a passion for creating meaningful digital
                experiences through web and UX design. Through tutoring, app
                design projects, and community leadership initiatives, I've
                developed collaborative skills that bridge the gap between
                innovative ideas and impactful execution.
            </p>
            <p class="mt-4 font-bold text-white text-lg max-w-xl">
                Below, you'll see some of my latest projects as an interactive
                demo :)
            </p>
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
        <div
            class="iframe-wrapper grid place-items-center w-full h-full p-6"
            class:visible={iframeVisible}
        >
            <iframe
                class="w-full h-full rounded-lg shadow-sm border-none"
                src="https://campuscues.vercel.app/?demo"
                allowfullscreen
            ></iframe>
        </div>
    </section>
</div>

<style>
    .main {
        background: linear-gradient(
            to left,
            #ff6b6b,
            #e4af0d,
            #12a3c4,
            #01aba6
        );
        background-size: 200% 200%;
        background-position: 0% 50%;
        /* animation: gradientShift 1s ease-out forwards; */
    }

    @keyframes gradientShift {
        to {
            background-position: 0% 50%;
        }
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

    .iframe-wrapper iframe {
        transform-origin: right center;
        transform: rotateY(90deg);
        opacity: 0;
        transition:
            transform 0.6s ease-out,
            opacity 0.6s ease-out;
    }

    .iframe-wrapper.visible iframe {
        transform: rotateY(0deg);
        opacity: 1;
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
