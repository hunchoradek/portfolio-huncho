<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const navItems = [
  { label: "About Me", href: "#about" },
  { label: "Projects", href: "#projects" },
  { label: "Education", href: "#education" },
  { label: "Skills", href: "#skills" },
  { label: "Contact", href: "#contact" }
]
const activeNav = ref("About Me")
const projects = [
  {
    title: "Walory App",
    description: "A SPA web application done in Vue.js and .NET for backend. It allows users to create, manage and share their own personal collections of items.",
    icon: "🪙",
    type: "Group",
    github: "https://github.com/KasmyrA/Walory"
  },
  {
    title: "Spotify Stats Website",
    description: "Website used for displaying Spotify statistics. It allows users to view their listening habits, favorite tracks, and more. It also creates personalized playlists based on user preferences. Done in Flask and Bootstrap.",
    icon: "🎵",
    type: "Solo",
    github: "https://github.com/hunchoradek/huncho-spotify-web-app"
  },
  {
    title: "Portfolio Website",
    description: "The website you are viewing right now! This portfolio website showcases my skills, projects, and experience. It is built with Vue.js and Tailwind CSS, providing a modern and responsive design.",
    icon: "💻",
    type: "Solo",
    github: "https://github.com/hunchoradek/portfolio-huncho"
  },
  {
    title: "FPL Machine Learning",
    description: "An AI model that predicts Fantasy Premier League (FPL) player performance using machine learning algorithms. It analyzes player statistics and provides insights for better team selection. Built with scikit-learn and Pandas and tensorflow.",
    icon: "⚽",
    type: "Solo",
    github: "https://github.com/hunchoradek/FPL-Machine-Learning-Project"
  },
  {
    title: "Cleopatra Beauty Salon",
    description: "Web application for a beauty salon, allowing customers to book appointments. Second portion of the web application allows managers to manage workers schedule, items needed and manage the whole salon. Built with React and Node.js.",
    icon: "📝",
    type: "Group",
    github: "https://github.com/hunchoradek/wt15_cleopatra"
  },
  {
    title: "Event Admin",
    description: "A C# application for managing events, allowing users to create, edit, and delete events. It provides a user-friendly interface for event organizers to manage their events efficiently.",
    icon: "📅",
    type: "Solo",
    github: "https://github.com/hunchoradek/Event-Admin-csharp"
  }
]

const typewriterTexts = [
  "Software Engineer",
  "Web Developer",
  "Open Source Enthusiast",
  "Tech Lover",
  "Lifelong Learner"
]
const typewriter = ref("")
let currentText = 0
let charIndex = 0
let isDeleting = false

function type() {
  const fullText = typewriterTexts[currentText]
  if (!isDeleting) {
    typewriter.value = fullText.substring(0, charIndex + 1)
    charIndex++
    if (charIndex === fullText.length) {
      setTimeout(() => { isDeleting = true; type() }, 1200)
      return
    }
  } else {
    typewriter.value = fullText.substring(0, charIndex - 1)
    charIndex--
    if (charIndex === 0) {
      isDeleting = false
      currentText = (currentText + 1) % typewriterTexts.length
    }
  }
  setTimeout(type, isDeleting ? 50 : 100)
}

onMounted(() => {
  type()
  window.addEventListener('scroll', onScroll)
})
onUnmounted(() => {
  window.removeEventListener('scroll', onScroll)
})

function setActiveNav(label: string) {
  activeNav.value = label
}

function onScroll() {
  const sectionIds = [
    { label: "About Me", id: "about" },
    { label: "Projects", id: "projects" },
    { label: "Education", id: "education" },
    { label: "Skills", id: "skills" },
    { label: "Contact", id: "contact" }
  ]
  const scrollPosition = window.scrollY + 120

  for (let i = sectionIds.length - 1; i >= 0; i--) {
    const section = document.getElementById(sectionIds[i].id)
    if (section && section.offsetTop <= scrollPosition) {
      activeNav.value = sectionIds[i].label
      break
    }
  }
}
</script>

<template>
      <header class="sticky top-0 z-50 bg-[#232425] rounded-b-2xl px-6 py-4 flex flex-col md:flex-row items-center justify-between shadow-lg">
      <div class="text-2xl font-extrabold text-white tracking-tight mb-4 md:mb-0">Radosław</div>
      <nav class="flex gap-2 md:gap-6 w-full md:w-auto justify-center md:justify-end">
        <a
          v-for="item in navItems"
          :key="item.label"
          :href="item.href"
          @click="setActiveNav(item.label)"
          class="relative px-4 py-2 rounded-t-xl font-semibold transition text-gray-200"
          :class="{
            'text-green-400 bg-[#18191A] shadow-md': activeNav === item.label,
            'hover:text-green-400': activeNav !== item.label
          }"
        >
          {{ item.label }}
          <span
            v-if="activeNav === item.label"
            class="absolute left-1/2 -bottom-1 -translate-x-1/2 w-8 h-1 bg-green-400 rounded-full"
          ></span>
        </a>
      </nav>
    </header>
  <div class="min-h-screen bg-[#18191A] text-white font-sans">
    <section class="w-full bg-[#18191A] px-4 py-12 md:py-20 flex flex-col items-center">
      <div class="max-w-4xl w-full mx-auto">
        <h1 class="text-4xl md:text-6xl font-extrabold text-white mb-2 flex items-center gap-2">
          Hi, I'm <span class="text-green-400">Radosław</span> <span class="text-3xl md:text-5xl"></span>
        </h1>
        <div class="text-2xl md:text-3xl font-semibold text-white mb-2">
          I'm a <span class="text-green-400">{{ typewriter }}</span><span class="animate-pulse text-green-400">|</span>
        </div>
        <div class="text-lg md:text-xl text-gray-300 font-semibold">
          Welcome to my portfolio!
        </div>
      </div>
    </section>

    <div class="max-w-4xl mx-auto px-2 md:px-0">
      <section id="about" class="flex flex-col md:flex-row items-center gap-8 bg-[#232425] rounded-2xl px-6 py-12 mt-8 mb-8 shadow">
        <div class="flex flex-col items-center md:items-start w-full md:w-1/3">
          <img
            src="https://randomuser.me/api/portraits/men/32.jpg"
            alt="Your Photo"
            class="mx-auto w-48 h-48 rounded-full mb-6 shadow-2xl object-cover drop-shadow-2xl"
          />
          <div class="flex gap-4 justify-center w-full">
            <a href="https://linkedin.com/" target="_blank" rel="noopener" class="bg-green-600 hover:bg-green-500 text-white px-4 py-2 rounded-full font-semibold transition flex items-center gap-2">
              LinkedIn
            </a>
            <a href="https://github.com/" target="_blank" rel="noopener" class="bg-gray-800 hover:bg-gray-700 text-white px-4 py-2 rounded-full font-semibold transition flex items-center gap-2">
              GitHub
            </a>
          </div>
        </div>
        <div class="w-full md:w-2/3 mt-8 md:mt-0 md:pl-8">
          <h2 class="text-2xl font-bold mb-4">About Me</h2>
          <p class="text-gray-200 mb-3">
            I'm Radosław, a passionate developer and designer from Silesia, Poland. I love building modern, user-friendly web experiences and exploring new technologies.
          </p>
          <p class="text-gray-400">
            My focus is on creating functional and attractive digital products. I enjoy collaborating with others, learning new things, and sharing knowledge with the community. Let's connect!
          </p>
        </div>
      </section>
      <section id="projects" class="mb-8">
        <h3 class="text-2xl font-bold mb-2">What I'm Doing</h3>
        <div class="w-12 h-1 bg-green-400 rounded mb-6"></div>
        <div class="grid md:grid-cols-2 gap-6">
          <div
            v-for="project in projects"
            :key="project.title"
            class="bg-[#232425] rounded-2xl p-6 flex flex-col gap-4 border border-transparent hover:border-green-400 transition shadow"
          >
            <div class="flex items-center gap-2">
              <span class="text-3xl text-green-400">{{ project.icon }}</span>
              <span
                class="ml-auto px-3 py-1 rounded-full text-xs font-bold"
                :class="project.type === 'Group' ? 'bg-green-900 text-green-300' : 'bg-gray-700 text-gray-200'"
              >
                {{ project.type }}
              </span>
            </div>
            <div>
              <h4 class="font-bold text-lg mb-1">{{ project.title }}</h4>
              <p class="text-gray-300 mb-3">{{ project.description }}</p>
              <a
                :href="project.github"
                target="_blank"
                rel="noopener"
                class="inline-flex items-center gap-2 bg-green-600 hover:bg-green-500 text-white px-4 py-2 rounded-full font-semibold transition shadow"
              >
                <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M12 .5c-6.62 0-12 5.38-12 12 0 5.3 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.085 1.84 1.237 1.84 1.237 1.07 1.834 2.809 1.304 3.495.997.108-.775.418-1.305.762-1.605-2.665-.304-5.466-1.334-5.466-5.931 0-1.31.469-2.381 1.236-3.221-.124-.303-.535-1.523.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.984-.399 3.003-.404 1.019.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.873.119 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.803 5.625-5.475 5.921.43.371.823 1.102.823 2.222v3.293c0 .322.218.694.825.576 4.765-1.587 8.2-6.086 8.2-11.385 0-6.62-5.38-12-12-12z"/>
                </svg>
                GitHub
              </a>
            </div>
          </div>
        </div>
      </section>

      <section id="education" class="bg-[#232425] rounded-2xl px-6 py-8 mb-8 shadow">
        <h2 class="text-2xl font-bold mb-2">Education</h2>
        <div class="w-12 h-1 bg-green-400 rounded mb-6"></div>
        <div class="flex flex-col gap-10">
          <div class="flex flex-col md:flex-row items-center gap-8">
            <div class="flex flex-col items-center w-full md:w-1/4">
              <img
                src="https://images.unsplash.com/photo-1506744038136-46273834b3fb?auto=format&fit=facearea&w=256&q=80"
                alt="School 1"
                class="w-32 h-32 rounded-xl object-cover shadow-lg mb-3"
              />
              <span class="bg-green-900 text-green-300 px-3 py-1 rounded-full text-xs font-semibold mt-2">
                2021 - 2026
              </span>
            </div>
            <div class="w-full md:w-3/4">
              <h3 class="text-xl font-bold mb-1">Silesian Univeristy of Technology</h3>
              <div class="text-green-400 font-semibold mb-2">BSc Computer Science</div>
              <p class="text-gray-300">
                Studied core computer science concepts, software engineering, and participated in various projects and hackathons. Developed strong programming and teamwork skills.
              </p>
            </div>
          </div>
          <div class="flex flex-col md:flex-row items-center gap-8">
            <div class="flex flex-col items-center w-full md:w-1/4">
              <img
                src="https://images.unsplash.com/photo-1464983953574-0892a716854b?auto=format&fit=facearea&w=256&q=80"
                alt="School 2"
                class="w-32 h-32 rounded-xl object-cover shadow-lg mb-3"
              />
              <span class="bg-green-900 text-green-300 px-3 py-1 rounded-full text-xs font-semibold mt-2">
                2017 - 2021
              </span>
            </div>
            <div class="w-full md:w-3/4">
              <h3 class="text-xl font-bold mb-1">ZSTI Gliwice (High School)</h3>
              <div class="text-green-400 font-semibold mb-2">IT Technician profile</div>
              <p class="text-gray-300">
                Focused on advanced mathematics and physics, participated in olympiads and science clubs. Built a strong analytical foundation for further studies.
              </p>
            </div>
          </div>
        </div>
      </section>

      <section id="skills" class="bg-[#232425] rounded-2xl px-6 py-8 mb-8 shadow">
        <h2 class="text-2xl font-bold mb-2">Skills</h2>
        <div class="w-12 h-1 bg-green-400 rounded mb-6"></div>
        <p class="text-gray-300">Your skills go here.</p>
      </section>

      <section id="contact" class="bg-[#232425] rounded-2xl px-6 py-8 mt-12 shadow">
        <h2 class="text-2xl font-bold mb-2">Contact</h2>
        <div class="w-12 h-1 bg-green-400 rounded mb-6"></div>
        <p class="text-gray-300 mb-4">Feel free to reach out for collaborations or just a friendly hello!</p>
        <a href="mailto:your@email.com" class="inline-block bg-green-600 text-white px-6 py-2 rounded-full hover:bg-green-500 transition font-semibold shadow">
          Email Me
        </a>
      </section>

      <footer class="text-center text-gray-600 py-6 text-sm mt-8">
        © {{ new Date().getFullYear() }} <span class="text-green-400">Your Name</span>. All rights reserved.
      </footer>
    </div>
  </div>
</template>