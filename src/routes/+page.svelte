<svelte:head>
    <link
        href="https://fonts.googleapis.com/css2?family=DM+Serif+Text:ital@0;1&family=Lexend:wght@100..900&family=Source+Code+Pro:ital,wght@0,200..900;1,200..900&display=swap"
        rel="stylesheet"
    />
</svelte:head>

<div
    class="h-screen w-full overflow-y-auto snap-y snap-mandatory bg-gradient-to-b from-[#1a1a1a] to-[#0a0a0a] text-gray-200 select-none"
>
    <!-- Hero -->
    <section
        class="bio snap-start h-5/6 flex flex-col items-center justify-center p-5"
    >
        <div class="text-left max-w-screen-xl">
            <div class="text-white text-5xl font-bold mb-4">Hello, I'm</div>
            <div
                class="text-[8rem] font-normal leading-[0.8] -ml-2 tracking-tight bg-gradient-to-r from-pink-500 via-purple-500 via-blue-500 via-green-500 to-orange-500 font-sans gradient-text mb-6"
            >
                Raima
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
                Below, you'll see some of latest projects as an interactive demo
                :)
            </p>
        </div>
    </section>

    <!-- Project 1: Campus Cues -->
    <section class="snap-start h-full w-full relative grid project-section">
        <div class="grid place-items-center text-white bg-pink-700 px-12">
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
        <iframe
            src="https://campuscues.vercel.app"
            class="w-full h-full border-none"
        ></iframe>
    </section>

    <!-- Project 2: Portfolio Match -->
    <section class="snap-start h-screen w-full relative grid project-section">
        <div class="grid place-items-center text-white bg-blue-800 px-12">
            <div class="title min-w-64">
                <h2 class="font-semibold text-3xl">Portfolio Match</h2>
                <p class="text-lg mt-4">
                    A web app designed to match stock portfolios with
                    recommended investments.
                </p>
                <ul class="languages list-none text-lg mt-4">
                    <li>Svelte</li>
                    <li>TypeScript</li>
                    <li>Tailwind CSS</li>
                    <li>Gemini API</li>
                </ul>
            </div>
        </div>
        <iframe
            src="https://portfolio-match.vercel.app"
            class="w-full h-full border-none"
        ></iframe>
    </section>
</div>

<style>
    @keyframes gradientShift {
        0%,
        100% {
            background-position: 0% 50%;
        }
        50% {
            background-position: 100% 50%;
        }
    }
    .gradient-text {
        background-size: 200% 200%;
        background-clip: text;
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        animation: gradientShift 4s ease-in-out infinite;
    }

    .bio {
        font-family: 'Source Code Pro', serif;
    }

    .project-section {
        font-family: 'Lexend', sans-serif;
        /* desktop: two columns, title + iframe */
        grid-template-columns: min-content 1fr;
        /* desktop: single‑row grid */
        grid-template-rows: auto;
    }
    /* 
    .project-section:nth-child(odd) {
        grid-template-columns: 1fr min-content;
    } */

    .languages {
        font-family: 'Source Code Pro', monospace;
    }

    /* mobile: single‑column, with title row auto‑height and iframe filling */
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
