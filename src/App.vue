<script setup>
import HeadBar from './components/HeadBar.vue'
import Greeting from './components/Greeting.vue'
import WhatIDo from './components/WhatIDo.vue'
import Resume from './components/Resume.vue'
import Portfolio from './components/Portfolio.vue'

const name = 'Marat Morozov'
const position = 'Full Stack Developer'
const description = 'My goal is to turn complex ideas into elegant solutions. With expertise in both frontend and backend development, I create seamless digital experiences that bring your vision to life.'
const technologies = ['Vue', 'Python', 'Celery', 'SQL', 'Docker',]
const socialLinks = [
  {
    name: 'GitHub',
    url: 'https://github.com/MaratFfrost',
    icon: 'fab fa-github',
    color: '#333'
  },
  {
    name: 'Telegram',
    url: 'https://t.me/mamkin_modnik',
    icon: 'fab fa-telegram',
    color: '#0088cc'
  },
  {
    name: 'Email',
    url: 'mailto:morozovmarat4@gmailcom',
    icon: 'fas fa-envelope',
    color: '#d44638'
  }
]
const bioText = 'Ambitious Math/CS student at BSU, Web Development Enthusiast, Emerging Technologies Explorer Currently pursuing a degree in Mathematics & Mechanics while actively mastering modern web technologies. Passionate about applying analytical thinking to solve complex development challenges and create innovative digital solutions.'

</script>

<template>

  <HeadBar :name="name" :position="position" photoUrl="public/myphoto.jpg" />
  <Greeting :socialLinks="socialLinks" :position="position" :description="description" :technologies="technologies" />
  <WhatIDo />
  <Resume :bioText="bioText" />
  <Portfolio></Portfolio>

</template>

<style noscoped>
html,
body {
  overflow-x: hidden;
  background: #000000;
  font-family: 'Montserrat', sans-serif;
}
</style>
