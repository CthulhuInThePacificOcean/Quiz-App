<template>
    <nav>
        <ul>
            <li>
                <router-link
                    to="/quizgen"
                    class="rounded bg-blue-500 p-1 text-white"
                >
                    Start New Quiz
                </router-link>
            </li>
        </ul>
    </nav>
    <div class="flex flex-row">
        <img src="" alt="placeholder" class="m-3" />
        <div class="m-3">
            <p>Number of questions answered correctly:</p>
            <p>Number of questions answered:</p>
            <p>Correct-Incorrect Ratio:</p>
        </div>
    </div>
</template>
