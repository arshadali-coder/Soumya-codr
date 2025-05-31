<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Soumya-codr's Enhanced Animated GitHub Profile</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        /* Custom CSS for animations and specific styles */
        body {
            font-family: 'Inter', sans-serif;
            background: linear-gradient(135deg, #1a202c 0%, #2d3748 100%);
            color: #e2e8f0;
            overflow-x: hidden;
            position: relative; /* Needed for absolute positioning of particles */
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            padding: 1.5rem;
        }

        /* Typing effect for the main text */
        .typing-text::after {
            content: '|';
            display: inline-block;
            animation: blink-caret 0.75s step-end infinite;
        }

        @keyframes blink-caret {
            from, to { border-color: transparent }
            50% { border-color: #63b3ed; }
        }

        /* Code rain animation */
        .code-rain-container {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            pointer-events: none;
            z-index: 0;
        }

        .code-drop {
            position: absolute;
            font-family: 'monospace';
            font-size: 0.8rem;
            color: rgba(99, 179, 237, 0.5);
            animation: fall linear infinite;
            white-space: nowrap;
            opacity: 0;
        }

        @keyframes fall {
            0% {
                transform: translateY(-100%);
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            90% {
                opacity: 1;
            }
            100% {
                transform: translateY(calc(100vh + 50px));
                opacity: 0;
            }
        }

        /* Subtle glow effect for cards */
        .card-glow {
            box-shadow: 0 0 15px rgba(99, 179, 237, 0.3);
            transition: box-shadow 0.3s ease-in-out;
        }
        .card-glow:hover {
            box-shadow: 0 0 25px rgba(99, 179, 237, 0.6);
        }

        /* Particle background animation */
        .particle {
            position: absolute;
            background-color: rgba(255, 255, 255, 0.2); /* White particles, semi-transparent */
            border-radius: 50%;
            animation: float-and-fade linear infinite;
            pointer-events: none;
            z-index: 0;
        }

        @keyframes float-and-fade {
            0% {
                transform: translateY(0) translateX(0) scale(1);
                opacity: 0;
            }
            25% {
                opacity: 1;
            }
            75% {
                opacity: 1;
            }
            100% {
                transform: translateY(-100vh) translateX(var(--float-x)) scale(var(--scale));
                opacity: 0;
            }
        }

        /* Contribution grid squares animation */
        .contribution-square {
            width: 20px; /* Size of a single square */
            height: 20px;
            background-color: #4a5568; /* Default grey */
            border-radius: 3px;
            transition: background-color 0.3s ease-in-out, transform 0.2s ease-out;
            cursor: pointer;
        }

        .contribution-square:hover {
            transform: scale(1.1);
        }

        /* Different shades for contributions */
        .level-0 { background-color: #4a5568; } /* No contributions */
        .level-1 { background-color: #2d6b42; } /* Low contributions */
        .level-2 { background-color: #3b82f6; } /* Medium contributions */
        .level-3 { background-color: #63b3ed; } /* High contributions */
        .level-4 { background-color: #90cdf4; } /* Very high contributions */

        /* Responsive adjustments for smaller screens */
        @media (max-width: 768px) {
            .container {
                padding: 1rem;
            }
            h1 {
                font-size: 2.5rem;
            }
            h2 {
                font-size: 1.5rem;
            }
            .text-lg {
                font-size: 1rem;
            }
            .contribution-square {
                width: 15px;
                height: 15px;
            }
        }
    </style>
</head>
<body class="min-h-screen flex items-center justify-center relative">

    <div class="code-rain-container" id="code-rain"></div>

    <div class="absolute inset-0 overflow-hidden" id="particle-container"></div>

    <div class="container relative z-10 p-6 md:p-8 bg-gray-800 bg-opacity-70 rounded-xl shadow-lg card-glow border border-gray-700">
        <header class="text-center mb-8">
            <h1 class="text-4xl md:text-5xl font-extrabold text-blue-400 mb-2 animate-pulse">
                Soumya Sagar
            </h1>
            <p class="text-xl md:text-2xl font-semibold text-gray-300">
                @Soumya-codr
            </p>
            <div class="h-1 w-24 bg-blue-500 rounded-full mx-auto mt-4"></div>
        </header>

        <section class="mb-8 p-6 bg-gray-700 bg-opacity-80 rounded-lg card-glow">
            <h2 class="text-2xl md:text-3xl font-bold text-blue-300 mb-4">About Me</h2>
            <p id="intro-text" class="text-lg md:text-xl text-gray-200 leading-relaxed typing-text">
                </p>
        </section>

        <section class="mb-8 p-6 bg-gray-700 bg-opacity-80 rounded-lg card-glow text-center">
            <h2 class="text-2xl md:text-3xl font-bold text-blue-300 mb-4">Inspiration</h2>
            <p id="quote-display" class="text-xl md:text-2xl italic text-gray-200 mb-2 transition-opacity duration-500 ease-in-out">
                "The only way to do great work is to love what you do."
            </p>
            <p class="text-sm text-gray-400">- Steve Jobs</p>
        </section>

        <section class="mb-8 p-6 bg-gray-700 bg-opacity-80 rounded-lg card-glow">
            <h2 class="text-2xl md:text-3xl font-bold text-blue-300 mb-4">My Journey & Dreams</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="p-5 bg-gray-600 bg-opacity-70 rounded-lg shadow-md border border-gray-500 hover:scale-105 transition-transform duration-300">
                    <h3 class="text-xl font-semibold text-blue-200 mb-3 flex items-center">
                        <svg class="w-6 h-6 mr-2 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.663 17h4.673M12 3v14m-3-6h6m-6 4h6m-9 1l-3 3v2h18v-2l-3-3m-6 0V3"></path></svg>
                        Aspirations
                    </h3>
                    <p class="text-gray-200">
                        I am a new fresher in the coding world, but my dreams and aspirations are not limited; they are endless! I am eager to build impactful projects and contribute to the tech community.
                    </p>
                </div>
                <div class="p-5 bg-gray-600 bg-opacity-70 rounded-lg shadow-md border border-gray-500 hover:scale-105 transition-transform duration-300">
                    <h3 class="text-xl font-semibold text-blue-200 mb-3 flex items-center">
                        <svg class="w-6 h-6 mr-2 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"></path></svg>
                        Learning Path
                    </h3>
                    <p class="text-gray-200">
                        Currently, I am diving deep into **Web Development** (HTML, CSS, JavaScript) and planning to learn **Python** parallely to expand my horizons.
                    </p>
                </div>
            </div>
        </section>

        <section class="mb-8 p-6 bg-gray-700 bg-opacity-80 rounded-lg card-glow text-center">
            <h2 class="text-2xl md:text-3xl font-bold text-blue-300 mb-4">My Skills</h2>
            <div class="flex flex-wrap justify-center gap-4">
                <div class="flex flex-col items-center p-3 bg-gray-600 rounded-lg hover:scale-110 transition-transform duration-300">
                    <i class="fab fa-html5 text-5xl text-orange-500 mb-2"></i>
                    <span class="text-gray-200 font-medium">HTML5</span>
                </div>
                <div class="flex flex-col items-center p-3 bg-gray-600 rounded-lg hover:scale-110 transition-transform duration-300">
                    <i class="fab fa-css3-alt text-5xl text-blue-500 mb-2"></i>
                    <span class="text-gray-200 font-medium">CSS3</span>
                </div>
                <div class="flex flex-col items-center p-3 bg-gray-600 rounded-lg hover:scale-110 transition-transform duration-300">
                    <i class="fab fa-js-square text-5xl text-yellow-400 mb-2"></i>
                    <span class="text-gray-200 font-medium">JavaScript</span>
                </div>
                <div class="flex flex-col items-center p-3 bg-gray-600 rounded-lg hover:scale-110 transition-transform duration-300">
                    <i class="fab fa-python text-5xl text-blue-600 mb-2"></i>
                    <span class="text-gray-200 font-medium">Python</span>
                </div>
                <div class="flex flex-col items-center p-3 bg-gray-600 rounded-lg hover:scale-110 transition-transform duration-300">
                    <i class="fab fa-github text-5xl text-gray-300 mb-2"></i>
                    <span class="text-gray-200 font-medium">GitHub</span>
                </div>
            </div>
        </section>

        <section class="mb-8 p-6 bg-gray-700 bg-opacity-80 rounded-lg card-glow">
            <h2 class="text-2xl md:text-3xl font-bold text-blue-300 mb-4">Contribution Insights</h2>
            <p class="text-gray-300 mb-4">
                A visual representation of my coding activity. (Simulated, not live data)
            </p>
            <div id="contribution-grid" class="grid gap-1 justify-center" style="grid-template-columns: repeat(auto-fill, minmax(20px, 1fr));">
                </div>
        </section>

        <section class="text-center p-6 bg-gray-700 bg-opacity-80 rounded-lg card-glow">
            <h2 class="text-2xl md:text-3xl font-bold text-blue-300 mb-4">Let's Connect!</h2>
            <p class="text-lg text-gray-200 mb-6">
                Feel free to explore my repositories and connect with me. Let's build amazing things together!
            </p>
            <a href="https://github.com/Soumya-codr" target="_blank" rel="noopener noreferrer"
               class="inline-flex items-center px-6 py-3 bg-blue-600 text-white font-bold rounded-full shadow-lg hover:bg-blue-700 transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-75">
                <svg class="w-6 h-6 mr-2" fill="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.828.092-.643.354-1.088.643-1.333-2.22-.253-4.555-1.119-4.555-4.934 0-1.089.389-1.979 1.029-2.679-.103-.253-.446-1.266.099-2.64 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.373.202 2.387.099 2.64.64.7 1.028 1.59.1028 2.679 0 3.823-2.339 4.681-4.566 4.925.359.309.678.92.678 1.855 0 1.336-.012 2.419-.012 2.747 0 .268.18.58.688.482C21.137 20.281 24 16.516 24 12.017 24 6.484 19.522 2 14 2h-2z" clip-rule="evenodd"></path></svg>
                Visit My GitHub
            </a>
        </section>
    </div>

    <script>
        // JavaScript for animations and dynamic content

        // 1. Typing Effect for Introduction
        const introTextElement = document.getElementById('intro-text');
        const fullIntroText = "Hello there! I'm Soumya Sagar, a passionate and aspiring developer embarking on an exciting journey into the world of code. As a new fresher, I'm eager to learn, build, and innovate.";
        let introCharIndex = 0;

        function typeIntroText() {
            if (introCharIndex < fullIntroText.length) {
                introTextElement.textContent += fullIntroText.charAt(introCharIndex);
                introCharIndex++;
                setTimeout(typeIntroText, 50); // Adjust typing speed here (milliseconds per character)
            } else {
                introTextElement.classList.remove('typing-text'); // Remove cursor after typing
            }
        }

        // 2. Code Rain Animation
        const codeRainContainer = document.getElementById('code-rain');
        const codeCharacters = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz!@#$%^&*()_+{}[]|:;"<>,.?/~`';

        function createCodeDrop() {
            const drop = document.createElement('span');
            drop.classList.add('code-drop');
            drop.style.left = Math.random() * 100 + 'vw';
            drop.style.animationDuration = (Math.random() * 5 + 3) + 's';
            drop.style.animationDelay = (Math.random() * 5) + 's';

            let codeString = '';
            const length = Math.floor(Math.random() * 10) + 5;
            for (let i = 0; i < length; i++) {
                codeString += codeCharacters.charAt(Math.floor(Math.random() * codeCharacters.length));
            }
            drop.textContent = codeString;

            codeRainContainer.appendChild(drop);

            drop.addEventListener('animationend', () => {
                drop.remove();
            });
        }

        // Generate initial code drops and then continuously add new ones
        const numberOfCodeDrops = 50;
        for (let i = 0; i < numberOfCodeDrops; i++) {
            createCodeDrop();
        }
        setInterval(createCodeDrop, 500);

        // 3. Particle Background Animation
        const particleContainer = document.getElementById('particle-container');
        const numberOfParticles = 70; // Adjust for desired density

        function createParticle() {
            const particle = document.createElement('div');
            particle.classList.add('particle');
            const size = Math.random() * 3 + 1; // Particle size (1-4px)
            particle.style.width = size + 'px';
            particle.style.height = size + 'px';
            particle.style.left = Math.random() * 100 + 'vw';
            particle.style.bottom = Math.random() * 100 + 'vh'; // Start from random bottom position
            particle.style.animationDuration = (Math.random() * 15 + 10) + 's'; // Float duration (10-25s)
            particle.style.animationDelay = (Math.random() * 10) + 's'; // Start delay

            // Custom CSS variables for animation
            particle.style.setProperty('--float-x', (Math.random() * 200 - 100) + 'px'); // Random horizontal drift
            particle.style.setProperty('--scale', (Math.random() * 0.5 + 0.5)); // Random scale variation

            particleContainer.appendChild(particle);

            particle.addEventListener('animationend', () => {
                particle.remove();
                createParticle(); // Recreate particle when one finishes
            });
        }

        for (let i = 0; i < numberOfParticles; i++) {
            createParticle();
        }

        // 4. Dynamic Coding Quotes
        const quotes = [
            { quote: "The only way to do great work is to love what you do.", author: "Steve Jobs" },
            { quote: "Any fool can write code that a computer can understand. Good programmers write code that humans can understand.", author: "Martin Fowler" },
            { quote: "First, solve the problem. Then, write the code.", author: "John Johnson" },
            { quote: "Experience is the name everyone gives to their mistakes.", author: "Oscar Wilde" },
            { quote: "Code is like humor. When you have to explain it, it’s bad.", author: "Cory House" }
        ];
        let currentQuoteIndex = 0;
        const quoteDisplay = document.getElementById('quote-display');

        function updateQuote() {
            quoteDisplay.style.opacity = 0; // Fade out
            setTimeout(() => {
                currentQuoteIndex = (currentQuoteIndex + 1) % quotes.length;
                const { quote, author } = quotes[currentQuoteIndex];
                quoteDisplay.innerHTML = `"${quote}"<br><span class="text-sm text-gray-400">- ${author}</span>`;
                quoteDisplay.style.opacity = 1; // Fade in
            }, 500); // Wait for fade out to complete
        }
        setInterval(updateQuote, 8000); // Change quote every 8 seconds

        // Initialize first quote
        window.onload = function() {
            const { quote, author } = quotes[currentQuoteIndex];
            quoteDisplay.innerHTML = `"${quote}"<br><span class="text-sm text-gray-400">- ${author}</span>`;
        };

        // 5. Contribution Insights Grid (Animated Placeholder)
        const contributionGrid = document.getElementById('contribution-grid');
        const numRows = 7; // Represents days of the week
        const numCols = 26; // Represents weeks (approx 6 months)

        function generateContributionGrid() {
            contributionGrid.innerHTML = ''; // Clear existing grid
            for (let i = 0; i < numRows; i++) {
                for (let j = 0; j < numCols; j++) {
                    const square = document.createElement('div');
                    let level;

                    // Simulate more recent contributions (towards the right/end of the grid)
                    // and generally higher levels for a "fresher" showing activity
                    if (j > numCols - 8) { // Last 8 weeks (more recent)
                        level = Math.floor(Math.random() * 3) + 2; // Levels 2, 3, 4 (more active)
                    } else if (j > numCols - 15) { // Weeks 9-15
                        level = Math.floor(Math.random() * 3) + 1; // Levels 1, 2, 3
                    } else { // Older weeks
                        level = Math.floor(Math.random() * 2); // Levels 0, 1
                    }

                    // Introduce some randomness to prevent perfect patterns
                    if (Math.random() < 0.1) { // 10% chance to drop a level
                        level = Math.max(0, level - 1);
                    }
                    if (Math.random() > 0.9) { // 10% chance to boost a level
                        level = Math.min(4, level + 1);
                    }

                    square.classList.add('contribution-square', `level-${level}`);
                    // Add a slight animation delay for a ripple effect
                    square.style.animationDelay = `${(i * 0.05) + (j * 0.02)}s`;
                    contributionGrid.appendChild(square);
                }
            }
        }

        // Regenerate the grid periodically for a dynamic feel
        setInterval(generateContributionGrid, 10000); // Regenerate every 10 seconds

        // Start all animations on window load
        window.onload = function() {
            typeIntroText();
            generateContributionGrid(); // Initial generation of the grid
        };
    </script>
</body>
</html>
